`dpkg -i `  安装deb包

cuda头文件在  `/usr/local/cuda/include` 中， 搜索 `grep -R ...`

查找 `find`

```

find [PATH] [option] [action]  
  
# 与时间有关的参数：  
-mtime n : n为数字，意思为在n天之前的“一天内”被更改过的文件；  
-mtime +n : 列出在n天之前（不含n天本身）被更改过的文件名；  
-mtime -n : 列出在n天之内（含n天本身）被更改过的文件名；  
-newer file : 列出比file还要新的文件名  
# 例如：  
find /root -mtime 0 # 在当前目录下查找今天之内有改动的文件  
  
# 与用户或用户组名有关的参数：  
-user name : 列出文件所有者为name的文件  
-group name : 列出文件所属用户组为name的文件  
-uid n : 列出文件所有者为用户ID为n的文件  
-gid n : 列出文件所属用户组为用户组ID为n的文件  
# 例如：  
find /home/ljianhui -user ljianhui # 在目录/home/ljianhui中找出所有者为ljianhui的文件  
  
# 与文件权限及名称有关的参数：  
-name filename ：找出文件名为filename的文件  
-size [+-]SIZE ：找出比SIZE还要大（+）或小（-）的文件  
-tpye TYPE ：查找文件的类型为TYPE的文件，TYPE的值主要有：一般文件（f)、设备文件（b、c）、  
             目录（d）、连接文件（l）、socket（s）、FIFO管道文件（p）；  
-perm mode ：查找文件权限刚好等于mode的文件，mode用数字表示，如0755；  
-perm -mode ：查找文件权限必须要全部包括mode权限的文件，mode用数字表示  
-perm +mode ：查找文件权限包含任一mode的权限的文件，mode用数字表示  
# 例如：  
find / -name passwd # 查找文件名为passwd的文件  
find . -perm 0755 # 查找当前目录中文件权限的0755的文件  
find . -size +12k # 查找当前目录中大于12KB的文件，注意c表示byte  
```





复制`cp   原地址  目标地址  -r`

  `ll`  相当于 `ls -l `查看文件的权限

```
在Linux中第一个字符代表这个文件是目录、文件或链接文件等等。

当为[ d ]则是目录
当为[ - ]则是文件；
若是[ l ]则表示为链接文档(link file)；
若是[ b ]则表示为装置文件里面的可供储存的接口设备(可随机存取装置)；
若是[ c ]则表示为装置文件里面的串行端口设备，例如键盘、鼠标(一次性读取装置)。
接下来的字符中，以三个为一组，且均为『rwx』 的三个参数的组合。其中，[ r ]代表可读(read)、[ w ]代表可写(write)、[ x ]代表可执行(execute)。 要注意的是，这三个权限的位置不会改变，如果没有权限，就会出现减号[ - ]而已。
Linux系统按文件所有者、文件所有者同组用户和其他用户来规定了不同的文件访问权限。

```

![](<https://www.runoob.com/wp-content/uploads/2014/06/363003_1227493859FdXT.png>)





`chown`更改文件属主，也可以同时更改文件属组  

- -R：递归更改文件属组，就是在更改某个目录文件的属组时，如果加上-R的参数，那么该目录下的所有文件的属组都会更改。

```
chown [–R] 属主名 文件名
chown [-R] 属主名：属组名 文件名
```

那么我们就可以使用 **u, g, o** 来代表三种身份的权限！

+(加入)    u+w
-(除去)    u-w
=(设定)   u=rwx

```
chmod [-R] xyz 文件或目录 // x，y,z 为 0-7中一个
chmod u=rwx,g=rx,o=r 文件名
```





`ps -ef | grep .. ` 查找指定程序信息( .. )

```
ps aux # 查看系统所有的进程数据  
ps ax # 查看不与terminal有关的所有进程  
ps -lA # 查看系统所有的进程数据  
ps axjf # 查看连同一部分进程树状态  
```



`killall [-iIe] [command name]    杀死进程,靠名字`，`kill 靠 进程id`



 `pwd` 显示工作路径

`mv dir1 new_dir` 移动，重命名文件

```
rm -rf 
-f, --force    忽略不存在的文件，从不给出提示。
-r, -R, --recursive   指示rm将参数中列出的全部目录和子目录均递归地删除。
```

`find . -name "*.c" `  将目前目录及其子目录下所有延伸档名是 c 的文件列出来。

`find path -name "*.c"`

```
grep  [选项]  ”模式“  [文件]
grep家族总共有三个：grep，egrep，fgrep。

常用选项：
　　-E ：开启扩展（Extend）的正则表达式。

　　-i ：忽略大小写（ignore case）。

　　-v ：反过来（invert），只打印没有匹配的，而匹配的反而不打印。

　　-n ：显示行号

　　-w ：被匹配的文本只能是单词，而不能是单词中的某一部分，如文本中有liker，而我搜寻的只是like，就可以使用-w选项来避免匹配liker

　　-c ：显示总共有多少行被匹配到了，而不是显示被匹配到的内容，注意如果同时使用-cv选项是显示有多少行没有被匹配到。

　　-o ：只显示被模式匹配到的字符串。

　　--color :将匹配到的内容以颜色高亮显示。

　　-A  n：显示匹配到的字符串所在的行及其后n行，after

　　-B  n：显示匹配到的字符串所在的行及其前n行，before

　　-C  n：显示匹配到的字符串所在的行及其前后各n行，context
　
　
　
　　位置锚定：

　　　　　　^ ：锚定行首

　　　　　　$ ：锚定行尾。技巧："^$"用于匹配空白行。

　　　　　　\b或\<：锚定单词的词首。如"\blike"不会匹配alike，但是会匹配liker

　　　　　　\b或\>：锚定单词的词尾。如"\blike\b"不会匹配alike和liker，只会匹配like

　　　　　　\B ：与\b作用相反。
```

tar 

```

压缩：tar -jcv -f filename.tar.bz2 要被处理的文件或目录名称  
查询：tar -jtv -f filename.tar.bz2  
解压：tar -jxv -f filename.tar.bz2 -C 欲解压缩的目录  

```

cat命令

该命令用于查看文本文件的内容，后接要查看的文件名，通常可用管道与more和less一起使用，从而可以一页页地查看数据。例如：

```

cat text | less # 查看text文件中的内容  
# 注：这条命令也可以使用less text来代替  
```

gcc命令

对于一个用Linux开发C程序的人来说，这个命令就非常重要了，它用于把C语言的源程序文件，编译成可执行程序，由于g++的很多参数跟它非常相似，所以这里只介绍gcc的参数，它的常用参数如下：

```

-o ：output之意，用于指定生成一个可执行文件的文件名  
-c ：用于把源文件生成目标文件（.o)，并阻止编译器创建一个完整的程序  
-I ：增加编译时搜索头文件的路径  
-L ：增加编译时搜索静态连接库的路径  
-S ：把源文件生成汇编代码文件  
-lm：表示标准库的目录中名为libm.a的函数库  
-lpthread ：连接NPTL实现的线程库  
-std= ：用于指定把使用的C语言的版本  
  
# 例如：  
# 把源文件test.c按照c99标准编译成可执行程序test  
gcc -o test test.c -lm -std=c99  
#把源文件test.c转换为相应的汇编程序源文件test.s  
gcc -S test.c  
```

time命令

该命令用于测算一个命令（即程序）的执行时间。它的使用非常简单，就像平时输入命令一样，不过在命令的前面加入一个time即可，例如：

```
time ./process  
time ps aux  
```

apt

```
apt list [package]
从本地仓库中查找指定的包名，支持通配符，比如"apt list zlib*"就能列出以zlib开头的所有包

apt search [key]
与list类似，通过给出的关键字进行搜索，列出所有的包和其描述

apt show [package]
列出指定包的详细情况，包名要填写完整。

apt install [package]
安装指定的包，并同时安装其依赖的其他包。
```

| apt 命令         | 取代的命令           | 命令的功能                     |
| ---------------- | -------------------- | ------------------------------ |
| apt install      | apt-get install      | 安装软件包                     |
| apt remove       | apt-get remove       | 移除软件包                     |
| apt purge        | apt-get purge        | 移除软件包及配置文件           |
| apt update       | apt-get update       | 刷新存储库索引                 |
| apt upgrade      | apt-get upgrade      | 升级所有可升级的软件包         |
| apt autoremove   | apt-get autoremove   | 自动删除不需要的包             |
| apt full-upgrade | apt-get dist-upgrade | 在升级软件包时自动处理依赖关系 |
| apt search       | apt-cache search     | 搜索应用程序                   |
| apt show         | apt-cache show       | 显示安装细节                   |