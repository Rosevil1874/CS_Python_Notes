# Git


### 169.说说你知道的 git 命令
新建：git init
克隆：git clone 'url'

删除文件：rm <filename>
查看更改：git status
添加更改：git add <filename>
添加全部更改：git add .

连接到远程：git remote add origin <url>
提交更改：git commit -m 'commit msg'
将本地同步到远程：git push
将远程同步到本地：git pull

新建分支：git checkout -b  <branch>
删除分支：git checkout -d  <branch>
切换分支：git checkout master
将分支推到远程：git push origin  <branch>
将更改合并到另一分支：git merge <branch>
查看分支差异：git diff  <branch>  <branch>

提交id：git log


### 170.git 如何查看某次提交修改的内容
1. git log 打印出提交id：<commitId>
2. git show <commitId> 查看这次提交修改的内容。