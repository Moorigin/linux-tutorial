# 查看 Linux 命令帮助信息

> 关键词：`help`, `whatis`, `info`, `which`, `whereis`, `man`


## 1. 查看 Linux 命令帮助信息的要点

- 查看 Shell 内部命令的帮助信息 - 使用 [help](#help)
- 查看命令的简要说明 - 使用 [whatis](#whatis)
- 查看命令的详细说明 - 使用 [info](#info)
- 查看命令的位置 - 使用 [which](#which)
- 定位指令的二进制程序、源代码文件和 man 手册页等相关文件的路径 - 使用 [whereis](#whereis)
- 查看命令的帮助手册（包含说明、用法等信息） - 使用 [man](#man)
- 只记得部分命令关键字 - 使用 man -k

> 注：推荐一些 Linux 命令中文手册：
>
> - [Linux 命令大全](http://man.linuxde.net/)
> - [linux-command](https://github.com/jaywcjlove/linux-command)

## 2. 命令常见用法

### 2.1. help

> help 命令用于查看 Shell 内部命令的帮助信息。而对于外部命令的帮助信息（比如ls、grep等）只能使用 man 命令（手册页）或者 --help 命令查看。例如：

```
man ls
```
或者
```
ls --help
```
这将分别显示ls命令的手册页和内置帮助信息。

### 2.2. whatis

> whatis 命令在 Linux 系统中用于显示一个简短的命令描述。它查询一个特定命令、系统调用、库函数或文件的手册页的简短描述，并将其展示给用户。这个命令对于快速了解一个程序或命令的基本功能非常有用。whatis 命令的信息来源是系统的手册页数据库，这个数据库通常由 mandb 程序创建和维护。如果数据库未被创建或更新，whatis 命令可能无法找到某些命令的信息。

使用 whatis 的基本语法如下：

```
whatis command_name
```

示例：

```
# 查看 man 命令的简要说明
whatis man

# 查看以 loca 开拓的命令的简要说明
whatis -w "loca*"
```

如果你刚刚安装了一个新程序或者手册页有更新，你可能需要更新手册页数据库。在大多数系统上，你可以使用以下命令来更新数据库：

```
sudo mandb
```

### 2.3. info

> 在 Linux 和 Unix 系统中，info 命令是用来阅读“信息页”的，它提供了比传统的 man（手册）页更详细和更容易浏览的文档。信息页通常包含比手册页更多的细节，并且支持超链接，类似于网页，使得用户可以轻松地在不同的信息节点（sections）之间跳转。
>
> info 页面是以 Texinfo 格式书写的，这是一个由 GNU 项目开发的文档系统，旨在提供结构化、有组织的文档。info 命令和 Texinfo 页面通常用于 GNU 软件包的文档，因为它们是由同一个组织开发的。

使用 info 命令的基本语法如下：

```
info [option] [name]
```

如果不带参数运行 info 命令，它通常会显示一个包含可用信息节点的菜单。如果你指定了一个名称，info 将会尝试显示与该名称相关的信息页。

例如，要查看 ls 命令的信息页，你可以输入：

```
info ls
```

在 info 页面内，你可以使用键盘导航：

Enter 或 Return：进入一个链接（类似于点击超链接）。
- u：向上移动一个层级。
- n：移动到下一个节点。
- p：移动到上一个节点。
- q：退出 info 阅读器。
info 页面还支持复杂的搜索和导航功能，可以在 info 阅读器内部查看更多命令和使用说明。

### 2.4. which

> which 命令用于查找并显示给定命令的绝对路径。which 命令会搜索你的 PATH 环境变量中列出的目录，找到符合条件的可执行文件并打印出它的完整路径。也就是说，使用 which 命令，就可以看到某个系统命令是否存在，以及执行的到底是哪一个位置的命令。
>
> 这对于确定你将要运行的命令的版本非常有用，尤其是当你安装了多个版本的同一个程序，或者你想确认一个命令是否在 PATH 中可用。

使用 which 的基本语法如下：

```
which command_name
```

示例：

查找 python 命令的位置，你可以输入：

```
which python
```

这将返回 python 可执行文件的完整路径，比如 /usr/bin/python。

说明：which 是根据使用者所配置的 PATH 变量内的目录去搜寻可运行档的！所以，不同的 PATH 配置内容所找到的命令当然不一样的！

```
[root@localhost ~]# which cd
cd: shell built-in command
```

cd 这个常用的命令竟然找不到啊！为什么呢？这是因为 cd 是 bash 内建的命令！它不适用于查找内建 shell 命令或别名。 which 默认是找 PATH 内所规范的目录，所以是一定找不到的！

对于内建命令，你可以使用 type 命令来查找，例如：

```
type command_name
```

而对于别名，你可以使用 alias 命令来查看当前定义的别名：

```
alias alias_name
```

如果你在使用 which 命令时没有找到期望的命令，可能是因为该命令没有安装，或者它的安装路径没有添加到 PATH 环境变量中。

### 2.5. whereis

> whereis 命令用来定位指令的二进制程序、源代码文件和 man 手册页等相关文件的路径。
>
> whereis 命令只能用于程序名的搜索，而且只搜索二进制文件（参数-b）、man 说明文件（参数-m）和源代码文件（参数-s）。如果省略参数，则返回所有信息。

使用 whereis 的基本语法如下：

```
whereis [options] program_name
```

示例：

查找 gcc 编译器的相关文件，你可以输入：

```
whereis gcc
```

这可能会返回类似以下内容的输出：

```
gcc: /usr/bin/gcc /usr/lib/gcc /usr/share/man/man1/gcc.1.gz
```

这里，/usr/bin/gcc 是 gcc 程序的二进制文件路径，/usr/lib/gcc 是可能包含库文件的路径，而 /usr/share/man/man1/gcc.1.gz 是 gcc 的手册页文件。

whereis 命令的常用选项包括：
- -b：只定位二进制文件。
- -m：只定位手册页。
- -s：只定位源代码文件。
- -u：查找那些不符合上述任何一个标准的文件。
例如，如果你只对 vim 编辑器的手册页感兴趣，你可以使用以下命令：

```
whereis -m vim
```

这将返回 vim 手册页的位置。

whereis 命令是一个快速定位程序相关文件的有用工具，特别是当你需要知道一个程序的不同组成部分存放在系统的哪些位置时。

### 2.6. man

> man 命令是 Linux 下的帮助指令，通过 man 指令可以查看 Linux 中的指令帮助、配置文件帮助和编程帮助等信息。

使用 man 的基本语法如下：

```
man [section] command_name
```

这里的 [section] 是可选的，它指定了手册页的章节。手册页被分为若干个标准的章节，每个章节都包含特定类型的信息，例如：
- 1：用户命令
- 2：系统调用(内核提供的函数)
- 3：C库函数(程序库中的函数)
- 4：特殊文件（通常位于 /dev ）
- 5：文件格式和约定，例如 /etc/passwd
- 6：游戏等
- 7：杂项(包括宏包和规范，如 man(7)，groff(7))
- 8：系统管理命令和守护进程
- 9. 内核例程 [非标准]

例如，要查看 ls 命令的手册页，你可以输入：

```
man ls
```

如果你想查看关于 printf 的 C 库函数的信息（它在第3章节），你可以指定章节号：

```
man 3 printf
```

当你在 man 命令中指定章节号时，它会直接查找那个章节中的手册页。如果不指定章节号，man 会按照默认的章节顺序搜索。

手册页通常包含以下几个部分：

- NAME：命令或函数的名称和简短描述。
- SYNOPSIS：命令或函数的使用语法。
- DESCRIPTION：命令或函数的详细描述。
- OPTIONS：命令支持的选项或参数。
- FILES：与命令或函数相关的文件。
- SEE ALSO：相关命令或文档的引用。
- BUGS：已知的问题和错误。
- EXAMPLES：使用示例。
- AUTHORS：作者信息。

在查看手册页时，你可以使用 page up 和 page down 来上下翻页，按 / 键后输入搜索词来搜索文本，按 n 来查看下一个匹配项，按 q 键退出手册页。

## 3. 参考资料

https://linuxtools-rst.readthedocs.io/zh_CN/latest/base/01_use_man.html
