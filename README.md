# GIT

# https://blog.csdn.net/u013288190/article/details/52740610  参考网址

　　Git基本常用命令如下：
　　mkdir：         XX (创建一个空目录 XX指目录名)
　　pwd：          显示当前目录的路径。
　　git init          把当前的目录变成可以管理的git仓库，生成隐藏.git文件。
　　git add XX       把xx文件添加到暂存区去。
　　git commit –m “XX”  提交文件 –m 后面的是注释。
　　git status        查看仓库状态
　　git diff  XX      查看XX文件修改了那些内容
　　git log          查看历史记录
　　git reset  --hard HEAD^ 或者 git reset  --hard HEAD~ 回退到上一个版本
　　(如果想回退到100个版本，使用git reset –hard HEAD~100 )
　　cat XX         查看XX文件内容
　　git reflog       查看历史记录的版本号id
　　git checkout -- XX  把XX文件在工作区的修改全部撤销。
　　git rm XX          删除XX文件
　　git remote add origin https://github.com/tugenhua0707/testgit 关联一个远程库
　　git push –u(第一次要用-u 以后不需要) origin master 把当前master分支推送到远程库
　　git clone https://github.com/tugenhua0707/testgit  从远程库中克隆
　　git checkout –b dev  创建dev分支 并切换到dev分支上
　　git branch  查看当前所有的分支
　　git checkout master 切换回master分支
　　git merge dev    在当前的分支上合并dev分支
　　git branch –d dev 删除dev分支
　　git branch name  创建分支
　　git stash 把当前的工作隐藏起来 等以后恢复现场后继续工作
　　git stash list 查看所有被隐藏的文件列表
　　git stash apply 恢复被隐藏的文件，但是内容不删除
　　git stash drop 删除文件
　　git stash pop 恢复文件的同时 也删除文件
　　git remote 查看远程库的信息
　　git remote –v 查看远程库的详细信息
　　git push origin master  Git会把master分支推送到远程库对应的远程分支上




git命令（自己总结）

git clone github地址 例如： git clone https://github.com/tugenhua0707/testgit.git

git checkout dev/sun          切换分支

git checkout -b dev/sun      创建并切换分支 （感觉不好用，直接在github或者gitlab网站内手动创建）

git branch    查看所有分支，当前分支前边会有*号 （课程创建的仅仅是一个本地的分支在github上看不见）

git branch –d name     删除分支

git status        查看修改文件,查看当前分支（即使git add . 提交到暂存区 但是 git status 还是能看到修改的文件列表）

git diff         查看修改前修改后文件修改详细内容

cat readme.txt      查看readme.txt文件内容

git add .        添加到暂存区

git commit -m '提交日志说明'      把暂存区的内容提交到当前分支

git push origin dev/sun         推到仓库

git log --oneline        查看日志（查看git log中，一直出现冒号： ，   如果想要退出，那么就需要使用命令字符 q）
git log --graph --oneline --abbrev-commit            详细查看日志（被删除的分支信息还在）

git merge dev   当前分支master，可以合并dev分支到master上

查看分支：git branch
创建分支：git branch name      
切换分支：git checkout name
创建+切换分支：git checkout –b name
合并某分支到当前分支：git merge name
删除分支：git branch –d name


git stash     把当前工作现场隐藏起来



回退（commit以后的代码都可以回退）
git reset --hard head^         把当前的版本回退到上一个版本 （commit提交过版本）

git reset --hard head^^       要回退到上上个版本只需把HEAD^ 改成 HEAD^^ 以此类推

git reset  --hard HEAD~100        那如果要回退到前100个版本的话，使用上面的方法肯定不方便，我们可以使用 head~100 命令操作

回退到最新的版本
描述： 提交三次  测试1  测试2 测试3  readme.txt     
111111 一次提交内容
22222  二次提交内容
33333  三次提交内容
执行  git reset --hard head^         把当前的版本回退到上一个版本   
 readme.txt     内容
111111 一次提交内容
22222  二次提交内容

如果现在想要回退到最新版本，有33333内容，git reset  --hard 版本号 ，但是现在的问题假如我已经关掉过一次命令行或者333内容的版本号我并不知道呢？要如何知道增加3333内容的版本号呢？可以通过如下命令即可获取到版本号：git reflog

git reflog


通过上面的显示我们可以知道，增加内容3333的版本号是 6fcfc89.我们现在可以命令
　　git reset  --hard 6fcfc89来恢复了。演示如下：

　　可以看到 目前已经是最新的版本了。 




git撤销修改和删除文件操作（commit以前的代码都可以撤销修改）
commit 以后   git log --oneline 里边就会多一条 commit 提交的记录
第一：如果我知道要删掉那些内容的话，直接手动更改去掉那些需要的文件，然后add添加到暂存区，最后commit掉。
第二：我可以按以前的方法直接恢复到上一个版本。使用 git reset  --hard HEAD^

第三种：直接使用撤销命令（推荐）
git checkout -- file   例如：git checkout -- readme.txt     工作区做的修改全部撤销（但是放到暂存区的内容不能修改）


撤销命令分两种情况：
readme.txt自动修改后，还没有放到暂存区，使用 撤销修改就回到和版本库一模一样的状态。
另外一种是readme.txt已经放入暂存区了，接着又作了修改，撤销修改就回到添加暂存区后的状态。（暂存区的内容通过撤销命令无法修改）

注意：命令git checkout -- readme.txt 中的 -- 很重要，如果没有 -- 的话，那么命令变成创建分支了。


删除文件
rm file  例如 rm src/pages/login/1.txt
删除文件只要在commit之前都可以通过 
git checkout -- src/pages/login/1.txt   恢复1.txt



GitHub创建仓库-关联到本地文件夹
git remote add origin https://github.com/tugenhua0707/testgit.git
把本地库的内容推送到远程，使用 git push命令，实际上是把当前分支master推送到远程。
git push -u origin master



git 合并分支
git checkout dev/sun   切换到dev/sun分支

修改文件1.txt 内容
原来内容： 
1111111
2222222
3333333
修改添加： 
4444444
cat 1.txt
当前dev/sun分支执行
git add .
git commit -m "添加444444"
git pull origin dev/sun
git push origin dev/sun
将当前代码提交到 dev/sun分支上

切换分支
git checkout master（非dev/sun分支）
查看1.txt还是原来的内容(cat 1.txt)，没有新添加的 444444，需要合并分支，把dev/sun内容合并到master上

原来内容： 
1111111
2222222
3333333

合并分支
git merge dev/sun 
git merge命令用于合并指定分支（dev/sun）到当前分支（master）上，合并后，再查看readme.txt内容，可以看到，和dev分支最新提交的是完全一样的。
cat readme.txt  -- 查看合并以后内容
注意到上面的Fast-forward信息，Git告诉我们，这次合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快。

执行一遍  add  commit  pull  push 才能在github上看到更新

合并分支（采用非fast-forward）
git merge  --no-ff -m "merge with no-ff"  待合并分支


删除分支
git checkout -d dev/sun     -d 删除         -b创建（感觉不好用，直接在github或者gitlab网站内手动创建）


总结创建与合并分支命令如下：
查看分支：git branch
创建分支：git branch name      
切换分支：git checkout name
创建+切换分支：git checkout –b name
合并某分支到当前分支：git merge name
删除分支：git branch –d name



bug分支(?试过几遍但是都不行drop,需要使用pop)
git stash 
git stash list 
git stash pop （list里边有几条记录执行几次 git stash pop）

项目开发过程中  （目前dev-sha分支），新开发或者修改部分内容，但是开发周期是7天，项目开发到一半，还未完成所以不能提交代码，但是原来开发好，已经上线项目，客户反馈有小bug，一天或者半天就可以修改完，需要先来修改bug，

当前分支（dev-sha） 
git status         查看状态，有修改内容的，不干净的

git stash           将当前的工作现场隐藏起来（一次不行，执行两次）

git status           查看状态，是干净的

切换分支到有bug的分支上，创建新分支 issue-404
git checkout -b issue-404        在master分支上创建临时分支issue-404

cat readme.txt           未修改前查看readme.txt 内容（假设就是readme.txt内容存在bug）

编辑器修改 readme.txt内容，改成没有bug状态

cat readme.txt            修改后查看readme.txt内容

git add readme.txt         提交readme.txt修改到 issue-404暂存区

git commit -m 'fix bug 404'

修复完成以后，切换到master分支上，并完成合并，最后删除 issue-404分支

git checkout master             切换分支

当前 属于master 分支
git  merge --no-ff -m 'nerge bug fix 404' issue-404          合并分支issue-404内容到master分支上

cat readme.txt        合并分支后查看内容，master分支和issue-404内容一致

git branch -d issue-404                     在master分支上删除临时分支 issue-404

修改 master 分支上的bug完成，
现在回到 dev-sha分支上干活  

git  checkout  dev-sha                    从master分支切换到 dev分支上

git  status						查看工作区目前干净

我们的工作区是干净的，呢我们的工作现场去哪里？  
git stash list                       工作现场还在，只是把stash内容存在某个地方，可以恢复一下

可以使用如下2个方法：
git stash apply恢复，恢复后，stash内容并不删除，你需要使用命令git stash drop来删除。
另一种方式是使用git stash pop,恢复的同时把stash内容也删除了。（测试成功）

git stash pop                直到 git stash list 为空  

git  stash list          输入为空  就全部回来
 


删除git log --oneline 上的历史commit(主要就是在提交pull push之前，修改下commit 的日志 )
https://blog.csdn.net/aixiaoxiaoyu/article/details/78598815
当我们在本地仓库中提交了多次，在我们把本地提交push到公共仓库中之前，为了让提交记录更简洁明了，我们希望把如下分支B、C、D三个提交记录合并为一个完整的提交，然后再push到公共仓库。



方法二： git rebase 用来合并提交到 远程端的文件pull push之前，commit之后的文件，将多条commit提交合并一条
git rebase -i head~4   (版本号)

进入 
pick-----
pick----- 
pick----- 
pick----- 

点键盘i进入vi模式，
修改除第一个保留pick 其他的pick修改为s,   
esc退出 vi模式,
shift + ;   
 :wq!保存并退出

git  add .
git rebase --continue
git commit -m "注释"

git pull origin master 
git push origin master



pick：保留该commit（缩写:p）
reword：保留该commit，但我需要修改该commit的注释（缩写:r）
edit：保留该commit, 但我要停下来修改该提交(不仅仅修改注释)（缩写:e）
squash：将该commit和前一个commit合并（缩写:s）
fixup：将该commit和前一个commit合并，但我不要保留该提交的注释信息（缩写:f）
exec：执行shell命令（缩写:x）
drop：我要丢弃该commit（缩写:d）


将某一段commit粘贴到另一个分支上
git rebase 
https://www.jianshu.com/p/4a8f4af4e803





将远程端无用的commit提交删除
方法一：
https://segmentfault.com/q/1010000002898735
git reset --hard head~1

git push --force

方法二：
leftstick的回答挺清晰了，我想再补充一点：假如你只是想修改上次提交的代码，做一次更完美的commit，可以这样
（1）git reset commitId，(注：不要带--hard)到上个版本
（2）git stash，暂存修改
（3）git push --force, 强制push,远程的最新的一次commit被删除
（4）git stash pop，释放暂存的修改，开始修改代码
（5）git add . -> git commit -m "massage" -> git push

方法三：(推荐方式 比较好用)
https://blog.csdn.net/hanchao5272/article/details/79435730

git log 

git reset --soft  commitId       --soft 适合用来修改commit 注释信息
    --hard 适合用来删除commitId本条记录

git log          确认是否成功撤销

git push origin master –force                   强制提交当前版本号，以达到撤销版本号的目的


修改代码，重新提交和推送:
git add .                                            //修改代码，添加修改
git commit -m "删除或者修改最新一条记录"                       //重新提交
git pull origin master
git push origin master                                         //重新推送
注意：git reset --soft  commitId 
          如果上边 reset --soft 修改commit 本次修改代码 的注释  “删除或者修改最新一条记录” 会被推送到远程端 
          如果上边 reset --hard 强制删除commit 本次修改代码 的注释，直接在远程端就删除掉看不到  



