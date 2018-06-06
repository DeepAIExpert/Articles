## 背景
  有时云盘目录包含的文件数量非常庞大，轻办公需要在用户进入到目录的时刻把云端文件信息同步写到数据库，几百K的文件 需要占满单核几十分钟。
  虽然下面重点是介绍SQLite 批量插入的几种优化方法，但是其中一些方法同样适用其他类型数据库。第三部分简单介绍了建表和查询语句的注意事项。
  以下所有示例都将数据插入到同一个表中。
  这张表有7个字段，其中ID是第一个元素，后面跟着三个FLOAT类型的字段，最后是三个INTEGER类型的字段。

## 插入方式的优化

### *逐条插入*
  这是将记录插入SQLite的最基本的方法。每个记录的查询调用一次sqlite3_exec。
  
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
  PRAGMA语句控制整个SQLite的行为。 它们可以用来设置Sqlite的选项，例如将数据刷新到磁盘的频率。
  以下是关闭同步机制 提升写入性能的一些设置。具体可以参考一下SQLITE的官方文档。
  但是同步机制关闭会导致SQLite停止并等待数据写入硬盘。在崩溃或电源故障发生时，数据库可能会损坏。
  实例代码:
  
    
    sqlite3_exec(mDb, "PRAGMA synchronous=OFF", NULL, NULL, &errorMessage);
    sqlite3_exec(mDb, "PRAGMA count_changes=OFF", NULL, NULL, &errorMessage);
    sqlite3_exec(mDb, "PRAGMA journal_mode=MEMORY", NULL, NULL, &errorMessage);
    sqlite3_exec(mDb, "PRAGMA temp_store=MEMORY", NULL, NULL, &errorMessage);
    

### *预解析 Statement*
  预解析 Statement 是一种高效的查询方式。 解析器只需要在批量查询语句上运行一次，而不是一遍又一遍地解析语句。根据文档，sqlite3_exec是一个便捷函数，
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
  到目前为止，上面的优化已经包含了批量查询的最常用的优化方法。但是在另一个方面，如果你没有对某些数据进行查询的需求，可以将其存储为一个BLOB。
  虽然不建议将所有内容都放到一个blob中存储到数据库中，但某些情况下这么做是有意义的。
  例如，如果你有一个由REAL类型的数值组成的点类（x，y，z），那么可以将它们存储在一个BLOB中而不是三个单独的存放。
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
    

### 性能对比图
  #### *各方法不同数量的插入动作的运行时间*
  
  ![](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/bulk_insert_runtime.png)
  
  #### *各方法不同数量的插入的每秒插入记录数*
  
  ![](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/inserts_per_second.png)
  
  #### *BLOB&Stetement不同数量的插入动作的运行时间*
  
  ![](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/big_insert_runtime.png)
  
  #### *BLOB&Stetement不同数量的插入的每秒插入记录数*
  
  ![](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/big_insert_per_second.png)

### 插入方法总结
  * 最原始的逐条插入性能最差，永远都不是批量写入的最佳选择。
  * Transaction 合并能带来一些性能提升，在大量的并且查询&写入方式不同的情景下，它是一个不错的选择。如果查询&写入方式相同，这种方式还有很大的提升空间。
  * 对于查询&写入方式相同的大量操作，它是性能最好的方法。
  * 对于不会被用来查询并且逻辑上适合放一起的表字段以BLOB形式存在数据库，还能带来一些性能提升。
  * PRAGMA 选项设置来提升写入效率 确实有效，但在有些异常情况下, 数据库可能会损坏。
  
## 建表与查询语句
  #### 建表之前明确好存储字段，找到真正的 *Primary Key*
    反例：
    CREATE TABLE t1(id UNIQUE Primary Key, fileId UNIQUE, Number);
    
    插入数据到表中：
    "insert or replace into table (id, fileId, Number) (select id from table where fileId = '1?'), ?2, ?3)
    
    id 在这是多余的，并且大幅增加了查询和写入语句算法复杂，每条插入语句都要进行一次基于fileId的查询，
    这个查询复杂度随着表的大小不断增长。

  #### 修改之后
    CREATE TABLE t1(fileId Primary Key UNIQUE, Number);

    插入数据到表中:
    insert or replace into table (fileId, Number) (1?, 2?)

## 优化之后的结果：
  1000K个记录整个插入过程持续几秒，CPU占用单核3%以内。
