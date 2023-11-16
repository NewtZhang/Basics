## 1、创建版本库

`git init`：把这个目录变成Git可以管理的仓库

`ls -ah`：看到隐藏文件

`git add readme.txt`：添加文件到仓库

`git commit -m "wrote a readme file"`：把文件提交到仓库

## 2、时光机穿梭！

### 2.1、查看版本状态

`git status`：让我们时刻掌握仓库当前的状态

`git diff readme.txt`：查看difference

```git
$ git diff readme.txt 
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
Git is free software.
```

"ok"的仓库状态：

```git
$ git status
On branch master
nothing to commit, working tree clean
```

### 2.2、版本回退

`git log`：查看提交历史，显示从最近到最远的几个提交日志

如果嫌输出信息太多，看得眼花缭乱的，
可以试试加上`--pretty=oneline`参数

怎么启动！：)

首先，Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，
也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），
上一个版本就是`HEAD^`，上上一个版本就是HEAD^^，
当然往上100个版本写100个^比较容易数不过来，所以写成H`EAD~100`。

`git reset --hard HEAD^`：回退到上一个版本

回到上一个版本后，再想恢复到最新版本怎么办捏：

找到之前的commit id，然后`git reset --hard 2c4f71a2`，再回到最新版本

但是我们找不到之前的commit id，怎么办捏：

`git reflog`：查看命令历史，以便确定要回到未来的哪个版本

### 2.3、工作区和暂存区

工作区（Working Directory）：就是你在电脑里能看到的目录

版本库（Repository）：工作区有一个隐藏目录`.git`，这个不算工作区，
而是Git的版本库

Git的版本库里存了很多东西，
其中最重要的就是称为`stage`（或者叫`index`）的暂存区，
还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

`git add`实际上就是把要提交的所有修改放到暂存区（Stage），
然后，执行`git commit`就可以一次性把暂存区的所有修改提交到分支。

### 2.4、管理修改

Git跟踪并管理的是修改，而非文件。

当你用git add命令后，在工作区的第一次修改被放入暂存区，
准备提交，但是，在工作区的第二次修改并没有放入暂存区，
所以，git commit只负责把暂存区的修改提交了，
也就是第一次的修改被提交了，第二次的修改不会被提交。

提交后，用`git diff HEAD -- readme.txt`
命令可以查看工作区和版本库里面最新版本的区别：

每次修改，如果不用git add到暂存区，那就不会加入到commit中

