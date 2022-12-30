@[TOC](git相关知识)
### 1. 用途
版本管理工具
### 2. 下载

#### 2.1参考资料
- [大牛写的详细安装教程](https://blog.csdn.net/mukes/article/details/115693833?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166875290416782390596877%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166875290416782390596877&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-2-115693833-null-null.142%5Ev65%5Econtrol,201%5Ev3%5Econtrol,213%5Ev2%5Et3_esquery_v2&utm_term=git&spm=1018.2226.3001.4187)
- [Git 官网](https://git-scm.com/)

- [官方文档](<https://git-scm.com/docs>)

- [GitHub Cheat Sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf)

- [Visual Git Cheat Sheet](http://ndpsoftware.com/git-cheatsheet.html)

- [一个国人写的Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)

- [Pro Git](https://git-scm.com/book/zh/v2)

- [猴子都能懂得 GIT 入门](https://backlog.com/git-tutorial/cn)

- [git游戏](https://learngitbranching.js.org)

#### 2.2 验证是否安装成功
- 在控制台中：git --version
- 鼠标右键

### 3. gitbash的使用：
- git命令行 gitbash(是一个应用程序，模拟终端，比自带的cmd功能强)
- 图形化界面 tortoiseGit、git GUI、sourceTree、开发工具中集成

```
# 新建目录
$ mkdir 目录1 目录2 ...

# 进入目录
$ cd 目录1

# 返回上级目录
$ cd ..

# 查看目录
$ ls

# 新建文件
$ touch 文件名1 文件名2

# 删除文件
$ rm 文件名1 文件名2

# 查看文件内容
$ cat 文件名1 

# 查看文件内容 需要按Q退出
$ less 文件名1

# tab键
自动补全

# 上下方向键
切换历史命令

# 清空屏幕
$ clear
```

下面的命令试了没有反应
```
# 创建并进入文件编辑模式
$ vi 文件名

# 进入插入编辑模式
$ i

# esc退出插入编辑模式
键盘esc

# 退出编辑模式，但不保存
$ :q

# 保存并退出编辑模式
$ :wq

# 强制退出但不保存编辑模式
$ :q!
```
### 4. git
#### 4.1 git 工作流程命令
- 建立一个空目录，在文件夹中点击右键，运行gitbash
- `git init`
- 在工作目录的添加文件
- `git status`  查看状态
- `git log`     查看日志
- `git add .`   将所有文件都添加到暂存区        
- `git add filename`    将指定文件添加到暂存区
- `git commit -m "提交说明"`    将提交到仓库的文件进行情况说明
	
	- （1）初次提交要先登记
	```
	$ git config --global user.email "邮箱地址"
	$ git config --global user.name "昵称"
	```
	- （2）邮箱地址和昵称可以进行修改
	```
	# 删除原信息
	$ git config --global --unset user.email "邮箱地址"
	$ git config --global --unset user.name "昵称"
	# 重新设置信息
	```
	- （3）在开发过程中，不要过于频繁地提交代码，而是应该完成某个功能开发之后，再去提交。
	- （4）对于commit的内容也应该遵循固定的格式与规范，可以使用[`commitizen`](https://www.jianshu.com/p/36d970a2b4da)来帮助写commit
		
		- `npm install -g commitizen`
		- `commitizen init cz-conventional -changelog --save-dev --save-exact`
		
#### 4.2 文件的四种状态
- 未跟踪     没有进行git add 的文件
- 已跟踪     已执行git add 的文件
    - 已修改    已执行ctrl+s操作
    - 已暂存    已进行commit操作
    - 已提交    已保存到git库中
		
#### 4.3撤销修改内容
-  （1）放弃工作区的修改     没有执行git add
	```
	# 放弃指定文件的修改
	$ git checkout -- 文件名1
	
	# 放弃所有文件的修改
	$ git checkout .
	```
- （2）放弃暂存区的修改      已执行git add
	两个命令
	```
	# 放弃指定文件
	$ git rest HEAD 文件名1
	$ git checkout -- 文件名1
	
	# 放弃所有文件
	$ git reset HEAD
	$ git checkout .
	```

- （3）从仓库恢复    已执行commit
每次提交都会有一个commitID，是一个永远不重复的编号，表示每一次的提交
通过`git log`查看
	```
	# 回滚整体版本
	git reset -- hard commitID

	# 恢复某一个文件
	$ git reset commitID 文件名
	$ git commit -m "提交说明"
	$ git checkout 文件名
	
	# 恢复某一个文件（简化版）
	$ git checkout commitID 文件名
	```

#### 4.4 分支管理
```
# 新建分支
$ git branch 分支名称
	
# 切换分支
$ git  checkout 分支名称
	
# 新建分支并切换到该分支
$ git checkout -b 分支名称
	
# 指定的分支名 合并到 当前的分支
$ git merge 分支名 
	
# 删除分支
$ git branch -d 分支名称
	
# 列出所有远程分支
$ git branch -a
	
# 新建分支，指向指定commit
$ git branch [分支名称] [commit]
	
# 图形化查看git commit的过程
$ git log --graph
$ gitk
```
#### 4.5  分支使用流程
开发过程中会接触三个分支
- master主分支
- dev开发分支
- bug临时分支
	```
	// 当前在dev分支进行开发
	
	// （1）保存目前手头上在dev分支上的修改
	git stash 或者 git commit
	
	// （2）从当前分支切换到master主分支
	git checkout master
	
	// （3）在maste分支上拉出一个新分支，分支名字包含bug及bug编号
	git checkout -b bug1118
	
	// （4）修改代码，修复bug
	git add 
	git commit -a ''
	
	// （5）解决完bug切换到master主分支
	git checkout master
	
	// （6）在maste分支上合并bug分支
	git merge bug1118
	
	// （7）可以删除bug1118分支
	git branch -d bug1118
	
	// （8）回到dev分支 继续开发
	git checkout dev
	(如果之前有git stash，则通过git stash pop恢复)
	```

#### 4.6 分支中的冲突
- 一般情况下，git会自动合并分支，且不会产生冲突
- 产生冲突的情景：
    - a分支修改文件1 且进行commit
    - b分支修改文件1 且进行commit
    - 两个分支修改了`同一个地方`

解决：
1. 打开有冲突的文件
2. 根据实际情况手动修改（注意去掉冲突时自动添加的特殊符号）
3. 保存修改 进行commit
### 5 git与github的关系
git是一个版本管理工具
github是一个网络版本的代码库

##### 5.1.1 如何下载代码
- 复制SSL地址
- 运行命令：`git clone 地址`

##### 5.1.2 如何建立自己的代码库
 1. 在github上建立仓库
 2. 在A电脑上：使用http协议，通过git clone到本地
 	clone命令会创建一个文件夹
 	clone命令只需要在第一次使用
 3. 在A电脑上：编辑代码，提交到本地仓库
 	```
 	git add .
 	git commit
 	```
 4. 在A电脑上：把本地仓库同步到github仓库中
 	```
 	git push
 	```
 5. 在B电脑上：下载代码到本地
 	```
	git clone
 	```
 6. 在B电脑上：提交前`先`拉取最新代码
 	```
 	git pull
 	```
 	可能会有多人在修改代码，所以提交之前先拉取最新代码

##### 5.1.3 本地代码库关联到远程github
1. 在github上建立一个人和本地代码库同名的代码库
2. 使用命令
	```
	git remote add origin https://github.com/dilireba/04-git.git
	git push -u origin master
	```
	解释：
	把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
	但是远程仓库是空的，所以在第一次推送master分支时，加上了-u参数。
	git不但会把本地的master分支内容推送到远程新的master分支，还会把本地的master分支 和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
	```
	$ git config --global --unset user.name dilireba
	$ git config --global --unset user.email dilireba@163.com
	```
	也可以用`git commit -a -m "提交说明"` 代替上面的两行代码
	
### 6 打标（代表性的功能是来标记发布节点）
```
# 查看已有标签
$ git tag

# 在当前commit新建一个tag
$ git tag [tag]

# 在指定的commit新建一个tag
$ git tag [tag] [commit]

# 删除本地tag
$ git tag -d [tag]

# 删除远程tag
$ git push origin :refs/tags/[tagName]

# 查看tag信息
$ git show [tag]

# 提交指定tag
$ git push [remote] [tag]

# 提交所有tag
$ git push [remote] --tags

# 新建一个分支，指向某个tag
$ git checkout -b [branch] [tag]
```

### 7 .gitignore文件（忽略文件）
作用：存放git工作区中被默认不追踪的文件信息
例如：忽略所有的js文件和node_modules
```
*.js
node_modules
```
如果一个文件已经在git仓库中跟踪了，则必须先从跟踪状态中移除
```
git rm --cached
```
	
### 8 名词解释
- **Version Control（版本控制）:** 任何一个能够让你了解文件的历史，以及该文件的发展进程的系统。
- **Git：** 一个版本控制程序，通过对变更进行注释，以创建一个易于遍历的系统历史。
- **Commit（提交）：** 在指定时间点对系统差异进行的注释 “快照”。
- **Local（本地）：** 指任意时刻工作时正在使用的电脑。
- **Remote（远程）：** 指某个联网的位置。
- **Repository (仓库，简称 repo)：** 配置了Git超级权限的特定文件夹，包含了你的项目或系统相关的所有文件。
- **Github：** 获取本地提交历史记录，并进行远程存储，以便你可以从任何计算机访问这些记录。
- **Push（推送）：** 取得本地Git提交（以及相关的所有工作），然后将其上传到在线Github。
- **Pull（拉取）：** 从在线的Github上获取最新的提交记录，然后合并到本地电脑上。
- **Master (branch)：主分支，** 提交历史 “树”的 “树干”，包含所有已审核的内容/代码。
- **Feature branch（功能分支/特性分支）：** 一个基于主分支的独立的位置，在再次并入到主分支之前，你可以在这里安全地写工作中的新任务。
- **Pull Request（发布请求）：** 一个 Github 工具，允许用户轻松地查看某功能分支的更改 （the difference或 “diff”），同时允许用户在该分支合并到主分支之前对其进行讨论和调整。
- **Merge（合并）：** 该操作**指**获取功能分支的提交，加入到主分支提交历史的顶部。
- **Check out（切换）：** 该操作指从一个分支切换到另一个分支。
