配置
	name
		git config --global user.name  '名字'
	email
		git config --global user.email "邮箱"
使用git:
	git status
		- 查看当前仓库的状态
	git init 
		- 初始化仓库
	
	刚刚添加到项目中的文件处于未跟踪状态：
		未跟踪 ---> 暂存
			git add <filename> 将文件切换到暂存的状态
			git add *  将所有已修改（未跟踪）的文件暂存
			git add .  将所有已修改（未跟踪）的文件暂存
		暂存 ---> 未修改
			git commit -m "xxxx" 将暂存的文件存储到仓库中
			git commit -a -m "xxxx"  提交所有已修改的文件
		未修改 ---> 已修改
			修改代码后，文件会变为修改状态
			
	4. 常用命令
		重置文件
			git restore <filename> # 恢复文件
			git restore  --staged <filename>  # 取消暂存状态
		删除文件
			git rm <filename> # 删除文件
			git rm <filename> -f  # 强制删除
		移动文件
			git mv from to # 移动文件  重命名文件

### 分支

git在存储文件时，每一次代码的提交都会创建一个与之对应的节点，git就是通过一个一个的节点来记录代码的状态的。节点会构成一个树状结构，树状结构就意味着这个树会存在分支，默认情况下仓库只有一个分支，命名为master，在使用git时，可以创建多个分支，分支与分支之间相互独立，在一个分支上修改代码不会影响其他的分子。

```bash
git branch  	# 查看分支
git branch <branch name> # 创建新的分支
git branch -d <branch name>	# 删除分支
git switch <branch name>	# 切换分支
git switch -c <branch name >	创建并切换分支
```

在开发中，都是在自己的分支上编写代码，代码编写完成后，再将自己的分支合并到主分支你人呢，

### 变基（rebase）

在开发中除了通过merge来合并分支外，还可以通过变基来完成分支的合并。

我们通过merge合并分支时， 在提交记录中会将所有的分支创建和分支合并的过程全部显示出来，这样当项目比较复杂，开发过程比较波折时，必须要反复的创建、合并、删除分支，这样一来将会使得我们代码的提交记录变得极为混乱。

原理（变基时发生了什么）：

 	1. 当我们发起变基时，git会首先找到两条分支的最近的共同祖先
 	2. 对比当前分支相对于祖先的历史提交，并且将它们提取出来存储到一个临时文件中
 	3. 将当前部分指向目标的基底
 	4. 以当前基底开始，重新执行历史操做

变基和merge对于合并分支来说最终的结果是一样的，但是变基会使得代码的提交记录更整洁清晰， 注意：大部分情况下合并和变基是可以互换的，但是如果分支已经提交给了远程仓库，那么这时最好不要使用变基。

 ### 远程仓库（remote）

目前我对于git的所有操作都是在本地进行的。在开发中显然是不够的，这时我们就需要一个远程的git仓库。远程的git仓库和本地本质没什么区别，不同点在于远程仓库可以被多人同时访问使用，方便我们协同开发。在实际工作中，git的服务器通常由公司搭建内部使用或是购买一些公共的私有git仓库，我们学习阶段，直接使用一些开放的公共git仓库，目前我们常用的库有两个：Github和Gitee（码云）

将本地库上传git: 

```bash
git remote add origin https://github.com/yiwangxi-1/test1.git
# git remote add <remote name> <url>
git branch -M main	# 修改分支为main
git push -u origin main
```

