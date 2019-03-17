# Git常用指令

## 一、本地仓库

### 基本操作：

1. `git init`初始化一个`Git`仓库。
2. `git add <filename>`将更新后的文件提交到`Git`仓库本地暂存区。
3. `git add .`将所有更新后的文件提交到`Git`仓库本地暂存区。
4. `git commit -m <message>`将暂存区的文件提交到本地仓库。
5. `git commit -am <message>`类似于指令2+4的组合，但区别在于，指令5只能提交已经提交过的文件，也就是说新增的文件无法提交。
6. `git checkout --file` 丢弃暂存区的修改。

### 版本回退：

1. `git log`查看提交日志
2. `git reset --hard commit_id`回退到`commit_id`（版本号）。
3. `git reflog`查看命令历史

### 分支管理：

1. `git branch`查看分支
2. `git branch <name>` 创建分支
3. `git branch -d <name>`删除分支
4. `git merge <name>`合并分支
5. `git checkout <name>`切换分支
6. `git checkout -b <name>`创建并切换分支

## 二、远程仓库

1. `git pull` 从远程仓库拉取。

2. `git remote -v`查看远程仓库信息。

3. `git clone git@github.com:ChongqingWangYu/My-study-notes.git`从远程仓库克隆到本地仓库。

4. `git remote add origin git@server-name:path/repo-name.git`关联一个远程仓库。

5. `git push -u origin master`关联后第一次推送master分支的所有内容。

6. `git push`把当前分支`master`推送到远程。

7. `git push origin master`同指令3功能类似，`origin`代表远程仓库，`master`代表主分支（分支名）。

   

## 三、标签管理

1. `git tag <TagName> commit_id`创建标签
2. `git tag -d <tagname>`删除标签
3. `git push origin <tagname>`与`git push origin --tags`标签推送到远程仓库
4. `git push origin :refs/tags/<tagname>`删除远程仓库标签
5. `git tag -a <tagname> -m <message>`设置标签信息
6. `git tag` 查看所有标签