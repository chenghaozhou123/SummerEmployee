git 操作

git add . 添加修改 git reset xx 取消要提交的变更

git status 查看修改情况

尚未暂存以备提交的变更

**git暂存要提交的变更**

git add file

git restore --stage file  取消暂存

**git提交到本地仓库**

git commit -m description // -m 后接此次提交的描述

如果此次提交需要撤销：

1、回滚代码

git log --pretty=oneline

git reset --hard commit_id  // 这时会回滚到commit_id的版本，一定要将现有的代码做好备份，否则回滚之后这些变动都会消失，比如我有个文件新传上去，那么回滚后就没了。

**git如何拉取历史版本**

git log --pretty=oneline

git checkout ID



**分支**

git branch //查看分支，前面带*为当前分支

git branch name //创建分支

git checkout name // 切换分支

git branch -d name // 删除分支，合并完后，分支没啥用了就可以删除

git push origin --delete name // 本地删除分支后，在远程仓库中删除

git push  <remote><localbranch>:<remotebranch> //将本地分支推送到远程仓库分支，如果remotebrach没有则会创建

**合并 merge**

现在有两个分支，master和test_branch，假设当前分支位于master

git fetch // 这将更新git remote 中所有的远程repo 所包含分支的最新commit-id, 将其记录到.git/FETCH_HEAD文件中。FETCH_HEAD： 是一个版本链接，记录在本地的一个文件中，指向目前已经从远程仓库取下来的分支的末端版本。

git pull的运行过程：

git pull

首先，基于本地的FETCH_HEAD记录，比对本地的FETCH_HEAD记录与远程仓库的版本号，然后git fetch 获得当前指向的远程分支的后续版本的数据，然后再利用git merge将其与本地的当前分支合并。

git pull 后不加参数的时候，跟git push 一样，默认就是git pull origin 当前分支名，当然远程仓库没有跟本地当前分支名一样的分支的话，肯定会报错。
本地master分支执行git pull的时候，其实就是git pull origin master。

拆解git pull

git pull操作其实是git fetch 与 git merge 两个命令的集合。
git pull 等效于先执行 git fetch origin 当前分支名, 再执行 git merge FETCH_HEAD，也就是说把当前版本和远程版本进行合并。

通过上述分析，可以知道，如果要合并代码就并不一定要用git merge命令了，也可以用git pull命名，比如要把远程origin仓库的xx分支合并到本地的yy分支，可以有如下两种做法。

第一种，传统标准的做法：
git fetch origin 目标分支名 // fetch到远程仓库目标分支的最新commit记录到 ./git/FETCH_HEAD文件中
git checkout 要被合并的分支名 // 切换到要合并的分支
git merge FETCH_HEAD // 将目标分支最新的commit记录合并到当前分支

举例说明：将远程origin仓库的xx分支合并到本地的yy分支。
git fetch origin xx
git checkout yy
git merge FETCH_HEAD
完成。

第二种，直接使用pull命令，将远程仓库的目标分支合并到本地的分支：
git pull <remoterepo_name> <branch_name> 

举例说明：将远程origin仓库的xx分支合并到本地的yy分支

git checkout yy

git pull origin xx



git merge work_company 部分冲突后我准备去work_company做一下push的，然后报错需要解决当前索引的冲突，使用git reset --hard回到之前的版本

token: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