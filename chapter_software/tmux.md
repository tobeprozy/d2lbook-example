# tmux使用教程

官网：https://github.com/tmux/tmux
tmux基础功能和screen差不多，但是目前来说tmux总体上比screen更加好用些。

## 安装

在Ubuntu系统中可以使用下面命令安装tmux：
sudo apt install tmux

## 创建新会话

tmux 创建新会话并进入；
tmux new -s name 创建一个名为name的会话并进入；（推荐做法）
tmux创建的会话会在底部依次显示会话名、窗口名、主机名、时间等信息；

## 退出会话

在tmux创建的会话中依次按下键盘 ctrl + b d 退出当前会话；

## 列出已创建的会话

使用 tmux ls 可以列出已创建的会话，会话名称、会话含有的窗口数、创建时间；
如果已经在tmux创建的会话中的话也可以依次按下键盘 ctrl + b s 进行查看，这个功能比较厉害，还可以预览各个会话的内容，并选择切换；

## 重新进入会话

tmux a -t name 使用会话名称重新进入已存在的会话；
如果已经在tmux创建的会话中的话也可以使用 tmux switch -t name 切换会话（没有 ctrl + b s 来的好用）；

## 关闭会话

tmux kill-session -t name 使用会话名称关闭已有会话；
如果已经在tmux创建的会话中的并且只有一个窗口和窗格的情况下可以按下键盘 ctrl + d 关闭当前会话；

## 重命名会话

tmux rename-session -t old-name new-name

## 窗口使用

一个tmux的会话中可以有多个窗口(window)，每个窗口又可以分割成多个窗格(pane)。对窗口和窗格相关操作都是在会话中进行的。

### 新建窗口

在会话中依次按下键盘 ctrl + b c 创建新窗口；
多个窗口下底部带*标记的为当前活动窗口；

ctrl + b % 将当前窗口垂直分割；
ctrl + b " 将当前窗口水平分割；

### 切换窗口

ctrl + b w 列出所有窗口，可以预览并选择切换；
ctrl + b 0 切换到0号窗口，依此类推；
ctrl + b p 上一个窗口；
ctrl + b n 下一个窗口；

ctrl + b ↑ 、ctrl + b ↓ 、ctrl + b ← 、ctrl + b →

### 关闭窗口

ctrl + b & 关闭当前窗口，会提示，按下y并回车确定；
当前窗口只有一个窗格的情况下可以按下键盘 ctrl + d 关闭当前窗口；
ctrl + b x 关闭当前窗口，会提示，按下y并回车确定；
也可以按下键盘 ctrl + d 关闭当前窗口，不会提示；

### 调整窗格

ctrl + b space 依次切换窗格布局；
ctrl + b { 当前窗格与上一个窗格交换位置；
ctrl + b } 当前窗格与下一个窗格交换位置；

### 缩放窗格

ctrl + b z 当前窗格全屏显示，再使用一次会变回原来大小；

### 拆分窗格


ctrl + b ! 将当前窗格拆分为一个独立窗口；