## Git 采坑记录

### 1 本地与远端 拒绝合并无关历史

在 Github 上创建了一个仓库，自带了 readme 和 license 文件，如果本地项目已经 Git 初始化后，需要关联远端仓库，并且将远端的文件 git pull 下来，才可以进行推送。在进行 git pull origin master 操作时，极大可能会发生错误并提示：拒绝合并无关的历史。

```shell
# 本地关联远端 master 分支
git remote add origin master https://github.com/xxx/xxx.git
# 从远端 pull 文件下来，使用 git pull origin master 是不行的，需要加上下面这条命令才能 pull
git pull origin master --allow-unrelated-histories
# 现在就是进行 push 操作了
git push -u origin master
```

## 2 

