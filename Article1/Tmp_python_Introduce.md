## _Python_
* ### 什么是 _Python_
_Python_ 是一种面向对象的解释型计算机程序设计语言，由荷兰人 _Guido van Rossum_ 于1989年发明，第一个公开发行版发行于 1991 年，是一个非常优秀的编程语言。

_Python_ 具有非常强大的库，并且它能够比较轻松地把基于其他语言的模块联结在一起，组成整个程序，而每个模块则**单独**使用利于实现该功能的最优语言编写。一个常见的应用场景是，_Python_ 快速生成程序原型，对其中有性能要求的模块，用 _C/C++_ 重写。这里还可以引出一个事实，**人工智能**上面最受欢迎的语言 _TensorFlow_ 就是用 _Python_ 去组建各个部件的，_TensorFlow_ 运算核心是 _Eigen_（_高性能 C++ 和 CUDA 库_）和 _NVidia_ 的 _cuDNN_（_用于 NVidia GPU 的非常优化的 DNN 库，用于卷积等功能_），[(_Google_(谷歌)](www.google.com) 的工程师们就是利用 _Python_，把这两个核心紧密串联在一起，形成了人工智能上面最广为使用的编程架构。

另外，值得一提的是，7月20日 _IEEE_ 发布 2017 年编程语言排行榜：_Python_ **高居首位**，其受欢迎程度可见一斑。

* ### _Python_ 的一些应用（_文末附带壁纸下载_）
不仅在工作中，_Python_ 是强而有力的工具，在日常生活中，_Python_ 也能完成一些很好玩的功能，例如我们下面介绍的一个小功能，就是利用 _Python_ 去定时获取 [(Bing(必应)](www.bing.com) 上的高清壁纸。

![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/python_pic1.PNG)

必应首页，每天都会更新一张独特的高精壁纸，不得不说，上面的壁纸质量还是很可以的。上面所展示的就是一部分我从必应保存下来的优质壁纸，我现在是每几分钟壁纸就轮换一遍，每天、每时每刻都是如此独特。**想象一下**，花几分钟写一个 _Python_ 脚本，就可以让电脑每天自动把壁纸（甚至是其他一些关注的东西）自动保存起来，而不是以人手的方式去保存这些壁纸（_基本上坚持不下来，并且会有水印_），这种感觉非常好呢。 

* #### 具体实现思路
  * 利用 _Python_ 的 _urllib_ 模块获取网页的全部内容
  * 利用 _Python_ 的 _re_ 模块进行网页正则分析，找到目标壁纸
  * 利用 _Python_ 的 _urllib_ 模块进行壁纸下载，保存至某一特定文件夹
  * 将该文件夹设置成壁纸，即可以实现系统壁纸每天自动更新
  
可以看到，整个思路比较简洁、清晰，而 _Python_ 就是这样一种工具，学会了运用 _Python_ ，对个人能力、生活趣味的提升，都有积极作用。而这个小工具的代码，前后也**不超过五十行**，是非常简单、有趣的实现。

![xxx](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/python_pic2.PNG)

* #### 精选一部分优质壁纸展示

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





* #### 壁纸包下载地址
由于壁纸数量太多，需要完整壁纸包的，或者想学编程的同学，可以私信了解。
链接: https://pan.baidu.com/s/1KYvjlKFs0d7gZsDZNnhzrg 密码: q2jr
