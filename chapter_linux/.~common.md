# 常用操作

## linux挂载nas、ftp

### nas

创建挂载目录：

```
mkdir ~/sophgo_drive
```

挂载：

```
sudo` `mount` `-t cifs -o domain=sophgo-inc,username=zhiyuan.zhang //disk.sophgo.vip/home/Drive ~/sophgo_drive
```



输入nas密码：

```
xxx
```

取消挂载：

```
sudo umount ~/sophgo_drive
```

### ftp

```
//挂载
sudo apt-get update
sudo apt-get install curlftpfs
sudo mkdir ftp
curlftpfs  ftp://172.28.141.89 /home/frotms/hdd/zhiyuan.zhang/ftp -o user=AI:password
//卸载
sudo umount /mnt/ftp
```

