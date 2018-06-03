##创建版本库
* *创建一个空目录*

    *   **$ mkdir learngit**  
        **$ cd learngit**  
        **$ pwd**  
        **/Users/michael/learngit**
        * `pwd`命令用于显示当前目录。在我的Mac上，这个仓库位于/Users/michael/learngit
* *管理仓库*
    * **$ git init**  
        * `git init`命令把这个目录变成Git可以管理的仓库
* *文件添加到版本库*
    * 编写一个readme.txt保存放到learngit目录下  
    **$ git add readme.txt**
        * `git add`命令告诉Git，把文件添加到仓库
* *文件提交到仓库*
    * **$ git commit -m "wrote a readme file"**
        * `git commit`命令，-m后面输入的是本次提交的说明  
        `1 file changed`1个文件被改动  
        `2 insertions`文件插入了两行内容  
***

##版本回退
* *查看历史修改*
    *   **$ git log**  
        * `git log`命令查看历史修改记录  
        加上`-pretty=oneline`参数更加简明直接的查看历史  
        一大串类似`1094adb...`的是`commit id(版本号)`
* *退回之前版本*
    *   **$ git reset --hard HEAD^**  
        * `git reset`命令退回之前的版本  
        `HEAD`表示当前版本  `HEAD^`表示上一个版本`HEAD^^`表示上上一个版本
* *再复原之前的版本*
    * **$ git reset --hard 1094a**
        * `hard 1094a`是之前的那个版本的版本号
* *命令的记录*
    * **$ git reflog**
        * `git reflog`用来记录每一次命令
***
##工作区和暂存区
* *工作区*
    * **你在电脑里能看到的目录**
* *版本库*
    * **版本库里包含stage（或者叫index）的`暂存区`以及一个分支`master`以及指向master的一个指针叫`HEAD`**
        * 把文件向版本库中添加分两布：   
        `第一步是`用`git add`把文件添加进去，实际上就是把文件修改添加到`暂存区`；  
`第二步`是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到`当前分支`。
* *查看仓库状态*
    * **$ git status**
        * `git status`命令用于查看仓库中的文件的状态  
        `Untracked`表明文件未被`git add`到工作区
***

##管理修改
* *文件的两次修改的提交*
    * **第一次修改 -> `git add` -> 第二次修改 -> `git add` -> `git commit`**  
* *查看文件具体前后修改内容*
    * **git diff HEAD -- 文件名**
        * `git diff HEAD -- 文件名`命令可以查看工作区和版本库里面最新版本的区别
***
##撤销修改
* *丢弃工作区的修改*
    * **$ git checkout -- 文件名**  
        * `git checkout -- 文件名`命令意思就是，把文件在工作区的修改全部撤销  
        只适用于readme.txt自修改后`还没有被放到暂存区`
* *丢弃暂存区的修改*
    * **$ git reset HEAD 文件名**  
        * `git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本  
        现在`暂存区是干净的`，`工作区有修改`之后再`丢弃工作区的修改`
***

##删除文件
* *从工作区中删除文件*
    * **$ rm 文件名或者直接用文件管理器删除**  
* *从版本库中删除文件*
    * **$ git rm 文件名**  
      **$ git commit -m**
        * `git rm 文件名`命令用于删除已经添加到版本库的文件只适用于readme.txt自修改后`还没有被放到暂存区
* *在工作区误删文件*
    * **$ git checkout -- 文件名**
        * `git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”
***

##添加远程库
* *在Github创建一个新的仓库*
    * **第一步“Create a new repo”创建一个新的仓库**  
    **第二步在Repository name填入仓库名字，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库**
* *本地仓库的内容推送到GitHub仓库*
    * **第一步$ git remote add origin git@github.com:GitHub账户名/仓库名.git**  
    **第二步$ git push -u origin master** 
        * `origin`是远程库的名字，`git push`命令实际上是把`当前分支master`推送到远程  
        加上了`-u`参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令  
        此后，每次本地提交后就可以使用命令`git push origin master`推送最新修改
***

##从远程库克隆
* *在Github创建一个新的仓库*
    * **第一步“Create a new repo”创建一个新的仓库**  
    **第二步在Repository name填入仓库名字，`勾选Initialize this repository with a README`，这样GitHub会自动为我们创建一个`README.md`文件。创建完毕后，可以看到README.md文件**
* *远程库克隆到本地库*
    * **$ git clone git@github.com:michaelliao/gitskills.git**  
    **$ cd gitskills**  
    **$ ls**  
        * `git clone`命令用于将远程库克隆到本地库
***

##创建与合并分支
* *创建dev分支，然后切换到dev分支*
    * **$ git checkout -b dev**
        * `git checkou`t命令加上-b参数表示创建并切换
* *查看当前分支*
    * **$ git branch**  
        ** *dev**  
        **master**
        * `git branch`命令会列出所有分支，当前分支前面会标一个 * 号
* *合并分支*
    * **$ git checkout master**    
      **$ git merge dev** 
        * `dev分支`的`工作完成`，我们就可以`切换`回`master`分支  
        `git merge`命令用于合并指定分支到当前分支  
        `Fast-forward`信息,合并是`“快进模式”`，也就是`直接把master指向dev的当前提交`,并不是所有都是这种模式
* *删除分支*
    * **$ git branch -d dev**
    * 
***

##解决冲突
* *冲突发生的情况：在`两个不同的分支`都做了`不一样的修改`并且都`提交`*了,这种情况下，Git`无法`执行“`快速合并”`*    
*文件存在冲突，必须`手动解决冲突后`再提交。`git status`也可以告诉我们冲突的文件*  
    * **`直接查看`冲突文件的内容**  
    **Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出`不同分支`的内容**  
    **手动编辑为我们希望的内容，再提交** 
        * `$ git log --graph --pretty=oneline --abbrev-commit`可以看到分支的合并情况
***

##分支管理策略
* *禁用Fast forward*
    * **合并分支时用`Fast forward`模式，删除分支后，会`丢掉分支信息`**  
    **`强制禁用Fast forward模式`，Git就会在`merge`时生成一个`新的commit`，这样，从`分支历史`上就可以`看出分支信息`。**  
    **$ git merge --no-ff -m "merge with no-ff" dev**
        * `--no-ff参数`，表示`禁用Fast forward`  
           用`git log`看看分支历史，会发现有`合并的信息`
***

##Bug分支
* *隐藏工作区:有时候修改bug时，但是`分支工作没有完成不想提交时`来隐藏工作区*
    * **$ git stash**  
        * `stash`功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作,用`git status`查看工作区，就是干净的
* *查找隐藏的工作区*
    * **$ git stash list**  
        * `git stash list`命令用于查找对于那个分支做了工作区的隐藏
* *恢复隐藏的工作区*
    * **& git stash apply或者$ git stash pop**
        * `git stash apply`恢复，但是恢复后，`stash内容并不删除`，你需要用`git stash drop`来删除  
        `git stash pop`恢复的同时把stash内容也删了  
        恢复指定的stash，用命令`$ git stash apply stash@{0}`
***

##Feature分支
* *丢弃没有被合并过的分支*
    * **$ git branch -D feature-vulcan**  
        * `git branch -D <name>`用于强行删除一个没有被合并的分支
***

##多人协作
* *查看远程库的信息*
    * **$ git remote -v**  
        * `git remote -v`可以抓取和推送的origin的地址。如果没有推送权限，就看不到push的地址
* *推送分支*
    * **$ $ git push origin 分支名**  
        * `master`分支是主分支，因此要`时刻与远程同步`  
`dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与`远程同步`  
`bug`分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug  
`feature`分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发
* *抓取分支*
    * **`远程库clone`时，默认情况下只看到本地的master分支，要在dev分支上开发，就必须创建远程origin的dev分支到本地`$ git checkout -b dev origin/dev`**  
    **在dev上继续修改，然后，把dev分支`push`到远程**
* *两个人推送提交冲突*
    * **$ git pull**
        * `git pull`把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送  
        `git pull`失败了原因是没有指定`本地dev分支`与`远程origin/dev分支`的链接,用`$ git branch --set-upstream-to=origin/dev dev`就可以解决，再pull
***

##创建标签
* *创建标签*
    * **$ git tag tagname**  
        * `git tag <tagname>`命令用于新建一个标签，默认为`HE`AD，也可以指定一个`commit id`,命令为`$ git tag v0.9 commit id`
* *指定标签信息*
    * **$ git tag -a tagname -m “说明”**  
        * `git tag -a <tagname> -m "blablabla...`命令用于指定标签信息
* *查看标签*
    * **$ git tag**  
      **$ git show tagname**
        * `git tag`命令用来查看标签  
        `git show tagname`查看标签信息
***

##操作标签
* **命令git push origin tagname可以推送一个本地标签**

* **命令git push origin --tags可以推送全部未推送过的本地标签**

* **命令git tag -d tagname可以删除一个本地标签**

* **命令git push origin :refs/tags/tagname可以删除一个远程标签**





