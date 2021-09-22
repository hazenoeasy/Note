# 创建管理库

git init 

把目录变成git可管理的仓库

git add  添加到仓库

git commit 提交到仓库

commit可以一次提交很多文件

# 时光穿梭

git status   掌握仓库状态 

显示  changes not staged for commit   
     change to be committed
git diff   显示差别

git log 查看提交历史

git reset --hard HEAD^ 返回上一个版本
git reset --hard HEAD^^ 返回上上一个版本

git reflog 记录每一次命令
```
$ git reflog
e475afc HEAD@{1}: reset: moving to HEAD^
1094adb (HEAD -> master) HEAD@{2}: commit: append GPL
e475afc HEAD@{3}: commit: add distributed
eaadf4e HEAD@{4}: commit (initial): wrote a readme file
```

工作区   本地电脑环境

版本库  .git

add 加到暂存区

git commit 把暂存区加到分支

git checkout -- readme.text   把readme文件在工作区修改全部撤销

若没有add  则撤销至版本库

若add后 又修改   则撤销至刚添加到暂存区的状态

git reset HEAD readmd.txt  把暂存区的修改撤销掉


git rm 删除文件 git commit

git remote add origin git@github.com:xxxx/xxx.git   进行关联

git push -u origin master 第一次


HEAD 指向 master master指向提交

当我们创建新的分支，例如dev时，Git新建了一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上

假如我们在dev上的工作完成了，就可以把dev合并到master上。Git怎么合并呢？最简单的方法，就是直接把master指向dev的当前提交，就完成了合并

git checkout -b /git switch -c name dev -b -c会创建新分支 并切换至新分支

git merge 合并指定分支到当前分支  

git switch 和 git checkout 一样 语义更好

git branch -d name 删除分支

git stash 把工作区储藏起来
```
git stash list
stash@{0}: WIP on dev: f52c633 add merge
```
git stash apply stash@{0}

git stash pop 删除缓存

git cherry-pick 4c805e2  把bug提交的修改‘复制’到当前分支，避免重复劳动

如果要丢弃一个没有被合并过的分支，可以通过git branch -D  name 强行删除。

推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送：

但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push：


git pull / git fetch

fetch doesnt change local file.

pull will make local file up to date.

