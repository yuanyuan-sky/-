# Git #
1. 安装完后，在Git Bash中配置用户名和邮箱

		git config --global user.name "yuanyuan"
		git config --global user.email "943101128@qq.com"

		git config -l    //显示所有配置信息

1.  创建git本地仓库

		git init       //将当前文件夹初始化为git本地仓库
1. 将文件添加到缓存区

		git add 文件
1. 将缓存区的文件提交到本地仓库

		git commit -m "提交说明"
1. 修改后的文件已经添加到缓存区，怎么回退回去

		git reset HEAD 文件    //将缓存区的文件回退回去
		git checkout -- 文件   //清理缓存区
1. 已经提交到本地仓库，怎么回退到之前的版本

		git log       //显示之前每次提交的信息，可以获取每次提交的commit码 
		git reset --hard 某次commit的提交码     //回退到某次版本	
1. 删除所有版本

		1. 先删除本地文件
		2. git rm  文件
		3. git cimmit -m "提交说明"   //删除成功


### git status 命令   

		显示工作目录和暂存区的状态。可以看到哪些修改没有被添加到暂存区，那些暂存区的文件没有被提交到本地仓库。
		有3个状态
		1、Changes to be committed:在缓存区中，没有提交到本地仓库
		2、Untracked files ：这是项目中新加的文件，还没有添加到缓存区
		3、Changes not staged for commit:在之前已经提交的文件上进行了修改，但是没有添加到缓存区

1. 显示版本变更内容

		git diff HEAD^ HEAD 文件   //显示最新版本与上一个版本的变化
		HEAD^  上一个版本
		HEAD^^ 上两个版本
		
--------以上操作，都是对本地仓库的操作-------------------

# 把本地仓库上传到远程git仓库 #
1. 生成SSH
		
		打开Git Bash,输入下面的命令
		ssh-keygen -t rsa -b 4096 -C "注册github的邮箱"
		将生成的.pub文件的内容粘到github中生成SSH keys
		-----SSH生成一次就行了
1. 在github上新建仓库，并将本地仓库与远程github仓库关联起来

		在git bash，在本地仓库中，键入下面的命令
		git remote add origin https://github.com/yuanyuan-sky/ttt.git
										git仓库的地址
		//origin是连接名
1. 上传到远程仓库

		git push -u origin master 
		//上传到origin连接的master分支上（主分支）
		//如果想上传到连接的其它分支上，只需要将master改成相应分支名即可
		//git push -u origin new_branch    **远程仓库必须有new_branch这个分支
1. 以后修改的文件，上传到本地仓库，只需要使用 git push 命令即可

# 克隆远程仓库到本地 #
	
	Git Bash中，在本地想要clone的文件夹中，键入如下命令（该文件夹不能是git仓库）
	git clone 远程仓库地址
	
	后续在该仓库上的修改，只需要保存到本地仓库中，然后执行git push命令，即可上传到远程仓库中
# 标签管理 #
	
	1. git tag                         //查看所有标签
	2. git tag name                    //创建标签
	3. git tag -a name -m "comment"    //创建标签并给标签添加一个描述
	4. git tag -d name                 //删除本地标签
	5. git push origin name            //发布标签到远程仓库
	6. git push origin -d name         //删除远程仓库中的name标签

#分支
	
	1. git branch  //显示所有分支，当前所在的分支为绿色
	2. git branch name  //新建一个名为分支name的分支
	3. git checkout name   //切换到name分支
	4. 将分支内容进行add 、commit操作后，可以将其合并到主分支
	5. 切换到主分支
	6. git merge 要合并到主分支的分支名      //将分支合并带主分支中
	7. git branch -d 分支名        //删除分支

