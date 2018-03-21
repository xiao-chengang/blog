---
title: Mac终端使用技巧 切换到其他路径和目录
date: 2018-02-18 15:09:47
tags: 
    - mac 
    - terminal 
    - 快捷键
categories: terminal
---
**如果你想将当前 command line 会话切换到其他目录，需要用到三个命令：pwd，ls和cd。**
**pwd的含义是“print working directory”，会显示当前目录的绝对路径。**
**ls的含义是“list directory contents”，它会列出当前目录的内容。这个命令还有其他参数可选。**
**cd的含义是“change directory”，它会改变当前目录到你指定的目录。如果你不指定，则会返回你的 home folder。**
<!----more---->
## 常用快捷键
pwd　　　　　　当前工作目录

cd（不加参数）　　进root

cd（folder）　　进入文件夹

cd ..　　　　　　上级目录

cd ~　　　　　　返回root

cd -　　　　　　返回上一个访问的目录

rm 文件名 　　　　删除

cat 文件名(|less)　　在终端下查看文件

ls　　　　　　　　列出目录下所有文件

cp 文件名 目标目录　　将文件拷贝到目标目录下

~代表root　　如：~/Document/CPP2/

mkdiv　　　　　　新建文件夹

g++ 源文件名　　　　编译源文件，产生a.out

./文件名　　　　　　运行  例如：./a.out < 输入文件名 > 输出文件名

control+d　　　　　中断a.out运行

nano 　　　　　　编写脚本语言　　ctrl+o存储

nano ....sh　　　　打开

bash ....sh　　　　运行脚本

echo "...$i..."　　　输出语句

tar -zxf abc.tar.gz     tar文件解压

ssh root@192.168.1.222   以root账号远程连接222服务器
unrar x abc.rar     rar文件解压，需要安装rar工具