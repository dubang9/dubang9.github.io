---
layout: post
title:  笔记
date:  2019-04-11
categories: 学习
tags: Python
author: DuPont	
---

* content
{:toc}

# python中os.system、os.popen、subprocess.popen的区别



最近项目中需要在python中执行shell脚本，以下解释使用os.system、 
os.popen和subprocess.popen的区别：

1.os.system
该函数返回命令执行结果的返回值，system()函数在执行过程中进行了以下三步操作： 
1.fork一个子进程； 
2.在子进程中调用exec函数去执行命令； 
3.在父进程中调用wait（阻塞）去等待子进程结束。 
对于fork失败，system()函数返回-1。 
由于使用该函数经常会莫名其妙地出现错误，但是直接执行命令并没有问题，所以一般建议不要使用。

2.os.popen
popen() 创建一个管道，通过fork一个子进程,然后该子进程执行命令。返回值在标准IO流中，该管道用于父子进程间通信。父进程要么从管道读信息，要么向管道写信息，至于是读还是写取决于父进程调用popen时传递的参数（w或r）。通过popen函数读取命令执行过程中的输出示例如下：

``` 
!/usr/bin/python
import os

p=os.popen('ssh 10.3.16.121 ls')
x=p.read()
print x

p.close()
```



3.subprocess模块
1）概述
  subprocess模块是在2.4版本中新增的，官方文档中描述为可以用来替换以下函数：

    os.system、
    os.spawn、
    os.popen、
    popen2
2）参数
官方对于subprocess模块的参数解释如下：

> args is required for all calls and should be a string, or a sequence of program arguments. Providing a sequence of arguments is generally preferred, as it allows the module to take care of any required escaping and quoting of arguments (e.g. to permit spaces in file names). If passing a single string, either shell must be True (see below) or else the string must simply name the program to be executed without specifying any arguments.

![img](https://img-blog.csdn.net/20171009103025746?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYmNmZHNhZ2JmY2lzYmc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

参数既可以是string，也可以是list。 
subprocess.Popen([“cat”,”test.txt”]) 
subprocess.Popen(“cat test.txt”, shell=True) 
对于参数是字符串，需要指定shell=True



#### **3）使用示例**

- **其中subprocess.call用于代替os.system**，示例：

```
import subprocess
returnCode = subprocess.call('adb devices')
print returnCode
```

- **subprocess.check_output**

- **subprocess.Popen的使用**

  1.执行结果保存在文件

```
cmd = "adb shell ls /sdcard/ | findstr aa.png"  
fhandle = open(r"e:\aa.txt", "w")  
pipe = subprocess.Popen(cmd, shell=True, stdout=fhandle).stdout  
fhandle.close()  
```



2.执行结果使用管道输出

```
pipe=subprocess.Popen(cmd,shell=True,stdout=subprocess.PIPE).stdout  
print pipe.read() 
```

4.commands.getstatusoutput()
      使用commands.getstatusoutput() 方法就可以获得到返回值和输出：

```
(status, output) = commands.getstatusoutput('sh hello.sh')
print status, output
```





