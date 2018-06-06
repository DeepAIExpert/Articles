## 背景
  有时需要将信息快速获取到数据库中。 SQLite是一个轻量级数据库引擎，可以轻松嵌入到应用程序中。 这将涵盖优化大容量插入到SQLite数据库的过程。 
  虽然本文重点介绍SQLite，但此处显示的一些技术将适用于其他数据库。以下所有示例都将数据插入到同一个表中。
  这是一张表，其中ID是第一个元素，后面跟着三个FLOAT值，然后是三个INTEGER值。

## 分析
### *逐条插入*
  这是将记录插入SQLite的最基本的方法。 每个记录的查询调用一次sqlite3_exec。
  
  示例代码：
  
    
    char buffer[300];
    for (unsigned i = 0; i < mVal; i++)
    {
        sprintf(buffer, "INSERT INTO example VALUES ('%s', %lf, %lf, %lf, %d, %d, %d)",
                getID().c_str(), getDouble(), getDouble(), getDouble(),
                getInt(), getInt(), getInt());
        sqlite3_exec(mDb, buffer, NULL, NULL, NULL);
    }
    

### *合并 Transaction*
  事务是将SQL语句组合在一起的一种方式。如果遇到错误，可以使用ON CONFLICT语句来定义错误处理。用END或者COMMIT来关闭和写入事务，然后将内容写入SQLite数据库。
  实例代码:
  
    
    char* errorMessage;
    sqlite3_exec(mDb, "BEGIN TRANSACTION", NULL, NULL, &errorMessage);
    
    char buffer[300];
    for (unsigned i = 0; i < mVal; i++)
    {
    	sprintf(buffer, "INSERT INTO example VALUES ('%s', %lf, %lf, %lf, %d, %d, %d)",
    			getID().c_str(), getDouble(), getDouble(), getDouble(),
    			getInt(), getInt(), getInt());
    	sqlite3_exec(mDb, buffer, NULL, NULL, NULL);
    }
    
    sqlite3_exec(mDb, "COMMIT TRANSACTION", NULL, NULL, &errorMessage);
    
	
### *PRAGMA 语句*
  PRAGMA语句控制整个SQLite的行为。 它们可以用来调整选项
  例如将数据刷新到缓存大小的磁盘的频率。 这些是通常用于性能的一些。
  SQLite文档充分说明了它们的作用和使用它们的含义。 例如，同步关闭会导致SQLite停止并等待数据写入硬盘。在发生崩溃或电源故障时，数据库可能会损坏。
  实例代码:
  
    
    sqlite3_exec(mDb, "PRAGMA synchronous=OFF", NULL, NULL, &errorMessage);
    sqlite3_exec(mDb, "PRAGMA count_changes=OFF", NULL, NULL, &errorMessage);
    sqlite3_exec(mDb, "PRAGMA journal_mode=MEMORY", NULL, NULL, &errorMessage);
    sqlite3_exec(mDb, "PRAGMA temp_store=MEMORY", NULL, NULL, &errorMessage);
    

### *预解析 Statement*
  预解析 Statement是一种高效的查询方式。 解析器只需要在批量查询语句上运行一次，而不是一遍又一遍地解析语句。根据文档，sqlite3_exec是一个便捷函数，
  里面调用了sqlite3_prepare_v2（），sqlite3_step（），然后调用sqlite3_finalize（）。个人认为文档应该明确地指出 预解析的查询方式是首选的查询方法。
  sqlite3_exec（）只适合用于一次性的查询。
  
  示例代码：
  
    
    char* errorMessage;
    sqlite3_exec(mDb, "BEGIN TRANSACTION", NULL, NULL, &errorMessage);
     
    char buffer[] = "INSERT INTO example VALUES (?1, ?2, ?3, ?4, ?5, ?6, ?7)";
    sqlite3_stmt* stmt;
    sqlite3_prepare_v2(mDb, buffer, strlen(buffer), &stmt, NULL);
     
    for (unsigned i = 0; i < mVal; i++)
    {
        std::string id = getID();
        sqlite3_bind_text(stmt, 1, id.c_str(), id.size(), SQLITE_STATIC);
        sqlite3_bind_double(stmt, 2, getDouble());
        sqlite3_bind_double(stmt, 3, getDouble());
        sqlite3_bind_double(stmt, 4, getDouble());
        sqlite3_bind_int(stmt, 5, getInt());
        sqlite3_bind_int(stmt, 6, getInt());
        sqlite3_bind_int(stmt, 7, getInt());
     
        if (sqlite3_step(stmt) != SQLITE_DONE)
        {
            printf("Commit Failed!\n");
        }
     
        sqlite3_reset(stmt);
    }
     
    sqlite3_exec(mDb, "COMMIT TRANSACTION", NULL, NULL, &errorMessage);
    sqlite3_finalize(stmt);
    

### *数据用Binary Blob类型存储*
  到目前为止，上面的优化已经包含了批量查询的最常用的优化方法。但是在另一个方面，如果你没有对某些数据进行查询的必要，可以将其存储为一个blob。
  虽然不建议将所有内容都放到一个blob中存储到数据库中，但某些情况下这么做是有意义的。
  例如，如果你有一个由REAL类型的数值组成的点类（x，y，z），那么可以将它们存储在一个blob中而不是三个单独的存放。
  随着更多字段被转换为更大的blob，这种方法的性能就越能提升。
  示例代码：
  
    
    char* errorMessage;
    sqlite3_exec(mDb, "BEGIN TRANSACTION", NULL, NULL, &errorMessage);
     
    char buffer[] = "INSERT INTO example VALUES (?1, ?2, ?3, ?4, ?5)";
    sqlite3_stmt* stmt;
    sqlite3_prepare_v2(mDb, buffer, strlen(buffer), &stmt, NULL);
     
    for (unsigned i = 0; i < mVal; i++)
    {
        std::string id = getID();
        sqlite3_bind_text(stmt, 1, id.c_str(), id.size(), SQLITE_STATIC);
     
        char dblBuffer[24];
        double d[] = {getDouble(), getDouble(), getDouble()};
        memcpy(dblBuffer, (char*)&d, sizeof(d));
        sqlite3_bind_blob(stmt, 2, dblBuffer, 24, SQLITE_STATIC);
        sqlite3_bind_int(stmt, 3, getInt());
        sqlite3_bind_int(stmt, 4, getInt());
        sqlite3_bind_int(stmt, 5, getInt());
     
        int retVal = sqlite3_step(stmt);
        if (retVal != SQLITE_DONE)
        {
            printf("Commit Failed! %d\n", retVal);
        }
     
        sqlite3_reset(stmt);
    }
     
    sqlite3_exec(mDb, "COMMIT TRANSACTION", NULL, NULL, &errorMessage);
    sqlite3_finalize(stmt);
    

## 性能对比图
  #### *各方法不同数量的插入动作的运行时间*
  
  ![](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/bulk_insert_runtime.png)
  
  #### *各方法不同数量的插入的每秒插入记录数*
  
  ![](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/inserts_per_second.png)
  
  #### *BLOB&Stetement不同数量的插入动作的运行时间*
  
  ![](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/big_insert_runtime.png)
  
  #### *BLOB&Stetement不同数量的插入的每秒插入记录数*
  
  ![](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/big_insert_per_second.png)
