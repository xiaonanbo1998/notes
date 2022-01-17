# 1.工具

- VSCode：主要负责前端大部分【**功能业务**】的开发，调试与管理
- HBuilderX：主要负责前端【**小程序**】的调试、安装与管理
- 微信开发者工具：主要负责【**微信小程序**】等其他小程序的调试
- git：版本管理工具，配合以上工具使用（可能需要相应的配置不同参数），以及从GItLab网站【**拉取、推送**】项目文件使用

# 2.网址

- 禅道（[欢迎使用禅道集成运行环境！ (med-value.com)](http://wiki.med-value.com:8012/)）：项目任务的【**分配与管理**】
- GitLab（[Projects · Dashboard · GitLab (med-value.com)](http://git.med-value.com/)）：项目代码的【**存放仓库**】
- 蓝湖（[蓝湖 (lanhuapp.com)](https://lanhuapp.com/web/#/item)）：项目的【业务流程示意图】与项目界面的【**设计图**】

# 3.git常用指令

- git clone git@url：【**克隆**】项目到当前文件夹
- git checkout dev：【**切换**】到【dev分支】
- git checkout -b branchName：【**创建分支**】并【**切换**】到自己需要创建的分支上
- yarn：【**安装**】当前项目的依赖（每次克隆项目都需要安装依赖）
- git add .：【**添加**】【**本地修改**】到暂存区
- git commit -m 'modified content'：【**提交**】已添加的修改到【**本地仓库**】的【**当前分支**】，并添加日志，内容为【**modified content**】
- git pull origin branchName：【**拉取**】远端仓库对应仓库下【**对应分支**】的【**最新分支代码**】
- git rebase branchName：将【**branchName分支**】的代码【**合并**】到【**当前分支**】上，并手动进行【**冲突解决**】（详情自行查阅）
- git push origin branchName：【**推送**】远端仓库对应仓库下【**对应分支**】的【**本地代码**】
- 打开浏览器，访问【http://git.med-value.com/【**账户名**】/【**项目名**】/merge_requests】，提交【**New merge request**】
- 其他
  - git branch：查看分支
  - git checkout branchName：切换分支
  - git init：创建/初始化当前文件夹为仓库
  - git log：查看历史版本等信息
  - ...

# 4.指令详解

- git diff

  ```git
  git diff <branch1> <branch2>	# 比较两个分支差异，前旧后新
  git diff HEAD	# 查看工作区和HEAD的差别
  git diff test	# 查看工作区和另一个分支test的差别
  git diff --stat	# 查看简单的diff结果
  ```

- git log

  ```git
  git log --no-merges		# 显示整个提交历史记录，跳过合并
  git log -3				# 显示最近3次提交
  git log --pretty=oneline	# 按指定格式显示日志信息
  ```

- git reset

  ```git
  git reset HEAD <file>	# 回退添加暂存区的文件
  git reset --hard HEAD~1	# 回退一个版本，清除本地仓库的一次提交
  git reset --hard		# 回滚pull操作,清除暂存区/索引区的混乱
  ```

- git rebase

  ```git
  git rebase <branch>		# 将branch分支，合并到当前分支
  git add .				# 解决冲突后，添加到暂存区
  git rebase --continue	# 继续合并，即应用剩下的补丁
  git rebase --abort		# 终止合并，退回开始状态
  ```

- git commit

  ```git
  git commit -a	# 查看本地仓库的历史提交
  ```

- git branch

  ```git
  git branch				# 查看分支
  git branch -a			# 查看本地和远程分支
  git branch <branch>		# 创建分支
  git checkout <branch>	# 切换分支
  git checkout -b <branch>			# 创建分支，切换分支的合并简写
  git branch -m <oldname> <newname>	# 修改分支名称
  git branch --delete <branch>		# 删除本地分支，该分支必须和关联分支或者HEAD同步
  简写	git branch -d <branch>
  git branch --delete --force <branch>	# 删除本地分支，不检查合并/merge
  简写	git branch -D <branch>
  git push origin --delete <branch>	# 删除远程和追踪分支
  git fetch origin <branch1>:<branch2>	# 拉取远端branch1分支，合并到本地新建的branch2分支
  ```

  

- git push

  ```git
  git push <远程主机名> <本地分支名>:<远程分支名>
  git push origin master	# 推送当前分支，到远端master分支，如果不存在，则新建
  git push origin HEAD	# 当前分支推送到远端同名分支，简写
  git push origin :master	# 省略本地分支名，则表示删除远端指定的分支
  # 等同于
  git push origin --delete master
  git push --force origin	master	# 覆盖式的推送
  git push -u origin master	# 推送本地master分支到远端，同时指定一个默认主机，以后不用加参数使用 git push
  ```

- git pull

  ```git
  git pull <远程主机名> <远程分支名>:<本地分支名>
  git pull origin next:master	# 取回origin远端的next分支，与本地master分支合并
  git pull origin next	# 取回远端next分支，合并到当前分支
  ```

- 其他

  - 指定【master分支】，追踪【origin/next分支】
  
    ```shell
    git branch --set-upstream master origin/next
    ```
  
  - 【stash】相关指令
  
    ```shell
    git stash		#	将当前工作区更改，保存在堆栈中
    git stash list	#	查看已存在更改的列表
    git stash pop	#	从堆栈中删除更改，并将其放置在当前工作区
    git stash apply stash@{*}	#	从堆栈中应用某一项更改，且不删除
    git stash drop stash@{*}	#	从堆栈中移除更改
    git stash clear				#	清空堆栈
    ```
  
  - 【show】和【diff】相关指令
  
    ```shell
    git show	#	查看上次提交修改的内容
    git show 【log】	#	指定查看某次的提交修改的内容（首七位字符）
    git diff	#	查看当前本地修改的内容
    git diff 【log1】 【log2】	#	增加的是当前内容，删除的是上个版本内容
    ```
  
  - 解决乱码问题
  
    ```shell
    git config --global core.quotepath false			# 解决【git status】查看中文乱码的情况，因为默认情况下，中文显示为八进制的字符编码；除此之外，还要设置【git bash】终端的中文乱码情况，终端右键菜单中设置本地中文，以及字符编码为【UTF-8】
    ```
  
    > 参考： [(47条消息) git status 显示中文和解决中文乱码_夏虫不可语冰-CSDN博客_git status 中文乱码](https://blog.csdn.net/u012145252/article/details/81775362?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~default-1.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~CTRLIST~default-1.pc_relevant_default&utm_relevant_index=2) 
  
  - 其他
  
    ```shell
    git merge
    git fetch
    git remote add origin git@github.com:xiaonanbo1998/notes.git	#	添加远端仓库
    
    git update-index --assume-unchanged filename		#	忽略【已进行跟踪的文件】
    git update-index --no-assume-unchanged filename		#	恢复跟踪
    ```

# 5.参考网址

- npm指令

  ​	

  ```git
  npm install --registry=https://registry.npm.taobao.org			#	安装依赖，通过taobao镜像网址
  ```

- GitHub项目查找：[(29条消息) 三分钟教你如何用Github找开源项目--值得一看！_Z小旋-CSDN博客_github找项目](https://blog.csdn.net/as480133937/article/details/105611577)
