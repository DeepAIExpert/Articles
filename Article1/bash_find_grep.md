
## Bash是什么？

不就是一个人机交互界面嘛，我们以前习惯点点按钮，现在我们习惯一下敲敲命令

## Bash举个栗子？

* 高效的文件查找——find
隔壁老王说他阅片无数，为了证明这个事实，我们在他的电脑上实施
```
find / -iname "yo-ho"
# 表示忽略大小写查找文件名含有yo-ho的文件，从根目录(这个/符号就是根目录的意思)开始查找
```
得到以下结果：
```
Tokyo-Hot n0xxx.avi
...
Tokyo-Hot n1xxx.avi
...
```
给老王一句，老奶奶不扶就服你。
再来一个
```
find / -iname "yo-ho" | wc --line
# 查找结果是一行一行的文件名，把这些内容交给wc这个程序，让它算算有多少行(--line这个参数就是告诉wc，算出行数)
# 整个套路目的，就是看看含有yo-ho的文件有多少个
```
结果是
```
1024
```
老司机
![alt text](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/shehuisheshui.png "社会社会")
* 内容检索——grep
隔壁老王总是说，通过蓝色代码下载回来的torrent，文件名就是一串英文字母和数字，文件多了，就不知道对硬的内容是什么，我教他用grep，搜索文件内容，例如
```
grep -ri --include="*.torrent" "yo-ho" /
# 从根目录忽略大小写(-i参数)递归查找(-r参数，递归查找)文件内容含有yo-ho的torrent文件
```
结果老王求我不要贴出来。    

![alt text](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/suprising.jpg "想不到吧!")
