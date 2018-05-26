
## Bash是什么？

不就是一个人机交互界面嘛，我们以前习惯点点按钮，现在我们习惯一下敲敲命令

## Bash举个栗子？

* 高效的文件查找——find
隔壁老王说他阅片无数，为了证明这个事实，我们在他的电脑上实施
```
find / -iname "yo-ho"
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
```
结果老王求我不要贴出来。
![alt text](https://raw.githubusercontent.com/DeepAIExpert/Articles/master/Article1/suprising.jpg "想不到吧!")
