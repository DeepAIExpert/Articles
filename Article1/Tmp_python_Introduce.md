# Python
Python 是一种面向对象的解释型计算机程序设计语言，由荷兰人Guido van Rossum于1989年发明，第一个公开发行版发行于1991年，是一个非常优秀的编程语言。

Python 具有非常强大的库，并且它能够比较轻松地把基于其他语言的模块联结在一起，组成整个程序，而每个模块则单独使用利于实现该功能的最优语言编写。一个常见的应用场景是，Python 快速生成程序原型，对其中有性能要求的模块，用 C/C++ 重写。这里还可以引出一个事实，人工智能上面最受欢迎的语言 TensorFlow 就是用 Python 去组建各个部件的，TensorFlow 运算核心是 Eigen（高性能C ++和CUDA库）和 NVidia 的 cuDNN（用于 NVidia GPU 的非常优化的 DNN 库，用于卷积等功能）。

另外，值得一提的是，7月20日IEEE发布2017年编程语言排行榜：Python高居首位，其受欢迎程度可见一斑。

不仅在工作中，Python 是强而有力的工具，在日常生活中，Python 也能完成一些很好玩的功能，例如我们下面介绍的一个小功能，就是利用 Python 去定时获取 Bing 上的高清壁纸。

![avatar](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/python_pic1.PNG)

不得不说，[(Bing(必应)](www.bing.com)上面的壁纸，质量还是很可以的。花几分钟，写一个 Python 脚本，每天把高清图片资源下载到一个文件夹，然后把壁纸设置成这个文件夹，每几分钟壁纸就轮换一次，这种感觉非常好呢。
