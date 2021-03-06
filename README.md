# GIT小白篇
网络上很多教程虽然已经写得很简单了，很通俗易懂了，但是对于小白来说，看到那些分支树还有复杂的本地版本库，远程版本库，各种花式回滚还是比较惧怕的，所有就出了这篇按部就班式的教程。使用git从分支，到开发，再到上线就这几个步骤。假如一切顺利的话，期间不出现冲突，回滚，整个git开发就是下文所描述的。
## 开始篇
### 创建/提交/切换/删除分支
场景：团队有一个优化项目，需要采用分支开发，首先就是为项目创建一个分支，分支名称我们采用optimize

`创建分支`
```
git checkout -b optimize
```

场景：为了使得你的团队小伙伴都能看到这个分支，你需要提交刚才创建的分支

`提交分支`
```
git push origin optimize
```

场景：leader邀请新来的你，加入优化项目，你得切到optimize分支查看编辑代码

`切换分支`
```
git checkout optimize
```

场景：项目上线完成后，可以删除分支

`删除分支`
```
git branch -d optimize
```

## 工作篇
场景：自己需要在optimize项目中新增或者修改代码

1. 首先切换到optimize分支
```
git checkout optimize
```
2. 拉取最新的optimize分支代码
```
git pull origin optimize
```
每天工作前，必须要先把小伙伴的更新拉取下来，保证自己是在最新的版本上更改的。这两部做完之后就可以在项目中修改或者新增文件了。

场景：我们在optimize修改了代码，养成一个良好的习惯，每天提交自己修改的代码

1. 查看修改了哪些文件
```
git status
```
这一步要确认modified（红色字样）的文件都是你自己修改的文件，假设这一步显示修改的文件是`list.php`

2. 查看修改了哪些内容
```
git diff
```
这个命令后面也可以带上文件路径查看单独的文件diff内容，这一步确保你修改的没有问题，是可以提交的

3. 执行git add操作
```
git add list.php
```
多个文件时使用空格隔开，执行完之后，再次执行`git status`查看状态，这个时候查看modified编程了绿色字样

4. 提交文件
```
git commit -m "提交修改" list.php
```
同样多个文件使用空格隔开，至此，文件修改提交完毕。需要注意的是，这种commit操作提交的是git本地代码库，不会修改线上代码库，就是说你提交的别人更新不下来。

5. 提交到远程代码库
```
git push origin optimize
```
这个时候，你提交的东西就在远程代码库了，别人就可以更新到你修改的东西。你可以周而复始地进行上面5个步骤，然后每天都提交自己的工作量

## 上线篇
我们刚才所在的是optimize分支，这个分支是我们自己建立的，上线人员可不认识这个分支。上线分支没有特殊情况的话就是master分支。

场景：QA在optimize分支上测试功完毕，需要上线optimize分支的代码

1. 把当前分支切到master
```
git checkout master
```

2. 在当前master分支上合并optimize分支
```
git merge optimize
```
合并之后，你自己本地能看到master主干上代码的修改，但是远程master主干代码库没有没有同步修改。

3. 将代码push到远程master主干代码库
```
git push origin master
```
这一步完成之后远程master代码库就能看到修改了。只要远程master主干代码更新了，我们就认为代码达到了可上线状态，接下来运维会把主干代码上线到每一台机器。

## 后续
只要代码设计好，每个人编写不同的模块，上面的命令几乎就是我们GIT开发项目的全部了。笔者在工作多年，用的90%都是上面的命令。剩下的难点在于理解GIT的工作原理，未完待续...
