# note about git

## git仓库（本地）
1、分两部分：工作区（在仓库根目录中除了.git文件夹的所有文件及文件夹）、版本库（.git文件夹）。

2、工作区 里就是当前版本的所有文件及文件夹，工作区也是一个版本。

3、版本库 分两部分：暂存区、各个分支

    暂存区：
    每次添加（$ git add ...）的内容都添加到暂存区；
    
    各个分支：
    提交（$ git commit -m "..."）的内容提交的当前分支里。
    
    版本库中有多个版本。


## 下载git（仅是Windows）
首先，从官网https://git-scm.com/downloads下载并安装git；

然后，在某一文件夹的空白处右键单击，找找Git Bash Here命令；

找到，说明安装成功；成功之后，进行一些设置

    $ git config --global user.name "Your Name"
    $ git config --global user.email "email@example.com"
    设置全局用户名和邮箱，这样所有的仓库都使用这个设置；
    
    $ git config user.name "Your Name"
    $ git config user.email "email@example.com"
    在去掉--global，并且在仓库根目录下，
    也可以为每个仓库设置各自的用户名和邮箱；
    
    $ git config --global user.name
    $ git config --global user.email
    查看全局设置的用户名和邮箱；
    
    $ git config --list
    查看所有设置。
    
    设置主要在本机用户主目录下的.gitconfig文件
    和仓库.git目录下的config文件里。


## 创建仓库
### 1、新建并进入一个空文件夹
    $ mkdir learngit
    新建一个空文件夹
    $ cd learngit
    切换到文件夹路径下
    $ pwd
    显示一下当前路径
### 2、初始化仓库
    $ git init
    初始化空文件夹为一个git仓库
    $ ls -ah
    显示仓库中的所有文件及文件夹
    $ ls
    显示仓库中的所有文件

## 管理仓库
### 1、添加文件到仓库中
    $ git add 文件名1 文件名2 ...
    添加一个或多个文件，这里的文件并非是新建的，而是刚刚更新的，包括新建的，
    也可以连续多次add，对于某个文件的每次更新都可以add一次，可以连续多次，在暂存区会合并；
    
    $ git commit -m "关于这次提交的简要说明"
    将上述添加的更新文件提交到仓库中，并注明简要的提交说明；
### 2、检查仓库当前状态
    $ git status
    查看仓库当前状态，从当前状态信息就可以看出是否有未添加和提交的已更新文件。
    可以知道刚刚更新的文件，未提交的文件等。
### 3、查看文件的更新
    $ git diff 文件名
    当不知道文件的更新内容，可以查看。
    
    $ cat 文件名
    查看文件的当前内容
### 4、查看历史记录
    $ git log
    查看历史操作记录。
    有添加、提交等信息。
    还有各个历史版本的id。
    
    HEAD指当前版本，HEAD^指上一个版本，HEAD^^指上上一个版本，...
    HEAD~100指上100个版本。
    
    $ git log --pretty=oneline
    使历史记录显示的紧凑型
    
    $ git reflog
    查看保存的历史记录，里面包含版本号，
    所以，要从老版本回到比较新的版本，就需要直到新版本的版本号。
### 5、版本回退
    $ git reset --hard 版本号
    版本号 可以是 HEAD... 或者 一个存在的版本id
### 6、撤销更新
    撤销工作区中的更新
    更新的文件还未添加到暂存区：
        可以更新文件到原来的版本，
        或者可以
        $ git checkout -- 文件名
            此文件还没有添加到暂存区过
            或者
            添加过，但又接着做了一些更新
            
            不管哪种，都
        把此文件回到最近一次add或commit时的状态。
    
    撤销暂存区中的更新
    更新的文件添加到暂存区了：
        $ git reset HEAD 文件名
        把暂存区中此文件的更新从暂存区撤到工作区，
        这时，仓库当前状态中此文件是有修改未添加提交的。

    只要是未commit的更新，都能挽回。
### 7、文件的删除与恢复
    删除文件
    $ rm 文件名
    在工作区中把此文件删了，如果此文件从未提交到版本库中，则无法恢复此文件。
    
    彻底从版本库中删除文件
    $ git rm 文件名
    $ git commit -m "..."
    这样就把此文件从当前最新版本中删除。
    
    恢复误删的文件（当前最新版本中还有此文件）
    $ git checkout -- 文件名
    只能恢复到最新版本。
   
## 管理分支
    分支就是一条条时间线（版本线）
    master是主分支
    还有其它很多分支（可以创建删除合并等）
    
    一个项目有一个master主分支，
    平时不要在master分支上工作，
    在另一个develop（自建的）分支工作，
    而且，每个成员都有自己的一个分支，
    每个成员都只在自己的分支上工作，
    然后，把自己的工作合并到develop分支上，
    最后，要发布时，再把develop分支合并到master分支上。
    
### 1、查看分支
    $ git branch
    查看所有分支，以列表列出；
    当前分支以*在分支前标出。
### 2、创建分支
    $ git branch 分支名
    （未证实的不确定理解）
    在当前分支的当前版本为起点，
    创建此分支。
### 3、切换分支
    $ git checkout 分支名
    或者
    $ git switch 分支名
    切换当前分支为此分支。
### 4、创建并切换分支
    $ git checkout -b 分支名
    或者
    $ git switch -c 分支名
    创建并切换当前分支为此分支。
### 5、合并分支
    $ git merge 分支名
    合并此分支到当前分支中。
    
    $ git merge --no-ff 分支名
    普通方式合并，即不使用fast forward模式合并
    
    $ git merge -m "..." 分支名
    添加合并简要说明
    
    具体怎么合并，以什么规则合并，待续...
### 6、删除分支
    $ git branch -d 分支名
    删除此分支。
    
    $ git branch -D 分支名
    强行删除一个没有被合并到其它分支的临时分支。
    
### 7、解决冲突
    合并分支可能会产生冲突，
    所以要解决冲突，避免出错误。
    即使两个分支有冲突，也能合并，
    合并后，冲突的地方会有特殊标记：
    Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，
    修改后再次添加提交即可。
    
    $ git log --graph --pretty=oneline --abbrev-commit
    可以查看分支合并的具体情况。
### 8、debug分支
    某一分支有bug，要修复，但当前又有工作在做，
    而且，无法及时完成，
    所以，需要暂存当前工作，去修复bug。
    
    在此分支使用命令
    $ git stash
    保存当前工作；
    切换到要修复bug的分支，
    创建并切换到临时分支issue-001，
    然后修复bug，
    添加提交修复；
    切换到原来要修复bug的分支，
    合并分支issue-001到此分支，
    删除分支issue-001；
    然后，切换到原来工作的分支，
    使用命令
    $ git stash list
    查看保存的工作进度列表，
    使用命令
    $ git stash apply stash@{0}
    恢复工作进度0，
    然后使用命令
    $ git stash drop 
    删除保存的工作进度，
    或者
    使用命令
    $ git stash pop
    加载并删除保存的最近一个工作进度。
    
    如果要在多个分支修复同一个bug：
    只需修复一个分支，其它的则可以复制一个提交到此分支即可，
    在修复好bug后的那次commit有个id（提交号），
    切换到其它分支，
    使用命令 
    $ git cherry-pick 提交号
    将此提交复制到此分支，自动产生一个提交，提交号是新的。

## 管理标签
    标签tag简单来说就是一次commit的一个小名，
    一个tag对应一个commit，这个commit在哪个分支就能在哪个分支查看此tag，
    tag是为了方便管理版本。
### 1、加标签
    为某一分支最新的commit（即默认的HEAD）打标签：
    $ git tag 标签名（要有规律）
    
    为某一分支的某一历史commit打标签（忘了打了）：
    先查看commit记录中那个commit的提交号
    $ git log --pretty=oneline --abbrev-commit
    然后
    $ git tag 标签名 提交号
    
    创建有说明的标签：
    $ git tag -a 标签名 -m 简要说明 提交号    
### 2、查看所有标签
    $ git tag
    按字母顺序列出所有标签
### 3、查看标签信息
    $ git show 标签名
    包含了commit的具体信息。
### 4、推送标签
    $ git push origin 标签名
    推送一个标签名
    
    $ git push origin --tags
    推送所有未推送的标签名
### 5、删除标签名
    $ git tag -d 标签名
    删除一个本地的标签名 
    
    $ git push origin :refs/tags/标签名
    删除一个远程仓库的标签名
    要删除远程的标签，需要先删除本地的标签。
    


#
# note about github

## 注册登陆并设置SSH密钥
    在https://github.com/官网注册账号，
    登陆，
    创建一个SSH密钥。
    
    创建SSH密钥：
    在本地用户目录下是否有.ssh文件夹，里面是否有id_rsa和id_rsa.pub文件；
    没有，则在git bash here输入
    $ ssh-keygen -t rsa -C "邮箱"
    然后，再次确认是否有那两个文件；
    有，则在GitHub账户的设置中创建SSH密钥，
    在Title设置一个密钥名，
    再把id_rsa.pub文件中的内容复制到Key里。
    
    id_rsa里面是私钥，id_rsa.pub里面是公钥。
    私钥不可泄漏。
    
    如果，想在多台主机使用一个GitHub账号的仓库，
    可以为每台主机在GitHub账号中创建SSH密钥。

## 关联本地与远程仓库
1、在GitHub账户上创建一个空仓库

2、在本地仓库git bash here输入

    $ git remote add origin git@github.com:GitHub账号名/空仓库名.git
    进行关联

3、将本地仓库首次推送到远程仓库

    $ git push -u origin master
    首次把本地仓库全部推送到远程仓库（首次加上-u）
    只是主分支
    
    $ git push origin master
    以后每次推送到远程，只是主分支
    
    $ git push origin 分支名
    推送某一分支
    
    先抓取，再推送。
    进行分支链接
    $ git branch --set-upstream-to=origin/某一分支名 某一分支名
    在某一分支下
    $ git pull
    然后，有冲突解决冲突，再提交，
    最后，push此分支。
    
4、克隆远程仓库创建本地仓库

    先在git bash here里cd到某一目录，
    再输入
    $ git clone 仓库地址
    这样就把远程仓库克隆到本地了。
    
    克隆远程仓库某一分支
    $ git clone -b 分支名 仓库地址
    ...
    





























