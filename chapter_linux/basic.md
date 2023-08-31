# 基础

## bash快捷键

（1）ctrl+A：把光标移动到命令行开头。如果我们输入的命令过长，想要把光标移动到命令行开头时使用。

（2）ctrl+E：把光标移动到命令行结尾。

（3）ctrl+C：强制终止当前的命令。

（4）ctrl+L：清屏，相当于clear命令。

（5）ctrl+U：删除或剪切光标之前的命令。我输入了一行很长的命令，不用使用退格键一个一个字符的删除，使用这个快捷键会更加方便

（5）ctrl+K： 删除或剪切光标之后的内容。

（6）ctrl+Y：粘贴ctrl+U或ctul+K剪切的内容。

（7）ctrl+R：在历史命令中搜索，按下ctrl+R之后，就会出现搜索界面，只要输入搜索内容，就会从历史命令中搜索。

（8）ctrl+D：退出当前终端。

（9）ctrl+Z：暂停，并放入后台。这个快捷键牵扯工作管理的内容。

（10）ctrl+S：暂停屏幕输出。

（11）ctrl+Q：恢复屏幕输出。

## 常用命令

### gdb

```bash
gdb --args ./segformer_sail.pcie --input=../../datasets/test_car_person_1080P.mp4
1）gdb 直接进入调试模式，再输入file + xxx 跟踪； 或直接 gdb xxx
2）run (r) 运行
3）break（b） 断点，可以break mian 直接在函数处增加断点，也可以 break:10 在第几行增加断点
4）next (n) 继续执行下一步
5）step(s) 单步调试
6）continue （c） 继续执行
7）info（i）显示信息， i b 显示断点信息
8）delete （d）删除断点，删除单个断点添加断点号，删除全部断点直接d指令
9）print（p）显示变量的值或者数组的值，数组支持索引
10）quit（q）退出gdb
```

### 解压缩

```bash
unzip filename.zip
zip -r filename.zip directory/
unzip filename.zip -d /path/to/destination
 
 
tar -xvf filename.tar
tar -xzvf filename.tar.gz
tar -xvf filename.tar -C /path/to/destination
tar -xzvf filename.tar.gz -C /path/to/destination
 
//使用 -d 或 -C 参数时，指定的路径必须是已经存在的目录
 
tar -cvf filename.tar directory/
tar -czvf filename.tar.gz directory/
 
- c 表示创建归档文件
- z 表示使用 gzip 压缩
- v 表示显示详细信息
- f 表示指定文件名
```

### 显示环境变量

```bash
//显示所有环境变量
printenv
//显示名为PATH的环境变量及其值
echo $PATH
```

### 设置环境变量

```
//只对当前shell有用，关了重启会消失
export MY_VAR=hello
//追加环境变量
export PATH=$PATH:/path/to/new/directory
//永久方法
vi ~/.bashrc
export MY_VAR=value
source ~/.bashrc
```

### 显示当前使用的whoami用户名

```bash
whoami
which
history
manmkdir
uname-a
```

### cat

```bash
//显示文件内容
cat /etc/passwd
//显示多个文件内容
cat testtest1
//创建文件,我们将使用以下命令创建一个名为test2文件的文件。
cat >test2
//等待用户输入，键入所需的文本，然后按CTRL + D（按住Ctrl键并键入" d "）退出。文本将写入test2文件中。您可以使用以下cat命令查看文件的内容。
cat test2
hello everyone, how doyou do?
```

### tail

```bash
//与cat类似，tail打印文件内容时有一个主要警告：它只输出最后几行。默认情况下，它打印最后10行，但您可以使用-n修改该数字。,例如，要打印大型文本文件的最后几行，可以使用：
tail long.txt
tail -n 4 long.txt
```

### 查找命令

```bash
find \[flags\] \[path\] -name \[expression\]
//查找当前目录及其子目录中以 .txt 结尾的所有文件
find . -name "*.txt"
//查找 /home/user/documents 目录下所有以 .docx 结尾的文件
find /home/user/documents -name "*.docx"
//查找 /home/user/documents 目录下大小超过 1MB 的文件
find /home/user/documents -size +1M
```

### 磁盘相关

```bash
mount \[-hV\]
mount -a \[-fFnrsvw\] \[-t vfstype\]
mount \[-fnrsvw\] \[-o options \[,...\]\] device | dir
mount \[-fnrsvw\] \[-t vfstype\] \[-o options\] device dir
//将把 /dev/sdb1 这个设备挂载到 /mnt/usb 这个目录下
sudo mount /dev/sdb1 /mnt/usb
//把 /dev/sdc1 这个 NTFS 格式的设备挂载到 /mnt/windows 这个目录下。-t ntfs 表示设备的文件系统类型是 NTFS。挂载一个网络共享目录（NFS）：
sudo mount -t ntfs /dev/sdc1 /mnt/windows
//挂载所有在 /etc/fstab 文件中定义的文件系统
sudo mount -a
//查看已挂载的文件系统
mount
 
lsblk: 显示块设备信息，包括硬盘、分区和挂载点。
 
fdisk: 管理磁盘分区的命令行工具，可以创建、删除和查看分区。
sudo fdisk -l           # 列出所有磁盘和分区
sudo fdisk /dev/sdX     # 进入磁盘sdX的分区管理界面（用实际设备代替X）
 
parted: 另一个用于磁盘分区的命令行工具，功能比fdisk更强大。
sudo parted -l         # 列出所有磁盘和分区
sudo parted /dev/sdX   # 进入磁盘sdX的分区管理界面（用实际设备代替X）
 
mkfs: 创建文件系统。常见的文件系统包括ext4、NTFS等。
sudo mkfs.ext4 /dev/sdXY   # 创建ext4文件系统（用实际设备和分区代替X和Y）
 
mount: 挂载文件系统到指定的挂载点。
sudo mount /dev/sdXY /mnt   # 将sdXY分区挂载到/mnt目录（用实际设备和分区代替X和Y）
 
umount: 卸载挂载的文件系统。
sudo umount /mnt   # 卸载/mnt目录下的文件系统
 
df: 显示文件系统的磁盘使用情况。
df -h   # 以人类可读的方式显示磁盘使用情况
 
du: 显示指定目录或文件的磁盘使用情况。
du -h /path/to/directory   # 以人类可读的方式显示目录的磁盘使用情况
```

### 进程相关

```bash
ps：显示当前用户的进程状态。常用选项如下：
ps aux：显示所有用户的所有进程信息。ps-aux | grepmediamtx
ps -ef：显示所有进程信息。
ps aux | grep<进程名>：根据进程名过滤显示相关进程。
top：实时显示进程状态，按 CPU 占用排序。可按 q 键退出。
htop：类似于 top命令，但提供更友好的交互界面和更多功能。需要先安装 htop 包。
kill：终止进程。常用选项如下：
kill <进程ID>：通过进程ID终止指定进程。
kill -9 <进程ID>：使用强制终止信号(SIGKILL)终止进程。
kill all：根据进程名终止进程。使用时需谨慎，因为它会终止所有匹配进程。
kill all <进程名>：终止所有指定名称的进程。
pgrep：通过进程名查找进程ID。
pgrep <进程名>：查找匹配进程名的进程ID。
pkill：根据进程名终止进程。
pkill <进程名>：终止所有指定名称的进程。
jobs：显示在后台运行的作业。
```

### 网络相关

```bash
ifconfig：查看和配置网络接口信息，如IP地址、子网掩码等。不过在较新的Linux发行版中，ifconfig已被弃用，建议使用ip命令代替。
ip：一个强大的工具，用于管理网络接口和路由。它可以执行ifconfig的功能，还支持更多高级功能。
示例：
ip address show：查看所有网络接口的IP地址信息。
ip link：列出网络接口及其状态。
ip route：显示路由表。
ping：用于测试与目标主机之间的连通性。它发送ICMP回显请求并等待回复。
示例：ping google.com
traceroute（或tracert）：跟踪数据包从本地到目标主机的路径。
示例：traceroute google.com
netstat：显示网络统计信息，如网络连接、路由表、接口状态等。
示例：netstat -tuln（查看所有TCP和UDP端口的监听情况）
ss：netstat的替代工具，用于显示套接字信息，如网络连接、路由表等。
示例：ss -tuln（查看所有TCP和UDP端口的监听情况）
nslookup（或dig）：用于查询DNS（域名系统）记录，获取主机名对应的IP地址和反向查询等。
示例：nslookup google.com
route：查看和管理内核IP路由表。
示例：route -n（显示数字格式的路由表）
wget：用于从网络下载文件。
示例：wget http://example.com/file.txt
curl：通过URL方式传输数据，支持多种协议。
示例：curl http://example.com
ssh：用于通过安全的加密方式远程登录到其他Linux服务器。
示例：ssh username@remote_host
scp：用于通过SSH安全地复制文件和目录。
示例：scp file.txt username@remote_host:/path/to/destination
 
查看监听端口：
sudo netstat -lnp | grep nginx
```
