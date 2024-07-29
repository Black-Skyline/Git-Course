# Git

## 下载和安装

- 官网提供的安装程序链接：https://git-scm.com/download下载好安装程序之后根据需求本地安装即可
- 官网提供的其他下载方式参阅：[https://git-scm.com/book/zh/v2/起步-安装-Git](https://git-scm.com/book/zh/v2/起步-安装-Git)
  - 下载源码编译安装（如何你没有在Linux下交叉编译的经验，请不要选择这种方式，不然这会令你戴上痛苦面具），源码的仓库地址请参见上方的文档说明
  - 下载 GitHub Desktop程序（Windows、macOS系统有效）网址：https://desktop.github.com/download/

## 基本概念

1. ##### 简述一下Git

   >Git是一个免费开源的**分布式版本控制工具**，几乎所有的操作都是在本地进行，需要网络的操作仅仅是同步。
   >
   >基本的设计思想和原理就是在本地复制一个代码库，每次操作都是提交到自己的代码库中。
   >
   >简而言之，Git可以管理本地的代码仓库，并可以与远程(Remote)仓库进行简单的交互
   >
   >- 分布式：
   >
   > Git主要是在本地进行版本控制管理，每个人在本地都可以建立一个自己的仓库，进行文件更改等等操作，需要多人云端协作时再推到云端。为什么要这么做呢？我们可以先来看看**集中式**的版本控制是怎么样的。
   >
   > ![集中式版本控制.jpg](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/%E9%9B%86%E4%B8%AD%E5%BC%8F%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6.jpg)
   >
   > 版本控制交由中心服务器，本地文件更改后提交到服务器。但是如果中心服务器寄了以后，就容易受到损失，并且带来其他很多不利后果。
   >
   > 那如果是**分布式**呢？
   >
   > ![分布式版本控制.jpg](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/%E5%88%86%E5%B8%83%E5%BC%8F%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6.jpg)
   >
   > 每个本地的仓库都是独立的，可以拥有自己的版本变动体系，同时也可以使用一个中心服务器来实现云端多人协同开发。这样就可以避免了许多集中式版本控制的方案带来的问题。
   >
   >- 版本控制：Git会帮助我们追踪在何时何人更改了文件的哪些内容，这些“追踪的记录”的集合可以使文件从一个版本变更到另一个版本。我们可以利用Git对这些不同的版本进行管理和控制。

2. ##### 为什么要使用Git？

   > 1. 对文件进行版本控制，方便进行版本的迭代、回滚，以及分支的合并等操作。
   >
   >    想象一下，假如我们没有对版本进行控制的工具，会是一个怎样的情景？
   >
   >    ![1689823422327.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1689823422327.png)
   >
   >    这种手动进行版本控制的方式在文件数量激增时，出现问题的概率会大大提高，同时管理效率会显得捉襟见肘。
   >
   >    因此，我们需要一种便捷且有效的方式来完成不同版本的切换与访问。
   >
   > 2. 方便进行多人的协同工作。
   >
   >    当我们需要多人协同开发时，若同一文件内容在同一版本时间段被多人修改，然后进行版本合并就会发生版本冲突，而Git提供了有效的在本地解决版本冲突的功能，可以让我们更加方便的把自己开发的版本与别人开发的版本进行合并，或是基于其他人的版本继续开发新的内容。（在出事故的时候还可以**精准地找人背锅**）
   >
   >    ![1690373705592.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690373705592.png)
   
3. ##### GitHub、GitLab、Gitee和Git的关系？

   > 前三者其实就是后者的一个托管平台（可以作为本地仓库的远端来源），当我们本地建好Git仓库以后，就可以上传到平台进行托管，同时也可以让其他用户对平台上的代码进行进一步开发，利用平台进行多人协作开发。
   
4. ##### Git工作流中涉及的名词

   > - Git的三种状态
   >
   >   **已修改（modified）：**修改了文件，但还没保存到数据库中
   >
   >   **已暂存（staged）：**对当前已修改文件的当前版本做了标记，使之包含在下次提交的快照中（把已做出的修改放入暂存区保存，待到下次提交时将暂存区的所有修改一起提交）
   >
   >   **已提交（committed）：**提交的数据已经保存在了本地数据库中（持久化保存）
   >
   > - Git工作流程的三个阶段
   >
   >   ![工作区、暂存区以及 Git 目录。](https://git-scm.com/book/en/v2/images/areas.png)
   >
   >   **工作区（workspace）**：Git从数据库中提取出来的项目某个版本的内容（你在项目里看到的除了`.git`目录的其他目录都可以看成工作区）。
   >
   >   **暂存区（index\stage）**：实际上是一个文件，保存了下次将要提交的文件列表信息。
   >
   >   **Git 目录（Repository）**：Git 用来保存项目的元数据和对象数据库的地方，克隆仓库时，复制的就是 Git 目录的数据
   >
   >   ![](https://img2020.cnblogs.com/blog/2592465/202111/2592465-20211110172556035-1026107204.png)
   >
   > - 基本的工作流程总结
   >
   >   1. 在工作区中修改文件。
   >   2. 将你想要提交的更改选择性地暂存，这样只会将更改的部分添加到暂存区。
   >   3. 提交更新，快照永久性存储到 Git 目录。



## 基本操作

### 创建仓库

- 本地新建仓库

  在终端（或其他的类shell程序中）执行 `git init` ，在当前文件夹下创建一个git仓库

  ```shell
  git init . # 在当前(shell的工作路径)目录下创建 
  git init [dir_path] # 在指定的文件夹路径创建
  git init -b [分支名] # 创建仓库时指定本地主分支名
  git init --initial-branch=main # 同上
  ```

  

- 从远程仓库拉到本地

  在终端执行 `git clone <远程仓库地址>` ，将远程仓库拉到当前文件夹下

  clone 命令会自动将远程仓库命名为 origin，拉取它的所有数据，创建一个指向它的 main分支的指针，并且在本地将其命名为 origin/main。同时Git 也会给你一个与 origin 的main分支（项目默认的主分支）在指向同一个地方的本地 main分支（本地仓库的默认主分支）。

  例如从GitHub上拉取掌上重邮的仓库到本地：
  
  ```shell
  git clone git@github.com:RedrockMobile/CyxbsMobile_Android.git
  git clone https://github.com/RedrockMobile/CyxbsMobile_Android.git
  ```

在执行上述操作后，我们可以在项目文件夹中看到一个名称为 `.git` 的隐藏文件夹，Windows需要在显示中勾选 `隐藏的项目` 才能看到

![1689841720944.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1689841720944.png)

然后我们就可以看到以下文件夹，这个文件夹中的内容就是用于帮助我们进行版本管理的。

![1689841830043.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1689841830043.png)

这样我们就得到了一个Git仓库，接下来看看一些基础的命令使用。

### 基础命令

#### .gitignore文件

`.gitignore` 文件：里面声明了一些文件和目录，每次提交时Git会忽略这些文件和目录的修改，即该文件用于指定哪些文件或目录不应该被 Git 跟踪，有特殊需要可自行添加，例如：

![1689843342812.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1689843342812.png)

就是把**当前目录**下的 `build` 文件让Git忽略，当提交版本的时候也不会将 `build` 目录下的文件提交上去。

另外给出一些示例：

```shell
# 忽略所有的 .a 文件
*.a

# 但跟踪所有的 lib.a，即便你在前面忽略了 .a 文件
!lib.a

# 只忽略当前目录下的 TODO 文件，而不忽略 subdir/TODO
/TODO

# 忽略任何目录下名为 build 的文件夹
build/

# 忽略 doc/notes.txt，但不忽略 doc/server/arch.txt
doc/*.txt

# 忽略 doc/ 目录及其所有子目录下的 .pdf 文件
doc/**/*.pdf
```



#### add

```shell
git add [file/dir_name]  # 将指定文件或目录（的修改）添加到暂存区
git add .  # 将当前目录下所有“没被忽略”的文件和子目录的修改添加到暂存区(有些文件被.gitignore过滤,一般来说会过滤掉build文件来减小GitHub上仓库的体积)
git add *  # 添加所有的文件，包括(被.gitignore忽略的)
```

1、当我们准备提交一部分文件作为新的commit时，一般会在commit前进行add操作，这里的add只是标注“哪些文件的**修改**需要添加到这次commit中”。而不是“将哪些**文件**添加到这次commit”。

2、执行add命令会使得文件被Git追踪（tracked），文件作出的任何修改（包括删除、重命名、移动位置等）都会在每次文件被add时记录到暂存区

3、已经被Git追踪的文件，将其文件名添加到`.gitignore` 文件中是不会产生预期效果的。举个例子：

- 创建了`file_a.txt`，（这时`.gitignore` 文件中不包含它）然后执行了 `git add file_a.txt`
- 经历了一系列正常的Git操作之后
- 在`.gitignore` 文件中添加`file_a.txt`，然后对`file_a.txt`进行了修改（称为**修改A**），然后执行了 `git add file_a.txt` -> `git commit ……`  -> `git push [remote_path]`一系列命令，查看远程仓库，你会惊奇地发现，**修改A**居然被同步到了远程仓库中
- 如何解决这个问题，参见下方的`rm`命令



#### rm

大家都听说过删库跑路的经典命令 `rm -rf /*` 吧

![1690453445877.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690453445877.png)

Git 中也有 `rm` 操作，具体作用如下：

```shell
git rm [文件名] # 会删除暂存区或者分支上的文件，工作区的文件也会被删除，删除操作会被记录在接下来的提交中

git rm --cached [文件名] # 是从git取消对本文件的追踪（不会删除工作区的本地文件）。当你不想对本文件进行版本控制了，但想保留文件在目录中，就用本命令。
```

1. 当`rm`命令操作的对象包含目录时，使用`-r`参数 递归地遍历目录下的每一个子目录和子文件执行该操作

2. `rm --cached` 移除对某文件的追踪后，想要再次将该文件add到缓存区就需要通过`.gitignore` 文件的过滤直到该文件重新被追踪

3. rm的操作记录会被记录到缓存区并和其他缓存区的修改添加到下次的提交中

   

#### commit

```shell
# 直接提交信息（常用于短文本信息）
git commit -m "[对此次提交的描述]"
# 会弹出一个Git默认编辑器(这个和你安装Git时的选项有关)，以vim为例，按i进入insert插入模式，输入一些commit信息后退出。
# 这个git commit命令实际上和git commit -m 命令是等效的。
git commit
# 组合命令，将所有已追踪文件的修改add之后commit
git commit -a -m "[提交描述]"
```

以Vim为例：

commit信息输入完成后按**Esc**，按“**:**”键输入命令“**wq**”(write quit)按回车会自动保存,后退出，如果输入“q”表示直接退出不保存

如果已经commit了，发现commit描述里面缺少了部分信息，想要补加上，怎么办？可以使用以下命令：

```shell
git commit --amend # 用于修改最近一次的commit
```

> #### 注意：命令会产生一些不可忽视的副作用

`git commit --amend` 会自动将当前工作目录中所有已追踪文件 的未暂存（unstaged）的修改以及暂存（staged）的更改合并到上一次的提交中，并更改上一次提交的hash值，同时可以更改上一次提交的附带信息来对commit的描述进行补充和修改



#### stash

假如有这么一种情况，我们正在写一个功能，写到一半突然被老板告知需要修复另外一个bug，这时我们就需要另外切一个分支去修复这个bug

![1690373606291.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690373606291.png)

但是对于当前分支写了一半的新功能，我们有以下三种选择：

1. 直接丢弃已有的更改，checkout到目标分支进行后续操作。

   这样会让我们之前写的东西功亏一篑，在上一次commit之后的更改都将会丢失，损失惨重。

2. 对于已有的更改进行一次commit用于保存变动。

   但是并不推荐对未完成的内容进行一次commit，尽量在完整地完成一个板块后再进行commit。

3. 使用stash操作进行更改内容的暂存，完成其他分支的工作后再恢复暂存的内容继续开发。

   这样就可以让我们保存写了一半的内容，并且安心地去完成其他分支的工作了。

```shell
# 等同于git stash save/git stash push，能够将所有未提交的修改（工作区和暂存区）快照至堆栈中，用于后续恢复当前工作目录。
git stash

# 查看当前stash中的内容
git stash list

# 将当前stash中的内容中最近一次stash弹出，并应用到当前分支对应的工作目录上。相当于回退，但是该次stash的内容会消失
git stash pop

# 以下内容涉及到stash名字的地方需要注意：
# 如果你使用Windows系统并且是在PowerShell中使用以下命令，大括号会被识别为代码块，如果想正常使用，请在大括号前加反引号 `
# 使用反引号对大括号进行转义，例如： git stash apply stash@`{1`}

# 将堆栈中的内容应用到当前目录 如：git stash apply stash@{1}，该stash的内容不会消失
git stash apply [stash名字]
# 从stash的堆栈中删去指定的一次stash
git stash drop [stash名字]
# 清空stash列表 
git stash clear
# 查看堆栈中最新保存的stash和当前目录的差异
git stash show
```

`git stash save` 和`git stash push`  均可以在命令末尾添加一个可选的字符串参数，作为对该此快照的描述（类似于 `git commit -m "this is a message"`）

#### 状态变更

上述的几个命令会改变**文件**在Git仓库中的**状态**，状态变更以及对应的操作如下图所示：

![状态变更.jpg](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/%E7%8A%B6%E6%80%81%E5%8F%98%E6%9B%B4.jpg)

#### status

当文件状态改变后，应该如何查看文件目前处于一个什么状态呢？未跟踪，或是暂存？这时候就可以使用 `status` 命令查看各文件当前的状态（还会显示当前所在分支）

```shell
# 查看当前文件夹下文件的状态（例如:未追踪或未加入暂存区等状态）
git status
```

#### log

在提交之后会生成对应的提交记录，每次提交都会有一个哈希值，通过这些提交记录我们可以通过一些操作查看每次提交相关的信息。要查看提交记录可以使用 `git log` 相关的指令

```shell
# 查看log
git log

# 使用图形化的方式查看log
git log --graph

# 会显示每次提交的差异细节
git log -p

# 显示每次提交的统计信息（行数变化，修改过哪些文件）
git log --stat

# 查看引用的历史,默认为HEAD
git reflog
```

#### diff

如何显示不同提交之间的差异呢？可以使用 `diff` 操作查看两次commit之间文件的变动等信息。

```shell
# 显示工作区和暂存区文件的差异，如果没有add过（暂存区没有它），则对比的是最近一次版本和工作区的差异。
git diff [文件名]

# 对比工作区的文件和分支的文件的差别
git diff [分支名] [文件名]

# 对比暂存区和git仓库的区别（就是暂存区和最近一次commit的差异）
git diff --cached [文件名]

# 对比工作区和git仓库中某次提交的区别
git diff [哈希码] [文件名]

# 对比暂存区和git仓库中某次提交的区别
git diff --cached [哈希码] [文件名]

# 对比任意两次提交（可以来自不同分支，因为每次提交都有唯一的哈希码）
git diff [哈希码] [哈希码]
```

#### branch

分支相关的操作

```shell
# 新建一个分支
git branch [名称]

# 新建一个本地分支，并让其追踪一个远程分支
git branch [本地分支名称] [远程分支名称]

# 列出远程分支
git branch -r

# 列出本地分支，并且在当前分支前面加*号
git branch

# 删除在本地分支
git branch -d [名称]

# 删除远程分支
git push origin --delete [名称]

# 分支重命名
git branch -m [旧名称] [新名称]

# 主分支重命名
git branch -M [新的主分支名称]

# 查看本地仓库和远程仓库的对应关系
git branch -vv
```

#### checkout

checkout会将HEAD指针指向分支或者指向某一个commit

```shell
# 切换到某一分支
git checkout [分支名称]     # 切换分支
git checkout -b [分支名称]  # 新建一个分支并切换到该分支上
git checkout -b [本地分支名称] [远程分支名称] 	# 同branch操作，新建一个本地分支，让其追踪一个远程分支，并切换过去
git checkout -q [分支名称]  # 无提示切换分支
git checkout -f [分支名称]  # 强制切换（如果工作区有修改，则丢弃本次修改，强制切换到分支）

# 切换到某一次commit
git checkout [哈希值]		 # 切换到哈希值对应的commit上，commit对应的哈希值可通过log相关操作查看
```

#### reset

![img](https://ts1.cn.mm.bing.net/th/id/R-C.56f8b5e148fa570afaa8ffab058d6a0a?rik=OT2d8GQ%2bL1aOlg&riu=http%3a%2f%2fwww.linuxeden.com%2fwp-content%2fuploads%2f2021%2f11%2frefactor.jpg&ehk=Rjg1wzF0N%2fyddpNoP9yiBX8c3gD4mRx9TgFGt7x8Kaw%3d&risl=&pid=ImgRaw&r=0) 

当我们尝试对代码进行改动时，总会出现明明没改什么东西但是代码却无法运行的情况。如果在这之前有commit记录，那么可以使用 **reset** 操作回到上一次commit的样子（无参`git reset`命令的结果），让程序恢复正常。

**reset** 是一个比较常用的操作，可以带着分支一起往某个commit移动，或者将当前分支移动到某个分支所指向的commit

```shell
git reset [目标commit的哈希值] [reset的模式，默认为 --mixed ]
```

reset的模式有两个

| 模式    | 含义                                                         |
| ------- | ------------------------------------------------------------ |
| --soft  | 只移动到对应的commit，文件的变动（工作目录和暂存区的更改）仍然存在，但是在Git中的状态会对应改变 |
| --hard  | 移动到对应的commit，文件的变动也会丢失，文件会完全还原至目标commit的样子 |
| --mixed | 移动到对应的commit，只保留工作目录的修改，暂存区则重置为该commit的状态 |



#### rebase

顾名思义，**变基**，即改变当前分支指向的基础

假设有这样一条本地分支树(当前在featrue分支)：

![image_git_rebase_1](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262220470.png)

执行`git rebase main `之后：

![image_git_rebase_2](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262220985.png)

使用rebase（变基）可以简化美化分支，也是一种分支合并操作，但是他会将分支复制一份，然后只显示从1-4‘这一条线路（美化后的分支路径），从树形图来看rebase的合并减少了树的分叉，同时如果4还有分支指向的话，不会随着feature一起移动

使用 `rebase -i`可以使用交互式的提交修改，可以使用其他指令来修改这个rebase过程

进入交互式的界面后大概可以看到如下的命令提示（不同版本的Git提示可能会有不同，请以自己电脑上安装的Git的相关提示信息为准）：

```shell
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
```

#### merge

将目标分支合并进当前分支

```shell
git merge [可选参数] [分支名]
# 参数 --commit（默认）自动生成一个提交，包含两个节点合并的结果。
# 参数 --no-commit 为了防止合并失败，先不提交，让用户手动提交
```

`git merge branch_a` 命令的结果是：将 分支 `branch_a`合并到当前分支中，并生成一个合并后的commit

如果有冲突则要先处理冲突，Git会列出冲突的文件，我们需要打开这些文件一个一个地合并（Git自动合并了全部，我们只用删掉不需要的部分即可），然后重新commit就行了（这时不用再merge了）

merge的分类

| 类别           | 含义                                                 |
| -------------- | ---------------------------------------------------- |
| --fast-forward | 分支合并无冲突，直接砍掉分支信息，认为是主分支的推进 |
| --no-ff        | 单独创建一个commit来完成合并(默认)                   |
| --squash       | 可以对被合并分支的多次提交压缩为一次提交信息         |





#### cherry-pick

如果某个分支不需要了，但是其中的3个commit的变动需要迁移到当前分支，可以使用 `cherry-pick` 操作，获取另一个分支中的commit信息

```shell
git cherry-pick [hashcode1] [hashcode2] [hashcode3]
```

上面命令就会将指定的3个hashcode对应的提交，应用于当前分支。这会在当前分支产生对应个数的新的提交，当然它们的哈希值和原来的会不一样。

另外如果在操作过程中发生代码冲突，Cherry pick 会停下来，让用户决定如何继续操作，不过之后的操作使用git命令行比较麻烦，对新手来讲不太友好，给出一个Git官方文档关于cherry-pick命令的链接供查阅：

https://git-scm.com/docs/git-cherry-pick



#### Git分支概念

前面介绍完了一些有关Git分支的操作，相信大家对分支有了一些自己的理解，那么Git分支到底是一个什么样的存在呢？在我们对其进行切换，新建，合并等等操作的时候，分支到底具体发生了哪些变化？

在Git中，分支指的是从主线上分离出来进行另外的操作，既不影响主线，主线又可以继续干它的事，它可用来解决临时需求；当分支做完事后可合并到主线上，而分支的任务完成可以删掉了。

> 如果听起来还是比较懵，可以这这么想：
>
> 每个分支被创建时实际上可以看成 `截取当前时间节点的分支来源` 并以该来源为基础`创建一个副本分支(类似于平行世界)`，当“平行世界”的使命完成时就可以与“主世界”相融合，这样在“平行世界”发生的事就会在“主世界”成为既定的现实

每一个分支相当于一个隔离的环境进行开发，可以用于：

- 新功能的开发
- bug的修复

在Git中有一个特殊的引用HEAD，它只会指向当前分支最新的commit（**何解？**）。

当Git需要创建新分支的时候，它不需要将主分支的所有内容重新拷贝一份副本，只需要让新分支的指针指向某一个commit对象，这个commit对象及其之前的所有commit内容都将作为新分支的基础。然后对新分支进行修改再提交之后，那么新分支的指针就会指向你对新分支最新提交的这个commit对象，而原来分支的指针则指向你原来开发的位置(不会因为新分支的建立而受到影响)
**而当你在哪个分支开发，HEAD就指向那个分支的最新提交对象commit**。

我们来两张图展示一下：

![image_git_branch](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262015624.png)

![image_new_branch](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262016973.png)

当我们使用  `git branch` 指令查看分支时，前面有个*号的就为我们目前所处的分支，而这个分支的指针就指向最新的commit对象，也就和HEAD指向同一对象。也可以通过 `checkout`  操作来切换到目的分支。



分支的创建和切换操作，其实只是简单的创建指针找指针而已，而根据找到的指针找到所指向的commit对象，然后将工作空间恢复成该commit对象所指的文件快照让我们来进行后续的工作。当提交一次，指针就重新指向这个最新提交的对象。

下面用几张图来举例解释下我们对分支的操作对commit树有什么影响（若我们默认的主分支为 **`main`** ）：

我们在新建分支前：

![image_branch_show_pic_1](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262021849.png)

此时只有一个main分支，同时**HEAD**指向**最新的commit**也就是**commit_3** 



此时我们如果通过  `git branch dev` 命令**新建一个dev分支**的话，dev也指向**commit_3** （如下图）：

![image_branch_show_pic_2](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262021868.png)

由于新建dev分支的操作没有改变最新的 commit，因此，main分支和dev分支指针均指向当前的最新commit： **commit_3**

而且此时也没有切换当前的分支，故HEAD不改变



当我们在dev分支上开发并提交了两个版本commit_4 , commit_5后，由于HEAD要指向最新的commit，因此会指向dev分支的最新commit：**commit_5**（如下图）：

![image_branch_show_pic_3](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262021860.png)



假如这时候dev开发完成，要和main分支合并，由于main没有另外迁出版本(***用树来形容就是，树的主干自新枝桠长出的那一刻直到现在为止都停止了生长，而且没有生出另外的新的枝桠***)，与dev不冲突，那么就会 直接将main指针指向最新版本commit_5，也就是Fast-forward合并，此时如果dev分支任务完成了，删除dev分支即可：

![image_branch_show_pic_4](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262021874.png)



如果在dev开发两个版本后，在main分支的版本也更新了commit_6 , commit_7的话，首先HEAD会指向最新一次commit，也就是commit_7：

![image_branch_show_pic_5](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262021894.png)



此时要将dev合并进main分支，需要将commit_5 和 commit_7合并成一个commit_8版本，如果commit_5和commit_7的文件差别较大，需要**手动处理**好两个**版本间的冲突**才能继续合并：

![image_branch_show_pic_6](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262021901.png)



##### 本地分支、追踪分支和远程分支

- **本地分支**：本地分支就是我们可以通过 `git branch` 查看到的分支，也就是我们自己本地的Git仓库所创建和管理的分支，我们在本地都可以随意使用。

- **远程分支**：远程分支在逻辑概念上存在于远程仓库，但你在本地也可以查看到远程分支的信息，这时因为当我们从远程仓库克隆项目时，Git会获取远程仓库中存在的分支信息，并在本地为每个远程分支创建一个对应的远程跟踪分支。

- **追踪分支**：追踪分支比较难理解，它**也是一个存在于本地的分支**，只是它**对应了一个远程分支**，并可以关联与远程交互时的本地分支。那么本地就可以将更新到最新版的追踪分支当成远程分支来看待

- ##### 举个栗子

  假设我们从远程仓库克隆时（不考虑clone时指定某一个特殊分支/提交的情况），Git会帮我们自动建立一个与远程主分支同名的本地主分支（以`main`为例）同时建立一系列与每一个远程分支对应的追踪分支，远程主分支`main`对应本地追踪分支`origin/main`，这里origin指代了远程仓库名。

  当我们在本地main分支里执行默认远程交互操作，比如更新(fetch，pull)或是推送(push)，在当前本地分支为`main`且操作时不显式指定分支的情况下，默认的下载数据流为: `remote/main => origin/main => local/main`，上传数据流为：`local/main => origin/main => remote/main `

  你可能会奇怪`local/main`和`origin/main`是怎么关联起来的，总不能是更根据分支的名字对应吧，欸，还真不是。在Git中有这样的一条命令来设置本地分支与追踪分支的对应关系（当然也可以说是建立本地分支与远程分支的关联）

  ```shell
  git branch --ser-upstream-to=[追踪分支] [本地分支]
  ```

  而`local/main`和`origin/main`的对应关系实际上早就在Git帮你自动建立`local/main`时帮你设定好了



同样的，我们来几张草图生动形象的理解一下

假设我刚从远程拉下来一个仓库

![image_branch_show_pic_7](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262040876.png)

此时，`HEAD`指向最新一次commit 版本commit_3，本地分支`main`也指向commit_3，远程分支`origin/main`也指向 commit_3。 这里本地的`main`分支对应了远程`main`分支的追踪分支`origin/main`



如果我们没有及时更新追踪分支，自己在本地埋头苦干更新本地版本的话，就会是这样的情况

![image_branch_show_pic_8](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262040880.png)



当我们在本地开发的时候，已经有人开发完成并且推送到远程分支的话 (也就是远程分支在未与本地分支新的版本同步的情况下，被团队里的其他成员更新了)，可怕的事情就来了：

<img src="https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262040885.png" alt="image_branch_show_pic_9" style="zoom:135%;" />

当我们把远程分支更新到本地之后一看，好家伙！

别人都把远程推到commit_8了，如果要把我们本地的合并进最新的远程分支，**又要处理一堆的冲突** 因此建议大家在多人开发的时候一定要及时拉取最新的分支



#### remote

在本地对远程仓库的操作

##### 添加远程仓库

```shell
git remote add [远程仓库名] [远程仓库地址]
```

例如，要添加一个掌上重邮远程仓库，指定仓库名为**origin**，指令如下：

```shell
   			   		 # 名称                 远程仓库地址
git remote add origin git@github.com:RedrockMobile/CyxbsMobile_Android.git
```

如果手误输错了仓库名，需要更改的话，可以使用 **rename** ，例如需要修改名称  orgin -> origin

```shell
								# 原名称 修改后名称
git remote rename orgin origin
```

##### 移除远程仓库

```shell
    	   	  	#仓库名
git remote rm origin
```

##### 查看远程仓库

```shell
# 查看现有的仓库有哪些（一般只有一个origin仓库，这是默认的名称）
git remote
# 可以查看仓库的地址
git remote -v
```

#### clone

#### 

<img src="https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262127179.png" alt="image_git_clone" style="zoom:135%;" />
先克隆引用，然后根据引用的指向依次拿到commit对象，一直拿到溯源拿到根部的commit

#### 

#### fetch

更新本地追踪分支的指针

```shell
# 这个命令查找 “origin” 对应的远程仓库，从中抓取本地没有的数据，并且更新本地数据，移动 origin/main 指针指向新的、更新后# 的位置。
git fetch origin

# 当然我们也可以直接fetch
git fetch
```

听起来有点朦朦胧胧的，那么fetch到底做了什么？

1. 让Git从指定的远程仓库（比如 `origin` ）拉取了所有分支的最新提交信息和分支信息
2. 将获取到的远程分支信息更新到本地对应的远程跟踪分支。

> #### 注意，`fetch`命令不会主动更新本地的非追踪分支

在更新远程分支后，如果想基于 `origin/main` 分支继续工作，就可以从该分支迁出新分支进行开发：

```shell
git checkout -b dev origin/main
```

如果本地已经有一个 `main` 分支，并且想将 `origin/main` 拉取下来的更新合并入该分支，需要手动合并：

```shell
# 首先需要切换到本地main分支
git checkout main
# 将 origin/main 合并 到 main 分支
git merge origin/main
```

#### pull

从指定的远程仓库（通常是默认的 `origin` ）获取最新的更改，并将其合并到当前所在的本地分支。
```shell
git pull
```

上面的命令其实就相当于一并执行了 `fetch` 和 `merge` 两个指令:

```shell
# git fetch 会把所有的远端镜像更新到本地，然后更新缺少的commit，相当于是同步
git fetch

# git merge  会合并当前HEAD指向的分支，其余分支并不会
git merge origin/[对应的远程分支名]

# 可以在pull后添加 -r或--rebase 参数让合并的操作更换为rebase
```

另外其实该命令的完整格式大抵是这样：

```shell
git pull [远程主机名] [远程分支名]:[本地分支名]
```

即从指定的远程仓库（一般为默认的`origin`）的指定远程分支拉取最新的更新合并到指定的本地分支上（若指定的本地分支为当前所在本地分支，则可以省略不写）例如，`git pull origin main` 表示取回 `origin/main` 分支，并与本地的当前分支合并。

- 如果当前分支与远程分支存在追踪关系，`git pull` 可以省略远程分支名，如 `git pull origin` 表示本地的当前分支自动与对应的 `origin` 远程仓库追踪分支进行合并。
- 如果当前分支只有一个追踪分支，甚至连远程主机名都可以省略，直接使用 `git pull` 即可。

#### push

前面提过了如何把远程仓库的更新拉取到本地并且合并进分支，`push` 操作则是将本地的更改提交到远程仓库上去（其命令格式同pull）。

```shell
# 会将某个分支推送到远程分支上
git push [远程主机名/仓库名] [本地分支名]:[远程分支名]

# 表示将当前分支推送到[远程主机名]的对应分支
git push [远程主机名/仓库名]

# 强行推送，会强行覆盖掉远程仓库，慎用！
git push -f
```

我们来张图：

![image_git_push](https://obssh.obs.cn-east-3.myhuaweicloud.com/img_xunguang/202407262212358.png)
先将HEAD及指向的推到远程，然后把分支指向的commit补全，然后远端的HEAD会更新指到分支头上，同时本地的远端镜像也会更新

只有一个远程主机时，`git push` 后的远程主机名可以省略

如果有多个远程主机， 想要设置push的默认主机，可以使用

```shell
git push -u origin main
```

把本地当前分支先push到远程主机`origin`的main分支一次，确立远程分支与本地分支的追踪关系，后续可以直接使用 `git push` 默认push到远程主机 `origin` 上

这个`-u`参数的完整写法是**`--set-upstream`**,作用就是指定本地分支的上游分支。在本地仓库首次push到远程新仓库时一般都要强制加上该参数

![bbf9ac789c6d92a93f261b71d610de52.jpeg](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/bbf9ac789c6d92a93f261b71d610de52.jpeg)

#### tag

当我们想标记一次重要的commit，例如App发布一个版本v6.0.1的时候，就需要用到 `tag` 操作进行一个标记（标记重要的版本发布点，如`v1.0` 、`v2.11`等 或 对特定的开发阶段或里程碑进行标记，如 `beta-1`、`rc-2` ）

**编辑并提交tag（注意此时提交的tag还在本地）**

```shell
# 创建轻量标签
git tag [tag名称]

# 创建附注标签
git tag -a [版本号/tag名称] -m '版本信息或该次tag的介绍'
```

**给之前的commit 打 tag**

```shell
git tag -a [tag名称] [commit的哈希值] -m '信息'
```

**把本地的tag推送上去**

```shell
# 全部推送
git push origin --tags
# 推送指定tag
git push origin [tag名称]
```

推送到远程仓库后我们就能看到对应的tag，例如GitHub：

![1690461007680.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690461007680.png)

**如果突然发现有严重bug，可以删除tag（注意此时也是删除的本地）**

```shell
git tag -d 版本号
```

**在删除了本地tag之后再同步删除对应的远程tag**

```shell
git push origin :refs/tags/v1.1
```

同时，在一些情况下也可以使用 `tag` 来代替commit的哈希值使用

例如：

```shell
git checkout tag名称
git checkout -b new分支名称 tag名称
git pull --t tag名称
```

#### GitHub

~~GayHub~~ GitHub是 ~~全球最大的同性交友网站~~ 全球最大的代码托管平台，它提供了一个集中存储、版本控制、协作和代码管理的平台。它提供了强大的协作功能，允许多个开发者共同参与一个项目，进行代码的修改、审查和合并等等。

[GitHub](https://github.com/) 这是GitHub的官方网站，可以在这里注册账号并开始使用GitHub。

##### Pull requests

在把本地的开发分支推到云端后，我们可以向仓库提一个Pull requests来更加安全地将我们的分支合并进仓库主分支中。

![1690461413049.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690461413049.png)

选择需要合并的原分支和目的分支，创建pr

![1690511549622.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690511549622.png)

完善合并描述，提交

![1690511633370.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690511633370.png)

然后就可以等待仓库管理员对我们的pr进行合并/打回，我们也可以在pr下与管理员进行交流

![1690512578368.png](https://why-1308312529.cos.ap-chongqing.myqcloud.com/2023_general_education_git/1690512578368.png)
