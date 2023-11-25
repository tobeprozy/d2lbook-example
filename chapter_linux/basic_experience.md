# linux精讲

## 安装软件包

### 安装C和C++的编译器

```
yum -y install gcc*
```

### 升级编译器

升级软件包：

```
yum -y install centos-release-scl devtoolset-8-gcc*
```

启用软件包：

```
echo "source /opt/rh/devtoolset-8/enable" >>/etc/profile
# 每次启动shell的时候，会执行/etc/profile脚本。
```

或

```
mv /usr/bin/gcc /usr/bin/gcc-4.8.5
ln -s /opt/rh/devtoolset-8/root/bin/gcc /usr/bin/gcc
mv /usr/bin/g++ /usr/bin/g++-4.8.5
ln -s /opt/rh/devtoolset-8/root/bin/g++ /usr/bin/g++
```

### 安装库函数的帮助文档

yum -y install man-pages

帮助文档的使用

man 级别 命令或函数

显示帮助的界面可以用vi的命令，q退出。

**man的级别：**

**1-****用户命令**；2-系统接口；**3-库函数**；4-特殊文件，比如设备文件；5-文件；

6-游戏；7-系统的软件包；8-系统管理命令；9-内核。

## 编译

gcc/g++ 选项 源代码文件1 源代码文件2 源代码文件n

常用选项：

```
-o		指定输出的文件名，这个名称不能和源文件同名。如果不给出这个选项，则生成可执行文件a.out。
-g		如果想对源代码进行调试，必须加入这个选项。
-On	在编译、链接过程中进行优化处理，生成的可执行程序效率将更高。
-c		只编译，不链接成为可执行文件，通常用于把源文件编译成静态库或动态库。
-std=c++11 支持C++11标准。
优化选项：
-O0： 不做任何优化，这是默认的编译选项。 
-O或-O1： 对程序做部分编译优化，对于大函数，优化编译占用稍微多的时间和相当大的内存。使用本项优化，编译器会尝试减小生成代码的尺寸，以及缩短执行时间，但并不执行需要占用大量编译时间的优化。 
-O2： 这是推荐的优化等级。与O1比较而言，O2优化增加了编译时间的基础上，提高了生成代码的执行效率。
-O3： 这是最高最危险的优化等级。用这个选项会延长编译代码的时间，并且在使用gcc4.x的系统里不应全局启用。自从3.x版本以来gcc的行为已经有了极大地改变。在3.x，-O3生成的代码也只是比-O2快一点点而已，而gcc4.x中还未必更快。用-O3来编译所有的软件包将产生更大体积更耗内存的二进制文件，大大增加编译失败的机会或不可预知的程序行为（包括错误）。这样做将得不偿失，记住过犹不及。在gcc 4.x.中使用-O3是不推荐的。
```

如果使用了优化选项：1）编译的时间将更长；2）目标程序不可调试；3）有效果，但是不可能显著提升程序的性能。

## 静态库和动态库

在实际开发中，我们把通用的函数和类分文件编写，称之为库。在其它的程序中，可以使用库中的函数和类。

一般来说，通用的函数和类不提供源代码文件（安全性、商业机密），而是编译成二进制文件。

库的二进制文件有两种：静态库和动态库。

### 静态库

**制作静态库**

```
g++ -c -o lib库名.a 源代码文件清单
```

**使用静态库**

不规范的做法：

```
g++ 选项 源代码文件名清单 静态库文件名
```

规范的做法：

```
g++ 选项 源代码文件名清单 -l库名 -L库文件所在的目录名
```

**静态库的概念**

程序在编译时会把库文件的二进制代码链接到目标程序中，这种方式称为静态链接。

如果多个程序中用到了同一静态库中的函数或类，就会存在多份拷贝。
