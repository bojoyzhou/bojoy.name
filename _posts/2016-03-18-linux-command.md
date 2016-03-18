---
layout: post
title: linux 常用命令
category: tech
tags: [linux, shell, command, cmd]
---

## cd [dir]

用来进入某个目录.

## vi [filename]

用来编辑文件.

## ps -aux

查看所有进程, 配合 `| grep processname` 来查看某个进程.

## top

查看进程资源占用情况, 跟windows的资源管理器类似.

## df

查看磁盘挂载情况.

## fdisk -l

查看磁盘信息, 包括未挂载的.

## scp [-r] sourcefile destfile

用来远程传输文件, 如果是目录则使用 `-r` 选项, 表示整个目录都传输. 如果文件是本地文件直接写路径即可, 如果是远程文件则格式为 `username@ip:filename` filename最好使用绝对路径(即 `/` 开头).

## ssh-keygen -rsa

生成一个ssh密钥

## ln -s sourcefile destfile

在destfile位置建立一个软链, 相当于windows的快捷方式的概念, 但不完全相同.

## cat filename

查看文件内容.

## tail [-f] filename

查看filename的最后几行, `-f` 选项常用来打开某日志文件, 当文件有新的内容的时候, 文件内容会被打印在控制台.

## echo "somestring" [{>>|>} filename]

用来把内容输出到某个输出流(默认是标准输出流, 即控制台), 可以使用流控制字符 `>>`(使用append的方式将新的内容添加到文件末尾) 或者 `>`(使用replace的方式覆盖文件) 来输出到其他文件

## ls | xargs -n1 echo

ls是用来查看当前目录下的文件的命令, xargs是一个把前一个命令的输出作为后一个命令的参数的方法. 这里用到了 `|` 操作符, 用来开启一个管道, 把前面命令的输入传送给后面的命令. 而xargs 可以使用 `-n1` 选项来把输入分行传给后面的命令. 

## chmod [-R] 0777 filename

修改filename的权限, `-R` 表示后面的filename是目录, 并且递归修改filename下的所有的文件和文件夹的权限, 如果需要区分文件和文件夹来设置权限, 最好结合 `find` 命令来实现, 下面有示例.

## chown [-R] user:group filename

跟chmod类似的使用方法, 功能是改变文件的所属用户和所属组.

## find dir -name findstr

在dir下面查找名称包含findstr的文件.

## find dir -type {d|f}

在dir下面查找所有目录(d), 或者文件(f).

## find . -type f | xargs -n1 chmod 0644

把当前目录所有的文件权限都修改为 `0644`, 文件一般不需要可执行权限.

## find . -type d | xargs -n1 chmod 0755

把当前目录所有的文件权限都修改为 `0755`, 目录需要可执行权限, 否则将失去文件下内容的可读权限.

## du -sh dir

查看目录有多大

## find -maxdepth 1 -type d | xargs -n1 du -sh

查看当前目录下所有子目录, 每个有多大, 这经常在磁盘空间不足时, 用来查找大文件时使用.

## ssh user@ip 'ls'

在远程机器上面执行 `ls` 命令, 当你有多台服务器需要管理时, 可能需要此用法, 这可能需要先打通机器间信任关系才会更好用些(因为不打通信任关系, 需要每次都输入密码)

## sed

sed命令用来执行一些字符串操作, 比较常用的是做字符串替换, 例如 `echo helloWord | sed 's/\(Word\)/ Bojoy \1/'` 分组用的括号需要转义的, 还有一些其他的字符也需要转义, 一般不用sed做过于复杂的匹配. 


## kill -9 pid

强制终结某个进程.