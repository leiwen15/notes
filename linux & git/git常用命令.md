# git 常用命令
## 一、在同一台电脑上 设置两个 git
+ 查看 git 的全局安装信息
>+ git config --list
+ 在想要修改的 git 仓库中，设置局部信息
>+ git config --loacl user.name leiwen15
>+ git config --local user.email xx@xx.com
## 二、分支管理
+ 创建分支
>+ git checkout -b new_branch1
+ 获取远程分支，并在本地创建对应分支
>+ git checkout -b new_branch2  origin/new_branch2
+ 将本地分支推送到远程（本地新建的，远程没有）
>+ git push --set-upstream origin new_branch1
## 三、git 设置 ignore
+ 添加 .gitignore 文件
>+ 在文件中写具体的内容
## 四、git remote 设置
+ 设置 remote
>+ git remote add origin https://github.local/mmmmmmmmmm.git
