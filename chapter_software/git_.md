# git 基础知识

## git 常用操作

### 最基本操作
```bash
git init # 将执行该命令时所在的目录初始化为一个 git 仓库（如：进入某目录后执行该命令会将该目录初始化为一个 git 仓库）
git add readme.md # 将 readme.md 文件添加到暂存区
git add . # 将当前工作目录的所有文件添加到暂存区
git commit -m 'Add readme.md' # -m 指定 commit 的信息
git push <远端名> <本地分支名>
git status # 查看工作目录和暂存区的状态
git log # 只查看当前分支(Head所指的分支)的log情况
git checkout branch_name # 切换分支
```

### 放弃本地代码：

```bash
git branch     查看自己 所在分支
git fetch --all  下载远程仓库最新代码  不做合并处理
git reset --hard origin/当前分支       #把head指针指向刚刚下载的最新代码，撤销本地、暂存区的修改，用版本库(github上面的新代码替代)**加粗样式**
```
### 回退操作
第一种方式：重置reset （谨慎：重置的方式不会保留废弃的提交记录）

1、查看并找到我们要回退的版本号。

```bash
git log
```
假如我们要回退到的历史版本号b498237e6dc1fc4861c79d3314d07285995b

2、git回滚到指定版本
```bash
git reset --hard  b498237e6dc1fc4861c79d3314d07285995b
```

3、push到远程分支，加-f标识强制push
```bash
git push -f origin main
```

第二种方式：撤销/还原revert

1、查看并找到我们要还原的版本号。

```bash
git log
```
假如我们要还原到的历史版本号b498237e6dc1fc4861c79d3314d07285995b

2、git还原到指定版本
```bash
git revert --hard  b498237e6dc1fc4861c79d3314d07285995b
```

3、push到远程分支，加-f标识强制push
```bash
git push -f origin main
```

