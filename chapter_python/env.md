# 环境配置

## 常用操作

### 安装常见问题

添加PPA源，执行命令：

```
sudo add-apt-repository ppa:deadsnakes/ppa
```

如果出现：`add-apt-repository: command not found`的问题，则执行：

```
sudo apt-get update
sudo apt-get install software-properties-common
```

add-apt-repository 命令是software-properties-common包的一部分，因此安装这个包就OK了。

更新软件包：

```
sudo apt update
```

安装python3.8

```
sudo apt install python3.8 python3.8-dev -y
```



### 修改python命令指向

查看默认python指向：

```
ls -l /usr/bin | grep python 
```

删除原有python软连接

```
rm /usr/bin/python
```

建立python到python3.8新的软链接

```
ln -s /usr/bin/python3.8 /usr/bin/python
```

### 修改pip或者pip3指向

查看默认pip、pip3指向：

```
pip --version
pip3 --version
which pip
// 如果是通过编译安装的python，一般会通过软链接链接到/usr/bin下
ls -l /usr/bin | grep pip
```

删除原有python软连接:

```
sudo rm /usr/bin/pip
```

建立新的软连接：

```
sudo ln -s /usr/bin/pip3.8 /usr/bin/pip
```

### 查看包的安装位置、导出安装包

```
pip show package_name
pip3 show package_name

# 当目标环境没有网络时，需要先下载好whl包
pip3 download requests
```

### 导出和安装requirement

先到指定项目下，然后导出：

```
cd /path/to/your/project``pip3 freeze > requirements.txt
```

执行下面的命令即可安装：

```
pip3 install -r requirements.txt
```

### 图片转视频

```
import cv2
import os
 
# 输入图片文件夹路径和输出视频文件路径
image_folder = 'stuttgart_02'
video_name = 'output_video.avi'
frame_rate = 25  # 设置帧率为30帧/秒
 
# 获取图片列表
images = [img for img in os.listdir(image_folder) if img.endswith(".png")]
 
frame = cv2.imread(os.path.join(image_folder, images[0]))
height, width, layers = frame.shape
 
# 创建视频写入对象
video = cv2.VideoWriter(video_name, cv2.VideoWriter_fourcc(*'XVID'), frame_rate, (width, height))
 
for image in images:
    video.write(cv2.imread(os.path.join(image_folder, image)))
 
cv2.destroyAllWindows()
video.release()
```

### 修改python版本指向



### 添加镜像源

#### 手动添加镜像源

使用方法：pip install 包名 -i 所用镜像源网址（这里我用的清华源）

```bash
pip install 下载的模块名 -i https://pypi.tuna.tsinghua.edu.cn/simple
```

#### 永久添加镜像源

使用方法一：打开cmd 添加如下命令

```bash
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

使用方法二：在C盘下创建一个名叫pip的文件夹，在文件夹内创建一个名为pip.ini的文档，添加如下内容，将pip路径添加到环境变量。

```bash
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

#### 国内镜像源 

① 阿里镜像 :  https://mirrors.aliyun.com/pypi/simple/

② 百度镜像: https://mirror.baidu.com/pypi/simple/

③ 清华镜像:https://pypi.tuna.tsinghua.edu.cn/simple/

④ 中科大镜像:https://pypi.mirrors.ustc.edu.cn/simple/

⑤ 豆瓣镜像:http://pypi.douban.com/simple/

⑥ 搜狐镜像:http://mirrors.sohu.com/Python/

⑦ 华中科大镜像:https://pypi.hustunique.com/

⑧ 山东理工大学镜像:https://pypi.hustunique.com/