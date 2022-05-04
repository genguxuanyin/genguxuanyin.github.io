# git使用命令

[参考链接](https://www.cnblogs.com/kenshinobiy/p/4543976.html)

## 检查git版本

`git --version`
`git -v`

## 配置

### 设置git使用者邮箱
`git config --global user.email "<邮箱>"`

### 查询git使用者邮箱
`git config --global user.email`

### 设置git使用者名称
`git config --global user.name "<姓名>"`

### 查询git使用者名称
`git config --global user.name`

### 查询git config
`git config --list`

## 基础操作

### 在指定目录创建仓库，如果没有指定目录名将在当前目录创建仓库
`git init [目录名]`

### 从指定地址克隆仓库，若不指定目录名将默认创建与远程同名目录
`git clone <远程仓库地址> [目录名]`

### 将文件或目录中已修改的代码添加追暂存区
`git add .`
`git add <目录名|文件名>`

### 撤销上一次add
`git reset HEAD`

### 指定目录或文件进行撤销add
`git restore --staged <目录名|文件名>`

或

`git reset HEAD <目录名|文件名>`

或

`git rm --cached <目录名|文件名>`

### 提交暂存区内容
`git commit -m "<注释>"`

### 把已跟踪的目录添加到暂存区并提交到本地仓库
`git commit -am "<注释>"`

### 从暂存区移除，并移除出工作目录
`git rm <目录名|文件名>`

### 查看仓库状态
`git status`

### 放弃单个文件修改(回到上一次add状态)
`git checkout -- <目录名|文件名>`

### 放弃所有的文件修改(回到上一次add状态)
`git checkout . `

## 比对 diff

### 比对当前内容和暂存区内容
`git diff`

### 比对当前内容和最近一次提交
`git diff HEAD`
或
`git diff --staged`

### 比对当前内容和倒数第二次提交
`git diff HEAD^`

### 比对最近两次提交
`git diff HEAD^ HEAD`

## 历史 log

### 查看提交历史
`git log [--oneline] [--all]`

### 打印为单行log
`git log --oneline`

### 打印所有记录（忽略HEAD的位置）
`git log --all`

### 打印示意图（忽略HEAD的位置）
`git log --graph`


## stash
### 保存当前未commit的代码
`git stash`

### 保存当前未commit的代码并添加备注
`git stash save "备注的内容"`

### 列出stash的所有记录
`git stash list`

### 删除stash的所有记录
`git stash clear`

### 应用最近一次的stash
`git stash apply`

### 应用最近一次的stash，随后删除该记录
`git stash pop`

### 删除最近的一次stash
`git stash drop`

## 分支 branch
### 有分支：创建分支，无分支：列出所有本地的分支
`git branch [分支]`

### 查看所有分支
`git branch -a`

### 查看本地分支
`git branch -l`

### 查看远程分支：
`git branch -r`

### 切换至分支
`git checkout <分支>`

### 创建并切换至分支分支
`git checkout -b <分支>`

### 删除分支
#### 安全删除（分支已合并）
`git branch -d <分支>`

#### 强制删除（分支未合并，不能安全删除）
`git branch -D <分支>`

### 删除本地的远程分支
`git branch -r -D origin/[分支]`

### 远程删除git服务器上的分支：
`git push origin -d [分支]`

### 一次删除所有已经合并的分支，不包括master和develop
`git branch -merged | egrep -v "(^*|master|develop)" | xargs git branch -d`

### 修改分支名称
假设分支名称为oldName
想要修改为 newName

1. 本地分支重命名(还没有推送到远程)

`git branch -m oldName newName`
2. 远程分支重命名 (已经推送远程-假设本地分支和远程对应分支名称相同)
a. 重命名远程分支对应的本地分支

`git branch -m oldName newName`
b. 删除远程分支

`git push --delete origin oldName`
c. 上传新命名的本地分支

`git push origin newName`
d.把修改后的本地分支与远程分支关联

`git branch --set-upstream-to origin/newName`

e. 查看所有分支

`git branch -a`

### 将分支与当前分支合并
`git merge <分支>`

### 放弃当前merge

`git merge --abort`

## Tag
### 添加tag
`git tag -a [tagName] -m "[memoContent]" `

### 展示所有tag
`git tag`

### 显示tag信息
`git show [tagName]`

### 回到tag所在
`git checkout [tagName]`

### 推送tags
`git push --tags`

## 远程

### 拉取远程仓库
`git pull`

`git fetch & git merge`

### 推送至远程仓库
`git push -u <远程仓库> <分支>`

### 查看远程仓库origin
`git remote -v`

### 新增远程仓库origin
`git remote add origin https://xxx.git`

### 修改远程仓库origin
`git remote set-url origin https://xxx.git`


## 设置 Git 短命令

方式一

`git config --global alias.ps push`

方式二

`vim ~/.gitconfig`

写入
```
[alias] 
        co = checkout
        ps = push
        pl = pull
        mer = merge --no-ff
        cp = cherry-pick
```

![一图胜千言](https://cdn.biaoyansu.com/TQDj8Uo1pj3YkMSoeSitYC1QB4a019V68N6GZFBE.png)

