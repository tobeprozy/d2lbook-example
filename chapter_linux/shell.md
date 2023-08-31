# shell 基础

## 基础语法

### 编写规范

```
#!/bin/bash              [指定告知系统当前这个脚本要使用的shell解释器]
Shell相关指令
```

后最一般为.sh，通过./文件名.sh执行，如果需要调整权限，chmod +x 文件名.sh

### 变量定义和使用

**定义变量时，变量名不加美元符号（$），使用变量的时候才加美元符（$）**，如：

```bash
your_name="coonote.com"
```

注意，**变量名和等号之间不能有空格**，这可能和你熟悉的所有编程语言都不一样。同时，变量名的命名须遵循如下规则：

- 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
- 中间不能有空格，可以使用下划线 _。
- 不能使用标点符号。
- 不能使用bash里的关键字（可用help命令查看保留关键字）。

除了显式地直接赋值，还可以用语句给变量赋值，如：

```
for file in `ls /etc`
或
for file in $(ls /etc)
```

**使用一个定义过的变量，只要在变量名前面加美元符号即可，如：**

```
your_name="qinjx"
echo $your_name
echo ${your_name}
```

变量名外面的花括号是可选的，加不加都行，加花括号是为了帮助解释器识别变量的边界，比如下面这种情况：

```
for skill in Ada Coffe Action Java; do
    echo "I am good at ${skill}Script"
done
```

### 变量类型

运行shell时，会同时存在三种变量：

- **1) 局部变量** 局部变量在脚本或命令中定义，仅在当前shell实例中有效，其他shell启动的程序不能访问局部变量。
- **2) 环境变量** 所有的程序，包括shell启动的程序，都能访问环境变量，有些程序需要环境变量来保证其正常运行。必要的时候shell脚本也可以定义环境变量。
- **3) shell变量** shell变量是由shell程序设置的特殊变量。shell变量中有一部分是环境变量，有一部分是局部变量，这些变量保证了shell的正常运行

#### Shell 字符串

- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；

```shell
str='this is a string'
```

- 双引号里可以有变量，双引号里可以出现转义字符

```shell
your_name="coonote"
str="Hello, I know you are \"$your_name\"! \n"
echo -e $str
```

- 可以进行字符串拼接

```shell
your_name="coonote"
# 使用双引号拼接
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting  $greeting_1
# 使用单引号拼接
greeting_2='hello, '$your_name' !'
greeting_3='hello, ${your_name} !'
echo $greeting_2  $greeting_3
# 输出结果为：
hello, coonote ! hello, coonote !
hello, coonote ! hello, ${your_name} !
```

- 获取字符串长度

```shell
string="abcd"
echo ${#string} #输出 4
```

- 提取子字符串，**注意**：第一个字符的索引值为 **0**。

```shell
string="coonote is a great site"
echo ${string:1:4} # 输出 oono
```

- 查找子字符串，查找字符 **i** 或 **o** 的位置(哪个字母先出现就计算哪个)：

```shell
string="coonote is a great site"
echo `expr index "$string" io`  # 输出 4，脚本中 ` 是反引号，而不是单引号 '
```

#### Shell 数组

bash支持一维数组（不支持多维数组），并且没有限定数组的大小。

```bash
array_name=(value0 value1 value2 value3)
array_name=(
value0
value1
value2
value3
)
# 还可以单独定义数组的各个分量：
array_name[0]=value0
array_name[1]=value1
array_name[n]=valuen
# 可以不使用连续的下标，而且下标的范围没有限制。
```

读取数组元素值的一般格式是：

```bash
valuen=${array_name[n]}
# 使用 @ 符号可以获取数组中的所有元素
echo ${array_name[@]}
```

- 获取数组长度

```bash
# 取得数组元素的个数
length=${#array_name[@]}
# 或者
length=${#array_name[*]}
# 取得数组单个元素的长度
lengthn=${#array_name[n]}
```

### 参数传递

在执行 [shell](https://www.coonote.com/shell/shell-tutorial.html) 脚本时，向脚本传递参数，脚本内获取参数的格式为：**$n**。**n** 代表一个数字，0 为执行的文件名（包含文件路径），1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推……

```shell
#!/bin/bash

echo "Shell 传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";
```

为脚本设置可执行权限，并执行脚本，输出结果如下所示：

```bash
$ chmod +x test.sh 
$ ./test.sh 1 2 3
Shell 传递参数实例！
执行的文件名：./test.sh
第一个参数为：1
第二个参数为：2
第三个参数为：3
```

#### 特殊字符

```bash
参数处理	说明
$#	传递到脚本的参数个数
$*	以一个单字符串显示所有向脚本传递的参数。
如"$*"用「"」括起来的情况、以"$1 $2 … $n"的形式输出所有参数。
$$	脚本运行的当前进程ID号
$!	后台运行的最后一个进程的ID号
$@	与$*相同，但是使用时加引号，并在引号中返回每个参数。
如"$@"用「"」括起来的情况、以"$1" "$2" … "$n" 的形式输出所有参数。
$-	显示Shell使用的当前选项，与set命令功能相同。
$?	显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误。
```

$* 与 $@ 区别：

- 相同点：都是引用所有参数。
- 不同点：只有在双引号中体现出来。假设在脚本运行时写了三个参数 1、2、3，，则 " * " 等价于 "1 2 3"（传递了一个参数），而 "@" 等价于 "1" "2" "3"（传递了三个参数）。

```shell
#!/bin/bash

echo "-- \$* 演示 ---"
for i in "$*"; do
    echo $i
done

echo "-- \$@ 演示 ---"
for i in "$@"; do
    echo $i
done
```

执行脚本，输出结果如下所示：

```bash
$ chmod +x test.sh 
$ ./test.sh 1 2 3
-- $* 演示 ---
1 2 3
-- $@ 演示 ---
1
2
3
```

### 运算

[shell](https://www.coonote.com/shell/shell-tutorial.html) 和其他编程语言一样，支持多种运算符，包括：

- 算数运算符
- 关系运算符
- 布尔运算符
- 字符串运算符
- 文件测试运算符

原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 [awk](https://www.coonote.com/shell/shell-awk-usage.html) 和 expr，expr 最常用。

expr 是一款表达式计算工具，使用它能完成表达式的求值操作。

#### 算数运算符

**注意：条件表达式要放在方括号之间，并且要有空格，例如: **[$a==$b]** 是错误的，必须写成 **[ $a == $b ]**。

- 乘号(*)前边必须加反斜杠(\)才能实现乘法运算；
- 

```shell
#!/bin/bash

a=10
b=20

val=`expr $a + $b`
echo "a + b : $val"

val=`expr $a - $b`
echo "a - b : $val"

val=`expr $a \* $b`
echo "a * b : $val"

val=`expr $b / $a`
echo "b / a : $val"

val=`expr $b % $a`
echo "b % a : $val"

if [ $a == $b ]
then
   echo "a 等于 b"
fi
if [ $a != $b ]
then
   echo "a 不等于 b"
fi
```

执行脚本，输出结果如下所示：

```shell
a + b : 30
a - b : -10
a * b : 200
b / a : 2
b % a : 0
a 不等于 b
```

#### 关系运算

```shell
#!/bin/bash

a=10
b=20

if [ $a -eq $b ]
then
   echo "$a -eq $b : a 等于 b"
else
   echo "$a -eq $b: a 不等于 b"
fi
if [ $a -ne $b ]
then
   echo "$a -ne $b: a 不等于 b"
else
   echo "$a -ne $b : a 等于 b"
fi
if [ $a -gt $b ]
then
   echo "$a -gt $b: a 大于 b"
else
   echo "$a -gt $b: a 不大于 b"
fi
if [ $a -lt $b ]
then
   echo "$a -lt $b: a 小于 b"
else
   echo "$a -lt $b: a 不小于 b"
fi
if [ $a -ge $b ]
then
   echo "$a -ge $b: a 大于或等于 b"
else
   echo "$a -ge $b: a 小于 b"
fi
if [ $a -le $b ]
then
   echo "$a -le $b: a 小于或等于 b"
else
   echo "$a -le $b: a 大于 b"
fi
```

执行脚本，输出结果如下所示：

```shell
10 -eq 20: a 不等于 b
10 -ne 20: a 不等于 b
10 -gt 20: a 不大于 b
10 -lt 20: a 小于 b
10 -ge 20: a 小于 b
10 -le 20: a 小于或等于 b
```

#### 布尔运算

```shell
#!/bin/bash

a=10
b=20

if [ $a != $b ]
then
   echo "$a != $b : a 不等于 b"
else
   echo "$a == $b: a 等于 b"
fi
if [ $a -lt 100 -a $b -gt 15 ]
then
   echo "$a 小于 100 且 $b 大于 15 : 返回 true"
else
   echo "$a 小于 100 且 $b 大于 15 : 返回 false"
fi
if [ $a -lt 100 -o $b -gt 100 ]
then
   echo "$a 小于 100 或 $b 大于 100 : 返回 true"
else
   echo "$a 小于 100 或 $b 大于 100 : 返回 false"
fi
if [ $a -lt 5 -o $b -gt 100 ]
then
   echo "$a 小于 5 或 $b 大于 100 : 返回 true"
else
   echo "$a 小于 5 或 $b 大于 100 : 返回 false"
fi
```

执行脚本，输出结果如下所示：

```shell
10 != 20 : a 不等于 b
10 小于 100 且 20 大于 15 : 返回 true
10 小于 100 或 20 大于 100 : 返回 true
10 小于 5 或 20 大于 100 : 返回 false
```

#### 逻辑运算符

```shell
#!/bin/bash

a=10
b=20

if [[ $a -lt 100 && $b -gt 100 ]]
then
   echo "返回 true"
else
   echo "返回 false"
fi

if [[ $a -lt 100 || $b -gt 100 ]]
then
   echo "返回 true"
else
   echo "返回 false"
fi
```

执行脚本，输出结果如下所示：

```shell
返回 false
返回 true
```

####  字符串运算符

```shell
#!/bin/bash

a="abc"
b="efg"

if [ $a = $b ]
then
   echo "$a = $b : a 等于 b"
else
   echo "$a = $b: a 不等于 b"
fi
if [ $a != $b ]
then
   echo "$a != $b : a 不等于 b"
else
   echo "$a != $b: a 等于 b"
fi
if [ -z $a ]
then
   echo "-z $a : 字符串长度为 0"
else
   echo "-z $a : 字符串长度不为 0"
fi
if [ -n "$a" ]
then
   echo "-n $a : 字符串长度不为 0"
else
   echo "-n $a : 字符串长度为 0"
fi
if [ $a ]
then
   echo "$a : 字符串不为空"
else
   echo "$a : 字符串为空"
fi
```

执行脚本，输出结果如下所示：

```shell
abc = efg: a 不等于 b
abc != efg : a 不等于 b
-z abc : 字符串长度不为 0
-n abc : 字符串长度不为 0
abc : 字符串不为空
```

#### 文件测试运算符

变量 file 表示文件 **/var/test.sh**，它的大小为 100 字节，具有 **rwx** 权限。下面的代码，将检测该文件的各种属性

```shell
#!/bin/bash

file="/var/test.sh"
if [ -r $file ]
then
   echo "文件可读"
else
   echo "文件不可读"
fi
if [ -w $file ]
then
   echo "文件可写"
else
   echo "文件不可写"
fi
if [ -x $file ]
then
   echo "文件可执行"
else
   echo "文件不可执行"
fi
if [ -f $file ]
then
   echo "文件为普通文件"
else
   echo "文件为特殊文件"
fi
if [ -d $file ]
then
   echo "文件是个目录"
else
   echo "文件不是个目录"
fi
if [ -s $file ]
then
   echo "文件不为空"
else
   echo "文件为空"
fi
if [ -e $file ]
then
   echo "文件存在"
else
   echo "文件不存在"
fi
```

### 程序流

#### if

if 语句语法格式，如果 else 分支没有语句执行，就不要写 else

```shell
if condition
then
    command1 
    command2
    ...
    commandN 
fi
```

写成一行（适用于终端命令提示符）：

```shell
if [ $(ps -ef | grep -c "ssh") -gt 1 ]; then echo "true"; fi
```

末尾的 fi 就是 if 倒过来拼写。

```shell
a=10
b=20
if [ $a == $b ]
then
   echo "a 等于 b"
elif [ $a -gt $b ]
then
   echo "a 大于 b"
elif [ $a -lt $b ]
then
   echo "a 小于 b"
else
   echo "没有符合的条件"
fi
```

if else 语句经常与 test 命令结合使用，如下所示：

```shell
num1=$[2*3]
num2=$[1+5]
if test $[num1] -eq $[num2]
then
    echo '两个数字相等!'
else
```

#### for 循环

for循环一般格式为：

```shell
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done
```

写成一行：

```shell
for var in item1 item2 ... itemN; do command1; command2… done;
```

当变量值在列表里，for 循环即执行一次所有命令，使用变量名获取列表中的当前取值。命令可为任何有效的 shell 命令和语句。in 列表可以包含替换、字符串和文件名。

in列表是可选的，如果不用它，for循环使用命令行的位置参数。

例如，顺序输出当前列表中的数字：

```shell
for loop in 1 2 3 4 5
do
    echo "The value is: $loop"
done
```

输出结果：

```shell
The value is: 1
The value is: 2
The value is: 3
The value is: 4
The value is: 5
```

顺序输出字符串中的字符：

```shell
#!/bin/bash

for str in This is a string
do
    echo $str
done
```

输出结果：

```shell
This
is
a
string
```

#### while 语句

while 循环用于不断执行一系列命令，也用于从输入文件中读取数据。其语法格式为：

```shell
while condition
do
    command
done
```

以下是一个基本的 while 循环，测试条件是：如果 int 小于等于 5，那么条件返回真。int 从 1 开始，每次循环处理时，int 加 1。运行上述脚本，返回数字 1 到 5，然后终止。

```shell
#!/bin/bash
int=1
while(( $int<=5 ))
do
    echo $int
    let "int++"
done
```

以上实例使用了 Bash let 命令，它用于执行一个或多个表达式，变量计算中不需要加上 $ 来表示变量。运行脚本，输出：

```shell
1
2
3
4
5
```

while循环可用于读取键盘信息。下面的例子中，输入信息被设置为变量FILM，按结束循环。

```shell
echo '按下 <CTRL-D> 退出'
echo -n '输入你最喜欢的网站名: '
while read FILM
do
    echo "是的！$FILM 是一个好网站"
done
```

#### 无限循环

无限循环语法格式：

```shell
while :
do
    command
done
```

或者

```shell
while true
do
    command
done
```

或者

```shell
for (( ; ; ))
```

#### until 循环

until 循环执行一系列命令直至条件为 true 时停止。

```shell
#!/bin/bash
a=0

until [ ! $a -lt 10 ]
do
   echo $a
   a=`expr $a + 1`
done
# 输出结果0
1
2
3
4
5
6
7
8
9
```

#### case ... esac

**case ... esac** 为多选择语句，与其他语言中的 switch ... case 语句类似。

```shell
echo '输入 1 到 4 之间的数字:'
echo '你输入的数字为:'
read aNum
case $aNum in
    1)  echo '你选择了 1'
    ;;
    2)  echo '你选择了 2'
    ;;
    3)  echo '你选择了 3'
    ;;
    4)  echo '你选择了 4'
    ;;
    *)  echo '你没有输入 1 到 4 之间的数字'
    ;;
esac
```

```shell
#!/bin/sh

site="runoob"

case "$site" in
   "runoob") echo "菜鸟笔记"
   ;;
   "google") echo "Google 搜索"
   ;;
   "taobao") echo "百度搜索"
   ;;
esac
```

#### break、continue、exit

```shell
#!/bin/bash
while :
do
    echo -n "输入 1 到 5 之间的数字:"
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的! 游戏结束"
            break
        ;;
    esac
done
```

执行以上代码，输出结果为：

```shell
输入 1 到 5 之间的数字:3
你输入的数字为 3!
输入 1 到 5 之间的数字:7
你输入的数字不是 1 到 5 之间的! 游戏结束
```

continue命令与break命令类似，只有一点差别，它不会跳出所有循环，仅仅跳出当前循环。

```shell
#!/bin/bash
while :
do
    echo -n "输入 1 到 5 之间的数字: "
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的!"
            continue
            echo "游戏结束"
        ;;
    esac
done
```

系统是有exit命令的，用于退出当前用户的登录状态。可是在Shell脚本中，exit语句是用来退出当前脚本的。也就是说，在Shell脚本中，只要碰到了exit语句，后续的程序就不再执行，而直接退出脚本。

```shell
[root@localhost ~]$ vi sh/exit.sh
#!/bin/bash
#演示exit的作用

read -p "Please input a number: " -t 30 num
#接收用户的输入，并把输入赋予变量num
y=$ (echo $num | sed 's/[0-9]//g')
#如果变量num 的值是数字，则把num的值替换为空，否则不替换
#把替换之后的值赋予变量y
[ -n "$y" ] && echo "Error! Please input a number!" && exit 18
#判断变量y的值如果不为空，输出报错信息，退出脚本，退出返回值为18
echo "The number is: $num"
#如果没有退出加班，则打印变量num中的数字
```

### Shell 函数

shell中函数的定义格式如下：

```shell
[ function ] funname [()]
{
    action;
    [return int;]
}
```

- 1、可以带function fun() 定义，也可以直接fun() 定义,不带任何参数。
- 2、参数返回，可以显示加：return 返回，如果不加，将以最后一条命令运行结果，作为返回值。 return后跟数值n(0-255)

```shell
#!/bin/bash
funWithReturn(){
    echo "这个函数会对输入的两个数字进行相加运算..."
    echo "输入第一个数字: "
    read aNum
    echo "输入第二个数字: "
    read anotherNum
    echo "两个数字分别为 $aNum 和 $anotherNum !"
    return $(($aNum+$anotherNum))
}
funWithReturn
echo "输入的两个数字之和为 $? !"
```

输出类似下面：

```shell
这个函数会对输入的两个数字进行相加运算...
输入第一个数字: 
1
输入第二个数字: 
2
两个数字分别为 1 和 2 !
输入的两个数字之和为 3 !
```

函数返回值在调用该函数后通过 $? 来获得。

注意：所有函数在使用前必须定义。这意味着必须将函数放在脚本开始部分，直至shell解释器首次发现它时，才可以使用。调用函数仅使用其函数名即可。



## 常用操作

### echo命令

用于字符串的输出。

```
# 显示普通字符串:
echo "It is a test"
echo It is a test # 双引号完全可以省略

# 显示转义字符
echo "\"It is a test\""  # "It is a test"
```

read 命令从标准输入中读取一行,并把输入行的每个字段的值指定给 shell 变量

```
#!/bin/sh
read name 
echo "$name It is a test"
```

以上代码保存为 test.sh，name 接收标准输入的变量，结果将是:

```
[root@www ~]# sh test.sh
OK                     #标准输入
OK It is a test        #输出
```

- 显示换行

```
echo -e "OK! \n" # -e 开启转义
echo "It is a test"
```

- 显示不换行

```
#!/bin/sh
echo -e "OK! \c" # -e 开启转义 \c 不换行
echo "It is a test"
```

输出结果：

```
OK! It is a test
```

- 显示结果定向至文件。

```shell
echo "It is a test" > myfile
```

- 原样输出字符串，不进行转义或取变量(用单引号)。

```shell
echo '$name\"' # $name\"
```

- 显示命令执行结果

```
echo `date`
```

**注意：** 这里使用的是反引号 `, 而不是单引号 '。结果：

```
Thu Jul 24 10:08:46 CST 2014
```

### printf 命令

printf 使用引用文本或空格分隔的参数，外面可以在 **printf** 中使用格式化字符串，还可以制定字符串的宽度、左右对齐方式等。默认的 printf 不会像 echo 自动添加换行符，我们可以手动添加 \n。

```shell
#!/bin/bash

printf "%-10s %-8s %-4s\n" 姓名 性别 体重kg  
printf "%-10s %-8s %-4.2f\n" 郭靖 男 66.1234
printf "%-10s %-8s %-4.2f\n" 杨过 男 48.6543
printf "%-10s %-8s %-4.2f\n" 郭芙 女 47.9876
```

执行脚本，输出结果如下所示：

```
姓名     性别   体重kg
郭靖     男      66.12
杨过     男      48.65
郭芙     女      47.99
```

%s %c %d %f 都是格式替代符，**％s** 输出一个字符串，**％d** 整型输出，**％c** 输出一个字符，**％f** 输出实数，以小数形式输出。

%-10s 指一个宽度为 10 个字符（**-** 表示左对齐，没有则表示右对齐），任何字符都会被显示在 10 个字符宽的字符内，如果不足则自动以空格填充，超过也会将内容全部显示出来。

%-4.2f 指格式化为小数，其中 **.2** 指保留2位小数。

```shell
#!/bin/bash

# format-string为双引号
printf "%d %s\n" 1 "abc"

# 单引号与双引号效果一样
printf '%d %s\n' 1 "abc"

# 没有引号也可以输出
printf %s abcdef

# 格式只指定了一个参数，但多出的参数仍然会按照该格式输出，format-string 被重用
printf %s abc def

printf "%s\n" abc def

printf "%s %s %s\n" a b c d e f g h i j

# 如果没有 arguments，那么 %s 用NULL代替，%d 用 0 代替
printf "%s and %d \n"
```

执行脚本，输出结果如下所示：

```
1 abc
1 abc
abcdefabcdefabc
def
a b c
d e f
g h i
j  
 and 0
```

### test命令

test 命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试。

```shell
num1=100
num2=100
if test $[num1] -eq $[num2]
then
    echo '两个数相等！'
else
    echo '两个数不相等！'
fi
```

### grep命令

[grep](https://www.coonote.com/shell/shell-grep.html)命令是文本搜索命令，它可以正则表达式搜索文本，也可从一个文件中的内容作为搜索关键字。
grep的工作方式是这样的，它在一个或多个文件中搜索字符串模板。如果模板包括空格，则必须被引用，模板后的所有字符串被看作文件名。搜索的结果被送到标准输出，不影响原文件内容。

```shell
grep [option] pattern file# 

# 查找/etc/passwd文件中是否存在quail用户信息
[root@www sed]# grep "quail" /etc/passwd
quail:x:1000:1000:quail:/home/quail:/bin/bash
[root@www sed]# grep -w "quail" /etc/passwd
quail:x:1000:1000:quail:/home/quail:/bin/bash
[root@www sed]# grep -i quail /etc/passwd
quail:x:1000:1000:quail:/home/quail:/bin/bash

# ifconfig看到网卡信息，只查看IP地址所在行信息
[root@www sed]# ifconfig |grep -w inet
        inet 192.168.249.132  netmask 255.255.255.0  broadcast 192.168.249.255
        inet 127.0.0.1  netmask 255.0.0.0
[root@www sed]# ifconfig |grep netmask
        inet 192.168.249.132  netmask 255.255.255.0  broadcast 192.168.249.255
        inet 127.0.0.1  netmask 255.0.0.0
[root@www sed]# ifconfig |grep -w 255
        inet 192.168.249.132  netmask 255.255.255.0  broadcast 192.168.249.255
        inet 127.0.0.1  netmask 255.0.0.0
[root@www sed]# ifconfig |grep -E "192|127"
        inet 192.168.249.132  netmask 255.255.255.0  broadcast 192.168.249.255
        inet 127.0.0.1  netmask 255.0.0.0
[root@www sed]# ifconfig |grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}"
        inet 192.168.249.132  netmask 255.255.255.0  broadcast 192.168.249.255
        inet 127.0.0.1  netmask 255.0.0.0
        
# 统计root 字符总行数
[root@www sed]# grep -c root list.txt 

# 不区分大小写查找RoOt所有行
[root@www sed]# grep -i RoOt list.txt 

# 打印www行以及行号
[root@www sed]# grep -n www list.txt 
# 不打印root行
[root@www sed]# grep -v root list.txt 
# 以168.开头的接3 5的行
[root@www sed]# grep "168.[35]" list.txt 
# 显示输出行首不是192的行
[root@www sed]# grep -E -v  "^192" list.txt
# 匹配R或r开头的行,提前echo “root 123\nRoot 123” > list.txt
[root@www sed]# grep -E "^[Rr]oot" list.txt
# 匹配r，两个任意字符，紧接t的行
[root@www sed]# grep "r..t" list.txt
# 匹配字母紧跟w 的行
[root@www sed]# grep -E "[a-Z]w " list.txt
# 打印字符w字符连续出现2次以上的行
[root@www sed]# grep "w\{2,\}" list.txt
# 打印字符o连续出现3次和5次的行
[root@www sed]# grep "o\{3,5\}" list.txt
# 匹配IPV4地址
[root@www grep]# grep -E -w --color "([0-9]{1,3}\.){3}[0-9]{1,3}" list.txt 
```

### sed命令

Sed本身是一个管道命令，可以分析 standard input 的，主要是用来分析关键字的使用、统计等，此外还可 以将数据进行替换、删除、选中、选取特定行等功能。

```shell
sed [options] ‘{command}[flags]’ [filename]    
# 中括号内容必有 大括号内容可有可无
sed  # 执行命令
[options]  # 命令选项
{command}[flags]    # sed内部选项和参数
[filename]     # 文件
```

sed结合正则使用：

|     正则      |                            说明                             |              备注               |
| :-----------: | :---------------------------------------------------------: | :-----------------------------: |
|     /key/     |                     查询包含关键字的行                      |     sed -n ‘/root/p’ 1.txt      |
| /key1/,/key2/ |                 匹配包含两个关键字之间的行                  | sed -n ‘/^adm/,/^mysql/p’ 1.txt |
|    /key/,x    | 从匹配关键字的行开始到文件第x行之间的行（包含关键字所在行） |       sed -n ‘/^ftp/,7p’        |
|    x,/key/    |         从文件的第x行开始到与关键字的匹配行之间的行         |                                 |
|     x,y!      |                        不包含x到y行                         |                                 |
|    /key/!     |                      不包括关键字的行                       |    sed -n ‘/bash$/!p’ 1.txt     |

```shell
# 想查看下student.txt的第二行，那么就可以利用“p”动作了:
[root@localhost ~]$ sed  '2p' student.txt
# 指定输出某行，使用-n选项
[root@localhost ~]$ sed -n  '2p' student.txt
#删除第二行到第四行数据
[root@localhost ~]$ sed  '2,4d' student.txt
#在第二行后加入 hello,
[root@localhost ~]$ sed '2a hello' student.txt
#在第二行前插入两行数据,如果是想追加或插入多行数据，除最后一行外，每行的末尾都要加入“\”代表数据未完结。
[root@localhost ~]$ sed '2i hello world' student.txt
#只查看sed命令操作的数据
[root@localhost ~]$ sed -n '2i hello world' student.txt
```

sed命令默认情况是不会修改文件内容的，如果我确定需要让 sed命令直接处理文件的内容，可以使用“-i”选项。不过要小心啊，这样非常容易误操作，在操作系统文件时请小心谨慎。可以使用
这样的命令:

```shell
[root@localhost ~]$ sed -i '2c No such person' student.txt
```

“c”动作是进行整行替换的，如果仅仅想替换行中的部分数据，就要使用“s”动作了。g 使得 sed 对文件中所有符合的字符串都被替换, 修改后内容会到标准输出，不会修改原文件。

```
[root@localhost ~]$ sed 's/旧字串/新字串/g' 文件名
[root@localhost ~]$ sed '行范围s/旧字串/新字串/g' 文件名
```

替换的格式和vim非常类似，假设我觉得我自己的PHP成绩太低了，想作弊给他改高点，就可以这样来做:

```
[root@localhost ~]$ sed '3s/74/99/g' student.txt
#在第三行中，把74换成99
```

这样看起来就比较爽了吧。如果我想把AAA老师的成绩注释掉，让他不再生效。可以这样做:

```
[root@localhost ~]$ sed '2s/^/#/g' student.txt
#这里使用正则表达式，“^”代表行首
```

在sed中只能指定行范围，所以很遗憾我在他们两个的中间，不能只把他们两个注释掉，那么我们可以这样:

```
[root@localhost ~]$ sed -e 's/AAA//g ; s/BBB//g' student.txt
#同时把“Liming”和“Tg”替换为空
```

“-e”选项可以同时执行多个sed动作，当然如果只是执行一个动作也可以使用“-e”选项，但是这时没有什么意义。还要注意，多个动作之间要用“;”号或回车分割，例如上一个命令也可以这样写:

```
[root@localhost ~]$ sed -e 's/Liming//g
>s/Tg//g'’ student.txt
```

**其他实例：**

```shell
1、正则表达式必须以”/“前后规范间隔
例如：sed '/root/d' file
例如：sed '/^root/d' file

2、如果匹配的是扩展正则表达式，需要使用-r选来扩展sed
grep -E
sed -r
+ ? () {n,m} | \d

注意：
在正则表达式中如果出现特殊字符(^$.*/[]),需要以前导 "\" 号做转义
eg：sed '/\$foo/p' file


3、逗号分隔符
例如：sed '5,7d' file                  删除5到7行
例如：sed '/root/,/ftp/d' file    
删除第一个匹配字符串"root"到第一个匹配字符串"ftp"的所有行本行不找 循环执行

4、组合方式
例如：sed '1,/foo/d' file            删除第一行到第一个匹配字符串"foo"的所有行
例如：sed '/foo/,+4d' file            删除从匹配字符串”foo“开始到其后四行为止的行
例如：sed '/foo/,~3d' file            删除从匹配字符串”foo“开始删除到3的倍数行（文件中）
例如：sed '1~5d' file                从第一行开始删每五行删除一行
例如：sed -nr '/foo|bar/p' file    显示配置字符串"foo"或"bar"的行
例如：sed -n '/foo/,/bar/p' file    显示匹配从foo到bar的行
例如：sed '1~2d'  file                删除奇数行
例如：sed '0-2d'   file                删除偶数行 sed '1~2!d'  file

5、特殊情况
例如：sed '$d' file                    删除最后一行
例如：sed '1d' file                    删除第一行

6、其他：
sed 's/.//' a.txt                        删除每一行中的第一个字符
sed 's/.//2' a.txt                    删除每一行中的第二个字符
sed 's/.//N' a.txt                    从文件中第N行开始，删除每行中第N个字符（N>2）
sed 's/.$//' a.txt                    删除每一行中的最后一个字符
```

### sort 排序命令

sort命令默认是用每行开头第一个字符来进行排序的。

```shell
[root@localhost~]$ sort [选项] 文件名
#排序用户信息文件
[root@localhost~]$ sort /etc/passwd
#反向排序
[root@localhost~]$ sort -r/etc/passwd
#指定分隔符是“:”，用第三字段开头，第三字段结尾排序，就是只用第三字段排序
[root@localhost~]$ sort -t ":" -k 3,3 /etc/passwd

```

### uniq 取消重复行

```shell
[root@localhost~]$ uniq [选项] 文件名
选项：
    -i：忽略大小写
```

###wc 统计命令

```shell
[root@localhost~]$ wc [选项] 文件名
选项：
    -l：只统计行数
    -w：只统计单词数
    -m：只统计字符数
```

### cut 列提取命令

cut命令的默认分隔符是制表符，也就是“tab”键，不过对空格符可是支持的不怎么好。

```shell
[root@localhost ~]$ cut [选项] 文件名
选项:
-f 列号: 提取第几列
-d 分隔符: 按照指定分隔符分割列
-n  取消分割多字节字符
-c 字符范围: 不依赖分隔符来区分列，而是通过字符范围（行首为0）来进行字段提取。“n-”表示从第n个字符到行尾;“n-m”从第n个字符到第m个字符;“一m”表示从第1个字符到第m个字符。
--complement    补足被选择的字节、字符或字段
--out-delimiter 指定输出内容是的字段分割符
```

我们先建立一个测试文件，然后看看cut命令的作用吧:

```txt
[root@localhost ~]$ vi student.txt
id  name    gender  mark
1   liming  m       86
2   sc      m       67
3   tg      n       90
```

```shell
# 提取第二列内容
[root@localhost ~]$ cut -f 2 student.txt 
# 那如果想要提取多列呢?只要列号直接用“，”分开
[root@localhost ~]$ cut -f 2,3 student.txt
```



## 进阶语法

### Shell 输入/输出重定向

输入/输出重定向是一种在命令行或脚本中控制程序输入和输出的技术，它允许您将程序的输入从键盘或一个文件中读取，并将程序的输出发送到屏幕或另一个文件中。

|      命令       |                        说明                        |
| :-------------: | :------------------------------------------------: |
| command > file  |               将输出重定向到 file。                |
| command < file  |               将输入重定向到 file。                |
| command >> file |         将输出以追加的方式重定向到 file。          |
|    n > file     |       将文件描述符为 n 的文件重定向到 file。       |
|    n >> file    | 将文件描述符为 n 的文件以追加的方式重定向到 file。 |
|     n >& m      |              将输出文件 m 和 n 合并。              |
|     n <& m      |              将输入文件 m 和 n 合并。              |
|     << tag      | 将开始标记 tag 和结束标记 tag 之间的内容作为输入。 |

#### 输出重定向

执行下面的 who 命令，它将命令的完整的输出重定向在用户文件中(users):

```shell
$ who > users
```

执行后，并没有在终端输出信息，这是因为输出已被从默认的标准输出设备（终端）重定向到指定的文件。

你可以使用 cat 命令查看文件内容：

```shell
$ cat users
_mbsetupuser console  Oct 31 17:35 
tianqixin    console  Oct 31 17:35 
tianqixin    ttys000  Dec  1 11:33 
```

输出重定向会覆盖文件内容，请看下面的例子：

```shell
$ echo "i am tobe" > users
$ cat users
i am tobe
```

如果不希望文件内容被覆盖，可以使用 >> 追加到文件末尾，例如：

```shell
$ echo "i am tobe" >> users
$ cat users
i am tobe
i am tobe
```

#### 输入重定向

接着以上实例，我们需要统计 users 文件的行数,执行以下命令：

```shell
$ wc -l users
       2 users
```

也可以将输入重定向到 users 文件：

```shell
$  wc -l < users
       2 
```

注意：上面两个例子的结果不同：第一个例子，会输出文件名；第二个不会，因为它仅仅知道从标准输入读取内容。

```shell
command1 < infile > outfile
```

同时替换输入和输出，执行command1，从文件infile读取内容，然后将输出写入到outfile中。

#### 重定向深入讲解

一般情况下，每个 Unix/Linux 命令运行时都会打开三个文件：

- 标准输入文件(stdin)：stdin的文件描述符为0，Unix程序默认从stdin读取数据。
- 标准输出文件(stdout)：stdout 的文件描述符为1，Unix程序默认向stdout输出数据。
- 标准错误文件(stderr)：stderr的文件描述符为2，Unix程序会向stderr流中写入错误信息。

默认情况下，command > file 将 stdout 重定向到 file，command < file 将stdin 重定向到 file。 如果希望 stderr 重定向到 file，可以这样写：

```shell
$ command 2>file
```

如果希望 stderr 追加到 file 文件末尾，可以这样写：

```shell
$ command 2>>file
```

**2** 表示标准错误文件(stderr)。

如果希望将 stdout 和 stderr 合并后重定向到 file，可以这样写：

```shell
$ command > file 2>&1
或者
$ command >> file 2>&1
```

如果希望对 stdin 和 stdout 都重定向，可以这样写：

```shell
$ command < file1 >file2
```

command 命令将 stdin 重定向到 file1，将 stdout 重定向到 file2。

#### /dev/null 文件

如果希望执行某个命令，但又不希望在屏幕上显示输出结果，那么可以将输出重定向到 /dev/null：

```shell
$ command > /dev/null
```

/dev/null 是一个特殊的文件，写入到它的内容都会被丢弃；如果尝试从该文件读取内容，那么什么也读不到。但是 /dev/null 文件非常有用，将命令的输出重定向到它，会起到"禁止输出"的效果。

如果希望屏蔽 stdout 和 stderr，可以这样写：

```shell
$ command > /dev/null 2>&1
```



### Shell 文件包含

[shell](https://www.coonote.com/shell/shell-tutorial.html) 也可以包含外部脚本。这样可以很方便的封装一些公用的代码作为一个独立的文件。Shell 文件包含的语法格式如下：

```shell
. filename   # 注意点号(.)和文件名中间有一空格
或
source filename
```

创建两个 shell 脚本文件。

test1.sh 代码如下：

```
#!/bin/bash
url="https://www.coonote.com"
```

test2.sh 代码如下：

```
#!/bin/bash
#使用 . 号来引用test1.sh 文件
. ./test1.sh
# 或者使用以下包含文件代码
# source ./test1.sh
echo "官网地址：$url"
```

接下来，我们为 test2.sh 添加可执行权限并执行：

```
$ chmod +x test2.sh 
$ ./test2.sh 
官网地址：https://www.coonote.com
```

### 正则表达式

```shell

元字符	描述	示例
\	转义符，将特殊字符进行转义，忽略其特殊意义	a.b匹配a.b，但不能匹配ajb，.被转义为特殊意义
^	匹配行首，awk中，^则是匹配字符串的开始	^tux匹配以tux开头的行
$	匹配行尾，awk中，$则是匹配字符串的结尾	tux$匹配以tux结尾的行
.	匹配除换行符\n之外的任意单个字符	ab.匹配abc或bad，不可匹配abcd或abde，只能匹配单字符
[ ]	匹配包含在[字符]之中的任意一个字符	coo[kl]可以匹配cook或cool
[^]	匹配[^字符]之外的任意一个字符	123[^45]不可以匹配1234或1235，1236、1237都可以
[-]	匹配[]中指定范围内的任意一个字符，要写成递增	[0-9]可以匹配1、2或3等其中任意一个数字
?	匹配之前的项1次或者0次	colou?r可以匹配color或者colour，不能匹配colouur
+	匹配之前的项1次或者多次	sa-6+匹配sa-6、sa-666，不能匹配sa-
*	匹配之前的项0次或者多次	co*l匹配cl、col、cool、coool等
()	匹配表达式，创建一个用于匹配的子串	ma(tri)?匹配max或maxtrix
{n}	匹配之前的项n次，n是可以为0的正整数	[0-9]{3}匹配任意一个三位数，可以扩展为[0-9][0-9][0-9]
{n,}	之前的项至少需要匹配n次	[0-9]{2,}匹配任意一个两位数或更多位数不支持{n,}{n,}{n,}
{n,m}	指定之前的项至少匹配n次，最多匹配m次，n<=m	[0-9]{2,5}匹配从两位数到五位数之间的任意一个数字
|	交替匹配|两边的任意一项	ab(c|d)匹配abc或abd
```

