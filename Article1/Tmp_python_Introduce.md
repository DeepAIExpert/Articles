## _Python_ 自动壁纸更新系统
* ### 什么是 _Python_
_Python_ 是一种面向对象的解释型计算机程序设计语言，由荷兰人 _Guido van Rossum_ 于1989年发明，第一个公开发行版发行于 1991 年，是一个非常优秀的编程语言。

_Python_ 具有非常强大的库，并且它能够比较轻松地把基于其他语言的模块联结在一起，组成整个程序，而每个模块则**单独**使用利于实现该功能的最优语言编写。一个常见的应用场景是，_Python_ 快速生成程序原型，对其中有性能要求的模块，用 _C/C++_ 重写。这里还可以引出一个事实，**人工智能**上面最受欢迎的语言 **_TensorFlow_** 就是用 _Python_ 去组建各个部件的。_TensorFlow_ 运算核心是 _Eigen_（_C++_） 和 _NVidia_ 的 _cuDNN_（_C++_），[(_Google_(谷歌)](www.google.com) 的工程师们凭借 _Python_，把这两个核心紧密串联在一起，形成了人工智能上面最广为使用的编程架构。

另外，值得一提的是，7月20日 _IEEE_ 发布 2017 年编程语言排行榜：_Python_ **高居首位**，其受欢迎程度可见一斑。

* ### _Python_ 的一些应用（_文末附带壁纸下载_）
不仅在工作中，_Python_ 是强而有力的工具，在日常生活中，_Python_ 也能完成一些很好玩的功能，例如我们下面介绍的一个小功能，就是利用 _Python_ 去定时获取 [(Bing(必应)](www.bing.com) 上的高清壁纸。

![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/python_pic1.PNG)

必应首页，每天都会更新一张独特的高精壁纸，不得不说，里面壁纸的质量还是很可以的。上面所展示的就是一部分我从必应保存下来的优质壁纸，我现在是每几分钟壁纸就轮换一张，每天、每时每刻都是如此独特。**想象一下**，花几分钟写一个 _Python_ 脚本，就可以让电脑每天自动把壁纸（甚至是其他一些关注的东西）自动保存起来，每天自动下载保存高清壁纸，而不是以人手的方式去保存这些壁纸（_基本上坚持不下来_），这种感觉非常好呢。 

* #### 具体实现思路
  * 利用 _Python_ 的 _urllib_ 模块获取网页的全部内容
  * 利用 _Python_ 的 _re_ 模块进行网页正则分析，找到目标壁纸
  * 利用 _Python_ 的 _urllib_ 模块进行壁纸下载，保存至某一特定文件夹
  * 将该文件夹设置成壁纸，即可以实现系统壁纸每天自动更新
  
可以看到，整个思路比较简洁、清晰，而 _Python_ 就是这样一种工具，学会了运用 _Python_ ，对个人能力、生活趣味的提升，都有积极作用。而这个小工具的代码，前后也**不超过五十行**，是非常简单、有趣的实现。

![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/python_pic2.PNG)




* ### 精选一部分优质壁纸展示

![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/AmalfiCathedral_ZH-CN9007250446_1920x1080.jpg)
---




![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/AeoniumLeaf_ZH-CN7490448951_1920x1080.jpg)
---




![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/BingWallpaper-2017-03-12.jpg)
---




![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/BlueMushroom_ZH-CN10091152411_1920x1080.jpg)
---




![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/MesseHall_ZH-CN8032841463_1920x1080.jpg)
---




![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/RoyalBarge_ZH-CN8556739705_1920x1080.jpg)
---




![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/BingWallpaper-2017-05-14.jpg)
---




![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/BingWallpaper-2017-05-16.jpg)
---




![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/BigHornSheep_ZH-CN6358178150_1920x1080.jpg)
---




![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/BingWallpaper-2016-03-21.jpg)
---




![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/AustrianAlpineMarmots_ZH-CN10896836289_1920x1080.jpg)
---




![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/WindmillLighthouse_ZH-CN12870536851_1920x1080.jpg)
---





* ### _Python_ 其他应用 与 就业前景
上面我们简单介绍了 _Python_ ，以及用 _Python_ 实现的一个比较有意思的东西，但其实上，_Python_ 可以做到的事情还有非常非常多。
  * **网络爬虫**

网络爬虫是 _Python_ 比较常用的一个场景，国际上，_google_ 在早期大量地使用 _Python_ 语言作为网络爬虫的基础，带动了整个 _Python_ 语言的应用发展。以前国内很多人用采集器搜刮网上的内容，现在用 _Python_ 收集网上的信息比以前容易很多了，本文的工具也是其中一个例子。
  * **人工智能与机器学习**

人工智能是现在非常火的一个方向，AI 热潮让 _Python_ 语言的未来充满了无限的潜力。现在释放出来的几个非常有影响力的 AI 框架，大多是 _Python_ 的实现，为什么呢？因为 _Python_ 足够动态、具有足够性能，这是AI技术所需要的技术特点。比如基于Python的深度学习库、深度学习方向、机器学习方向、自然语言处理方向的一些网站基本都是通过Python来实现的。
  * **数据分析处理**

数据分析处理方面，_Python_ 有很完备的生态环境。“大数据”分析中涉及到的分布式计算、数据可视化、数据库操作等，_Python_ 中都有成熟的模块可以选择完成其功能。对于 _Hadoop-MapReduce_ 和 _Spark_，都可以直接使用 _Python_ 完成计算逻辑。这无论对于数据科学家还是对于数据工程师而言都是十分便利的。
  * **服务器运维及其它小工具**

_Python_ 对于服务器运维而言也有十分重要的用途。由于目前几乎所有 _Linux_ 发行版中都自带了 _Python_ 解释器，使用 _Python_ 脚本进行批量化的文件部署和运行调整都成了 _Linux_ 服务器上很不错的选择。_Python_ 中也包含许多方便的工具，从调控 _ssh/sftp_ 用的 _paramiko_，到监控服务用的 _supervisor_，再到 _bazel_ 等构建工具，甚至 _conan_ 等用于 _C++_ 的包管理工具，_Python_ 提供了全方位的工具集合，而在这基础上，结合 _Web_，开发方便运维的工具会变得十分简单。

纵上所述，_Python_ 在未来具有很好的前景，而掌握了这一门语言，能让你的职业规划更多完善，走进更好的平台，从而**更好地实现人生价值**。

* #### 壁纸包下载地址
由于壁纸数量太多，需要完整壁纸包的，可以私信了解。
链接: https://pan.baidu.com/s/1KYvjlKFs0d7gZsDZNnhzrg 密码: q2jr

