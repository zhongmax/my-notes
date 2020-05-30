# SVN操作记录

## 1、创建版本库

新建一个 `SVN` 文件夹存放版本库

```shell
mkdir svn
```

在这个目录下新建版本库

```shell
svnadmin create spring-mvc-demo
cd spring-mvc-demo
```

## 2、设置版本库权限

在 VisualSVN Server 中选择仓库右键选择 Properties

在 Security 下，添加组或者用户，设置对应的权限，确定退出

## 3、SVN checkout 操作

在 VisualSVN Server 中选择仓库，右键复制URL到粘贴板

选择一个位置，使用命令行或者鼠标右键选择 SVN Checkout

```shell
svn checkout (SVN URL) --username xxx
```

此时当前目录下会出现从服务器上检出的文件

注：SVN checkout 会自动保存用户信息，推荐关闭认证缓存

Windows: 在 %appdata%/subversion 下，找到 config 文件

Linux: 在 ~/.subversion/conf 下

取消以下两行注释

```shell
# store-password = no
# store-auth = no
```

并删除 auth 目录

## 4、SVN 常用操作

此时，就可以将代码放在目录下，对其进行版本控制

SVN 常用的命令：

```shell
# 将项目 checkout 到本地
svn checkout svn_url --username xx
# 向版本库添加文件
svn add [file|*|*.*]
# 提交 commit
svn commit -m "提交信息"
# 更新版本到服务器
svn update
# 查看文件状态
svn status
# 查看日志 
svn log
# 比较差异
svn diff
# 合并两个版本之间的差异
svn merge
```

