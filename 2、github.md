![1643439770248](img\git.jpg)

# 一、push

git push 远程主机名  本质分支名  远程分支名

如：

## 1、git push origin master:refs/for/master

origin是远程主机名    本地分支名是master   远程分支名是refs/for/master

## 2、git push origin

当前分支名与远程分支存在追踪关系，则本地分支和远程分支都可以省略

## 3、git push origin refs/for/master

省略了本地分支名，则表示删除远程分支名

## 4、git push

如果当前分支只有一个远程分支，那么主机名、本地分支名、远程分支名都可以省略

## 5、

# 



# 二、分支

## 1、创建分支

git branch test: 基于当前commit创建test分支。.git/HEAD 文件中记录了当前分支名字。

## 2、删除分支

git branch -d test：删除本地test分支

git branch -D test： test分支还没有合入当前分支，所以要用-D参数才能删掉。

git push origin --delete test 删除远程test分支

git push origin :test 删除远程test分支

## 3、查看分支

 git branch 列出当前分支清单

git branch -a 查看远程分支和本地分支

git branch -v 查看各个分支最后一个提交信息

git branch --merged 查看哪些分支已经合并入当前分支

## 4、拉取分支 

git fetch origin 同步远程服务器的数据到本地

git checkout -b test origin/test_remote 将远程分支test_remote拉取下来到本地test分支

<p style="color:red">git checkout test 将远程分支test拉取下来到本地test分支</p>

<p style="color:red">git pull test从远程分支test 中checkout下来的本地分支test成为跟踪分支，使用git pull或者git push就会操作到对应的远程分支test</p>



## 5、切换分支

git checkout test

切换到test分支



## 6、合并分支

git merge A：把A分支合并到当前分支，若合并有冲突，需要解决冲突，android studio下使用右键项目工程，Git ->Resolve Conflict来解决冲突，解决冲突后，可能需要重新commit ，再push，此处切记不要直接push

## 7、git checkout -b newBrach origin/master

在`origin/master`的基础上，创建一个新分支。

## 8、更改分支名称

git branch -m 旧分支名称   新分支名称







# 三、Add

## 1、git add .

 不加参数默认为将修改操作的文件和未跟踪新添加的文件添加到git系统的暂存区，注意不包括删除

## 2、git add -u .

 -u 表示将已跟踪文件中的修改和删除的文件添加到暂存区，不包括新增加的文件，注意这些被删除的文件被加入到暂存区再被提交并推送到服务器的版本库之后这个文件就会从git系统中消失了。

## 3、git add -A .

 -A 表示将所有的已跟踪的文件的修改与删除和新增的未跟踪的文件都添加到暂存区。









# 四、remote

## 1、git remote －v 

查看远程地址

## 2、git remote rm origin 

删除远程origin 

## 3、git remote add pb git://github.com/paulboone/ticgit.git

添加主机名pb、添加远程仓库

## 4、git remote show 主机名

查看当前仓库基本信息

## 5、git remote

列出所有远程主机

## 6、git remote rm

删除远程主机

## 7、git remote rename

远程主机重命名







# 五、fetch  拉取

一旦远程主机的版本库有了更新（Git术语叫做commit），需要将这些更新取回本地，这时就要用到`git fetch`命令





# 六、tag

## 1、git tag  标签名

创建本地tag

## 2、git push origin 标签名

推送到远程仓库

## 3、git push origin --tags

将所有未推送的本地标签推送到本地仓库

## 4、git show 标签名

查看某个标签详细信息

## 5、git tag  或git tag -l

查看本地所有tag

## 6、git ls-remote --tags origin

查看远程所有tag

## 7、git tag -d 标签名

删除本地tag

## 8、git push origin:refs/tags/标签名

远程删除tag

## 9、git checkout  标签名

切换标签，此处和branch相同，切换标签之后需要进行pull



# 七、历史

## 1、git log

查看历史提交记录

## 2、git log --oneline 

查看历史记录的简洁的版本

## 3、git log--graph 

查看历史中什么时候出现了分支、合并。以下为相同的命令，开启了拓扑图选项

## 4、git log **--reverse** 

参数来逆向显示所有日志

## 





# 八、merge



https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6



## get merge 分支A，就是把分支A的代码合并到当前分支上，当前分支通常省略

把A分支合并到B分支上

1、git checkout B分支

2、git pull   拉下代码

3、git merge A    把A分支合并到当前分支【当前分支就是B分支，上面pull的】

4、再使用git push



主要用从一个分支合并到另一个分支

![1642386818781](img\1642386818781.png)

举例：

把优惠券 合到  0224分支上

220113_free_coupon         先(日期在前)

Release/release_22-02-24  后(日期在后)

因为220113_free_coupon   验收过了，应该把220113_free_coupon 的代码合到0224上去，是往住分支上和


所以命令是git merge 220113_free_coupon  把220113_free_coupon合并到当前分支(0224)







## 3、git blame 文件名

以列表形式查看指定文件的历史修改记录









# 九、常用操作

## 1、从已有远程分支上建立一个新的本地分支，修改收再推上去

拉取一个分支，git checkout  远程分支名

同步拉取的分支代码， git pull

在已有分支上建立一个新的分支，git checkout -b 分支名

修改完代码后，再提交   git push，如果本地分支与远程分支不存在关联，则需要

 git push --set-upstream origin 分支名

![1645427613707](img\1645427613707.png)

## 2、向远程分支上push了一个错的分支，要撤回【暂时不行】

git reset --hard commit序列号

git push

## 3、拉取commit，世界使用工具拉即可，as提供的工具或者直接checkout commit号



## 4、git撤销已提交的commit【未实战测试】

1、撤销本次提交：git reset --soft HEAD^
2、如果需要连add的文件也一并撤销，使用命令：git reset --hard HEAD^
命令解释：

HEAD^ 表示上一个版本，即上一次的commit，也可以写成HEAD~1 如果进行两次的commit，想要都撤回，可以使用HEAD~2
–soft 不删除工作空间的改动代码 ，撤销commit，不撤销git add file
–hard 删除工作空间的改动代码，   撤销commit且撤销add的文件
3、修改commit的message：git commit --amend   执行后会进入vim编辑器，使用Insert键进行编辑，完成后输入:wq进行保存









删除本地文件后，想从远程仓库中重新新Pull最新代码，但是执行了git pull命令后始终无法拉取下来
提示 Already up-to-date.
原因：当前本地库处于另一个分支中，需将本分支发Head重置至develop
git 强行pull并覆盖本地文件(依次执行)

git fetch --all
git reset --hard origin/master(master可修改为对应分支名)
git pull



## 

# 十、stash缓存

https://jingyan.baidu.com/article/7e44095386e1a06fc1e2ef33.html

1.然后，使用指令git stash 将文件修改缓存。这时候可以切换到其它分支干别的了，或者

2.使用git status指令确认当前分支没有修改内容。  

3.使用指令git stash list，查看当前缓存列表。

4.使用指令git stash apply stash@{id}，恢复指令ID的缓存内容，并且保留缓存条目。

6.使用git stash pop 恢复最新的stash，同时删除恢复的缓存条目。



【stash用上面的这个方法就行，亲测有效】



git stash clear  :注意这是清空所有stash

git stash drop stash@{0}  这是删除第一个队列

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

git pull会把本地未提交修改覆盖，处理的方式非常简单，主要是使用git stash命令进行处理，分成以下几个步骤进行处理。【注意本地分支和远程分支需要处于同步状态】
1、git stash       先将本地修改存储起来，这样本地的所有修改就都被暂时存储起来 。是用git stash list可以看到保存的信息，其中stash@{0}就是刚才保存的标记。
2、git  pull内容，暂存了本地修改之后，就可以pull了，pull后本地的代码就和远程对应分支代码一样了
3、还原暂存的内容
$ git stash pop stash@{0}
系统提示如下类似的信息：
Auto-merging c/environ.c
CONFLICT (content): Merge conflict in c/environ.c
意思就是系统自动合并修改的内容，但是其中有冲突，需要解决其中的冲突。

4、可以再对代码进行编辑后，再进行push等操作

4、解决文件中冲突的的部分
打开冲突的文件，会看到类似如下的内容：
git冲突内容
其中Updated upstream 和=====之间的内容就是pull下来的内容，====和stashed changes之间的内容就是本地修改的内容。碰到这种情况，git也不知道哪行内容是需要的，所以要自行确定需要的内容。
解决完成之后，就可以正常的提交了。





1）**git stash save "备注信息"** : 存放时添加备注便于查找；当然只执行`git stash` 也可以，系统会自动为我们添加备注，但不便于查找

2）**git stash list** : 查看存放列表

3）**git stash show** : 显示改动信息，默认展示第一个存储,如果要显示其它存储，后面加stash@{index}，比如第二个 git stash show stash@{1}

4）**git stash show -p** : 显示第一个存储的改动，如果想显示其它存储，`git stash show stash@{index} -p` ，比如第二个：git stash show  stash@{1} -p

5）**git stash pop** : 恢复之前存储的工作目录，将缓存堆栈中的对应stash删除，并将对应修改应用到当前的工作目录下,默认为第一个stash,即stash@{0}，如果要应用并删除其他stash，命令：git stash pop stash@{$num} ，比如应用并删除第二个：git stash pop stash@{1}

6）**git stash apply** : 应用某个存储,但其不会从存储列表中删除，默认使用第一个存储,即stash@{0}，如果要使用其他个，git stash apply stash@{index} ， 比如第二个：git stash apply stash@{1} 

> `git stash pop` 与 `git stash apply`的区别：前者应用后会将其从存储列表中删除，而后者则不会

7）**git stash drop stash@{index}** : 丢弃stash@{index}存储，从列表中删除某个存储

8）**git stash clear** : 清除存储列表中的所有stash















十一、git  tag

tag是git版本库的一个标记，指向某个[commit](https://so.csdn.net/so/search?q=commit&spm=1001.2101.3001.7020)的指针。

tag主要用于发布版本的管理，一个版本发布之后，我们可以为git打上 v.1.0.1 v.1.0.2 ...这样的标签。

tag感觉跟branch有点相似，但是本质上和分工上是不同的：

tag 对应某次commit, 是一个点，是不可移动的。
branch 对应一系列commit，是很多点连成的一根线，有一个HEAD 指针，是可以依靠 HEAD 指针移动的。
所以，两者的区别决定了使用方式，改动代码用 branch ,不改动只查看用 tag。
tag 和 branch 的相互配合使用，有时候起到非常方便的效果，例如：已经发布了 v1.0 v2.0 v3.0 三个版本，这个时候，我突然想不改现有代码的前提下，在 v2.0 的基础上加个新功能，作为 v4.0 发布。就可以检出 v2.0 的代码作为一个 branch ，然后作为开发分支。



1、创建本地tag标签                               git tag   tag名称   

2、将tag标签推送到远程仓库                git push origin     tag名称   

​      将所有tag标签推送到远程仓库        git push  origins  --tags 

以上是基于本地当前分支的最后的一个commit 创建的 tag ，但是如果不想以最后一个，只想以某一个特定的提交为tag ，也是可以的，只要你知道commit 的id。

git log --pretty=oneline //查看当前分支的提交历史 里面包含 commit id

git tag -a   标签名称  commitID



3、查看本地的eTag信息       git  show tag名称

4、查看本地所有Tag             git  tag   或者git  tag  -l

5、查看远程所有Tag             git ls-remote --tags  origin

6、删除本地Tag                    git tag -d Tag名称

​      删除远程Tag                    git push origin :refs/tags/<tagName>

7、把本地Tag推到远程       git push origin :<tagName>

 ![1643440376219](img\1643440376219.png)











# 九、其它：

给android studio配置密码：https://www.jianshu.com/p/2746133378b9

git config --global credential.helper store

![1641777317312](img\1641777317312.png)











2、

