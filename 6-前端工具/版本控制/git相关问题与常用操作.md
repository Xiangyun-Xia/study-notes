## git相关问题与常用操作

#### Mac下删除git文件夹

今天在使用git的时候，在错误的目录下执行了`git init`，而在mac系统下看不到`.git`的文件夹，于是参考了[Mac 删除git文件夹,删除svn文件夹](https://blog.csdn.net/u012881015/article/details/51960182)文章中的方法，删除了该文件夹。

- 删除方法：
  1. `cd 文件夹名称`
  2. `find . -name ".git" | xargs rm -Rf`



#### 修改git提交账户名称

- 修改用户名：`git config --global user.name 'yourname'`
- 修改邮箱：`git config --global user.email 'email@email.com'`



#### 常见的git命令

- 克隆项目：`git clone 项目地址`
- 添加文件到暂存区：`git add .`
- 提交文件：`git commit -m '提交说明'`
- 推送项目：`git push`
- 拉取项目：`git pull`
- 查看提交日志：`git log`
- 查看分支：`git branch`
- 查看远程分支：`git branch -r`
- 查看本地和远程分支：`git branch -a`
- 删除本地分支：`git branch -D '本地分支名称'`
- 切换分支：`git checkout <分支名称>`
- 创建并切换分支：`git checkout -b <分支名称>`
- 查看工作目录与暂存区的状态：`git status`
- 文件对比：`git diff`
- 合并分支：`git rebase`
- 解决冲突：`git rebase --continue`
- 强推：`git push -f`
- 拉取所有分支和远程一致：`git up`