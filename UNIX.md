# UNIX

## 系统

`passwd`：更改口令

`lock`：锁住终端

Ctrl+D、`logout`、`exit`：退出系统

`command &`：将命令command放在后台执行，用户不必等到这条命令执行结束

## 文件

文件类型：普通文件、目录文件、特别文件、命名管道

目录结构：

* 根目录root，用`/`表示
* 绝对路径名：以`/`开头；相对路径名：不以`/`开头
* `..`：向根目录方向攀登一级
* `.`：当前目录的绝对路径名(在某些必须指定绝对路径名的场合，可使用其代指工作目录)
* 目录名`.`、`..`：把文件系统连接在一起的”黏合剂“
* `~`：home目录

文件存取控制模式：

* rwxrwxrwx：文件所有者(user)、同组用户(group)、其它用户(other)
* 只有文件所有者可以改变文件的访问权限

## 通配符

`?`：匹配除'/'外的单个字符，在方括号内不是通配符

`*`：匹配任意字符串，包括空串，在方括号内不是通配符

`[abc]`：匹配a或b或c

`[a-c]`：ASCII连续字符中的任意一个，’-‘仅在方括号内作为通配符

`[0-13]`：匹配0或1或3

隐式文件第一个点必须显示匹配

只能在一个目录内匹配文件名

## cat

`cat > file`：读取用户输入至文件file中（每次都会新建，覆盖掉原来的）

`cat >> file`：不覆盖，添加到尾部

`cat < file`、`cat file`：显示文件内容

`cat < file1 > file2`、`cat file1 > file2`：复制文件

`cat file1 file2 | sort`：把file1、file2的数据连接起来，输出送至管道一端，sort命令从管道另一端读入并排序

`-v`：使控制字符也显示出来

## ls

`ls [-选项] [文件名表]`

`-l`：长列表，文件类型、文件权限、链接数、文件所有者、组名、文件大小、修改日期等

* 第一列：
  * -：普通文件
  * d：目录
  * b：块特别文件
  * c：字符特别文件
  * p：命名管道
  * l：符号链接文件

`-t`：按文件的修改时间顺序列出所有文件

`-r`：按文件或文件名的逆序排列

`-a`：将以“.”开始的隐文件名显示出来

`-F`：若文件为目录，则其名后放一"/"；若文件为可执行文件，则其名后放一"*"；若符号链接，则其名后放一"@"

`-b`：用八进制数\ddd表示形式显示不可打印的字符

`-i`：在第一域列出I节字号

选项可组合，如`-al`

## mkdir

`mkdir [-m 权限模式] 目录名`：默认777

建立目录项要对父目录有写权限

## rmdir

`rmdir [-p] 目录名`：只有当一个目录为空，才能删除

`-p`：如果删除指定的目录后父目录为空，那它也被删除

## cp

`cp 文件名1 文件名2`：用文件1复制文件2，若文件2已存在，则原始内容丢失，可带路径

`cp 文件... 目录`：将一个或多个文件复制到另一个目录，文件和目录都要已存在

`cp -r 目录1 目录2`：将目录1及其所有内容复制到目录2下

`-i`：在覆盖一个已存在的文件时事先获得确认

`-p`：复制文件时保留源文件的修改时间和权限方式

## mv

与`cp`前两种类似，区别是源文件不复存在

`mv 目录名1 目录名2`：目录改名

## rm

`rm [-fi] 文件...`：删除文件

`rm -r [-fi] 目录...`：删除目录

`-f`：强制，即使文件写保护，也不要求用户确认

`-i`：对话方式，删除任何一个文件都要求用户确认

## ln

`ln 文件名 新文件名`：对一个文件建立链接，使用其它文件名与一个文件实体建立链接

`ln 文件... 目录`：在另一个目录为一个或多个文件建立同名链接

以上为硬链接，系统建立的是不同文件名与同一个文件实体的链接

以下为软链接，建立的是新的文件或目录与原来文件或目录的路径名映射，速度稍慢

`ln -s ......`

## diff

`diff [-bie] 文件1 文件2`：以编辑指令的形式逐行显示两个文件的差异

```
n1 a n2,n3
> 显示文件2中n2~n3的那些行

n1,n2 d n3
< 显示文件1中n1~n2的那些行

n1,n2 c n3,n4
< 显示文件1中n1~n2的那些行
---
> 显示文件2中n3~n4的那些行
```

`-b`：忽略由于空格及制表符而引起的差异

`-i`：忽略字母的大小写差异

`-e`：产生一个编辑手稿，UNIX的编辑程序可用它来由文件1建立文件2

## file

`file 文件...`：判断一个文件是否为正文，还是二进制文件

## find

`find 目录 [条件] [操作]`：常用目录为“.”，在目录树中自上而下递归查找满足条件的文件

条件：

* `-atime [+|-]n`：指定文件的存取时间
* `-mtime [+|-]n`：指定文件的修改时间
* `-name 文件名`：查找的文件名，若文件名含通配符，必须予以转义
* `-type 字符`：指定由字符表示的文件类型
  * `f`：普通文件
  * `d`：目录
  * `c`：字符设备文件
  * `b`：块设备文件
  * `p`：管道文件

操作：

* `-print`：打印找到文件的带有路径的文件名
* `-exec`：对找到文件要执行的shell命令，"{}"为找到文件的占位符，末尾为转义的分号
* `-ok`：类似`-exec`，但在执行命令前，打印命令和参数，等待用户确认

`-a`：多个条件(操作)逻辑与，默认

`-o`：多个条件(操作)逻辑或

```
Example

打印当前目录子树中所有以.c.old结尾的文件
find . -name "*.c.old" -print
find . -name \*.c.old -print

打印当前目录子树中7天前修改过的C源程序名
find . -name \*.c -mtime +7 -print

打印/usr目录子树中所有以.sav结尾的文件和core文件
find /usr \(-name \*.sav -o -name core \) -print

打印当前目录子树下的全部文件
find . -print

-print可以通过执行echo命令实现
find . -exec echo {} \;

删除一星期以前的新闻项
find /usr/news -mtime +7 -exec rm {} \;
```

## chown

`chown 新属主 文件...`：将一个文件或目录的属主改变成另一个注册用户

只有文件原属主或超级用户才能改变文件的属主

`chown -r 新属主 目录`：用于递归改变目录以及该目录下的所有文件和子目录的属主

## chmod

改变文件所有者、组用户、其它用户对文件或目录的存取许可证，只有文件所有者和超级用户有权改变文件存取权

`chmod 模式 文件...|目录...`

两种模式：

* 八进制数表示：读：4；写：2；执行：1，`chmod 777 file`
* 符号表示：
  * u：文件所有者；g：同组用户；o：其它用户；a：所有用户
  * +：添加存取许可；-：取消存取许可；=：取消该文件的原有存取许可
  * r：读许可；w：写许可；x：执行许可；s：执行时置进程的有效用户标识数为文件所有者的标识数
  * `chmod ug+w file`

## umask

`umask [3位八进制数]`：新建文件的实际权限为创建时的权限值减去umask指定的八进制数值

## echo

`echo [-n] 参数表`：显示命令行中的字符串常数、Shell变量值、产生诊断信息、向管道发送数据等

`-n`：在输出一行后不换行

”*“会被扩展，若要使用需要用"\\"或单引号括起来，双引号没用

## more

`more [+起始行号]|[+/初始查找模式] [文件]`：一次一屏显示文件

more内部命令：

* 空格键：显示下一屏
* Enter键：显示下一行
* nf：向下移动n屏，n为数字
* nb：向上移动n屏，n为数字
* /模式：向下查找指定的字符串模式
* n：重复前面查找命令
* =：显示当前行号
* h：显示more所有命令的帮助信息
* q：退出more

## pg

与more类似，Enter键显示下一屏，在输入每个命令后必须按下Enter键

## head

`head [-显示行数] 文件`：显示文件的开始部分，默认10行

`tail [+起始行] 文件`、`tail [-起始行] 文件`：默认10行

从文件第51行起显示到第70行：`head -70 file | tail -20`

## lp

`lp [-mvc] [-d 打印机名] [-t 标题] 文件...`：打印文件

## lpstat

`lpstat [-p 打印机名表] [-u 用户名表]`：检查打印队列的状态

## cancel

`cancel 作业号表`

`cancel 打印机名表`

`cancel -u 用户标识符`

## pr

`pr [-h 标题] [-l 每页行数] [文件...]`：从标准输入或文件中读取数据，并产生带有日期、标题和页号的分页输出

```
Example

对文件进行格式化后通过管道输出到lp程序以便进行打印
pr file | lp

若pr的输入来自管道，则没有文件名，最好使用-h选项指定打印标题
cat file1 file2 | pr -h 'file1 and file2' | lp
```

## od

`od [格式] [文件] [位移量]`：以各种格式显示二进制文件的内容

格式：

* `-b`：二进制数
* `-o`：八进制数，默认
* `-d`：十进制数
* `-x`：十六进制数
* `-c`：ASCII

位移量：控制从文件中的哪个位置开始显示
































