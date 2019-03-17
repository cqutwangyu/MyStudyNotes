# Git常用指令

## 一、本地仓库

基本操作：

1. `git init`初始化一个`Git`仓库。

2. `git add <filename>`将更新后的文件提交到`Git`仓库本地暂存区。

3. `git add .`将所有更新后的文件提交到`Git`仓库本地暂存区。

4. `git commit -m <message>`将暂存区的文件提交到本地仓库。

5. `git commit -am <message>`类似于指令2+4的组合，但区别在于，指令5只能提交已经提交过的文件，也就是说新增的文件无法提交。

## 二、远程仓库

1. `git clone git@github.com:ChongqingWangYu/My-study-notes.git`从远程仓库克隆到本地仓库。

2. `git remote add origin git@server-name:path/repo-name.git`关联一个远程仓库。

3. `git push -u origin master`关联后第一次推送master分支的所有内容。

4. `git push`把当前分支`master`推送到远程。

5. `git push origin master`同指令3功能类似，`origin`代表远程仓库，`master`代表主分支（分支名）。

   