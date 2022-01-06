## 一些常用的Git命令

git branch -d ry 删除本地分支  
git merge feature-2022-01-06/declare 本地合并分支（dev合并declare...）  
git checkout -b feature-2022-01-06/declare 新建某个分支

## 使用规范

### 分支命名规范

|  分支   | 命名  |       说明  |
|  ----   | ----  |  ----  |
|主分支  | master | 主分支 |
|开发分支 | dev  | 开发分支 |
|功能分支 | feature-* | 新功能分支，某个功能点正在开发阶段 |
|发布版本 | release-* | 发布定期要上线的功能 |
|修复分支 | bug-*  | 修复线上代码的 bug |
|验证分支 | demo-*    |  技术调研，完成后删除该分支 |

### commit 提交规范

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

#### Header

包括三个字段：type（必需）、scope（可选）和subject （必需）

**type类别:**

 1. feat：新增功能
 2. fix：bug 修复
 3. docs：文档更新
 4. style：不影响程序逻辑的代码修改(修改空白字符，格式缩进，补全缺失的分号等，没有改变代码逻辑)
 5. refactor：重构代码(既没有新增功能，也没有修复 bug)
 6. perf：性能, 体验优化
 7. test：新增测试用例或是更新现有测试
 8. build：主要目的是修改项目构建系统(例如 glup，webpack，rollup 的配置等)的提交
 9. ci：主要目的是修改项目继续集成流程(例如 Travis，Jenkins，GitLab CI，Circle等)的提交
 10. chore：不属于以上类型的其他类，比如构建流程, 依赖管理
 11. revert：回滚某个更早之前的提交

**scope（可选）:**

用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同

**subject（必填）:**

commit 目的的简短描述，

#### Body

本次 commit 的详细描述，可以分成多行。

#### Footer

...

## 命令行

分布式版本控制系统
[下载安装程序](https://git-scm.com/downloads)  

[git init](#git-init)：把这个目录变成Git可以管理的仓库  
[git add](#git-add)：添加文件到仓库  
[git commit -m '备注'](#git-commit)：提交文件到仓库  
[git status](#git-status)：查看仓库状态  
[git diff](#git-diff)：查看修改修改内容  
[git log](#git-log)：显示从最近到最远的提交日志(git log --pretty=oneline 一行一行显示)（git log --graph --pretty=oneline --abbrev-commit：查看分支的合并情况）  
[git reset](#git-reset)：撤回，前进或者说是重置 HEAD 指向  
[git reflog](#git-reflog)：查看看命令历史  
[git checkout -- file](#git-checkout----file)：撤销修改  
[git rm](#删除文件)：从版本库中删除文件  
[git remote add](#添加远程库和git-push)：关联一个远程库  
[git clone](#从远程库克隆)：克隆一个本地仓库  
[git switch -c \<name>](#创建与合并分支)：创建+切换分支或者git checkout -b name  
[git branch <name>](#创建与合并分支)：创建分支,查看分支  
[git switch <name>](#创建与合并分支)：切换分支或者 git checkout name  
[git merge <name>](#创建与合并分支)：合并分支
[git branch -d <name>](#创建与合并分支)：删除分支  
[git stash](#bug分支)：“储藏”工作现场，开辟干净工作区  
[git stash list](#bug分支)：查看stash列表  
[git stash pop](#bug分支)：恢复的同时把stash内容也删了（另一种是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；）  
[git cherry-pick <commit>](#bug分支)：把bug提交的修改“复制”到当前分支，避免重复劳动。  
[git branch -D <name>](#Feature分支)：强行删除没有被合并的分支  
[git remote -v](#多人协作)：查看远程库信息  
[git push origin branch-name](#多人协作)：从本地推送分支  
[git checkout -b branch-name origin/branch-name](#多人协作)：在本地创建和远程分支对应的分支  
[git pull](#多人协作)：从远程抓取分支，如果有冲突，要先处理冲突。  
[git branch --set-upstream branch-name origin/branch-name](#多人协作)：建立本地分支和远程分支的关联  
[git rebase](#创建标签)：可以把本地未push的分叉提交历史整理成直线，目的是使得我们在查看历史提交的变化时更容易  
[git tag <tagname>](#创建标签)：用于新建一个标签，默认为HEAD，也可以指定一个commit id  
[git tag -a <tagname> -m "blablabla..."](#创建标签)：可以指定标签信息；  
[git tag](#创建标签)：可以查看所有标签  
[git show <tagname>](#创建标签)：查看标签信息  
[git push origin <tagname>](#操作标签)：可以推送一个本地标签(git push origin --tags 可以推送全部未推送过的本地标签)  
[git tag -d <tagname>](#操作标签)：可以删除一个本地标签  
[git push origin :refs/tags/<tagname>](#操作标签)：可以删除一个远程标签。  

### 配置名字和邮箱

```
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
```

查看是否配置成功

```
git config user.name
git config user.email
```

### 创建一个版本库

```
$ mkdir learngit     # 创建一个learngit 文件夹
$ cd learngit        # 进入learngit文件夹
$ pwd               # 显示当前目录
/e/ggg/learngit
```

### git init

把这个目录变成Git可以管理的仓库（当前目录下多了一个.git的目录，Git来跟踪管理版本库的）

### git add

文件添加到仓库

```
$ vi readme.txt
                        # 输入文本，保存退出文本编辑模式
$ git add readme.txt  
/*有时候会出现这个
注:warning: LF will be replaced by CRLF in readme.txt.
The file will have its original line endings in your working directory.

出现此问题是因为不同操作系统的使用的换行符不同：
     Linux / Unix 采用换行符LF表示下一行
     Windows  采用回车+换行 CRLF表示下一行
     
解决：可以通过设置 core.autocrlf 的值解决
*/
$ git config --global core.autocrlf false   # 关闭自动转换 
```

一、vi & vim 有两种工作模式：
1.命令模式：接受、执行 vi操作命令的模式，打开文件后的默认模式；
2.编辑模式：对打开的文件内容进行 增、删、改 操作的模式；

在编辑模式下按下ESC键，回退到命令模式。

二、创建、打开文件：$ vi [filename]
1.使用 vi 加 文件路径（或文件名）的模式打开文件，如果文件存在则打开现有文件，如果文件不存在则新建文件，并在终端最下面一行显示打开的是一个新文件。
2.键盘输入字母i或Insert键进入最常用的插入编辑模式。

三、保存文件：
1.在插入编辑模式下编辑文件。
2.按下ESC键，退出编辑模式，切换到命令模式。
3.在命令模式下键入ZZ或者:wq保存修改并且退出 vi。
4.如果只想保存文件，则键入:w，回车后底行会提示写入操作结果，并保持停留在命令模式。

四、放弃所有文件修改：
1.放弃所有文件修改：按下ESC键进入命令模式，键入:q!回车后放弃修改并退出vi。
2.放弃所有文件修改，但不退出 vi，即回退到文件打开后最后一次保存操作的状态，继续进行文件操作：按下ESC键进入命令模式，键入:e!，回车后回到命令模式。

### git commit

用命令git commit告诉Git，把文件提交到仓库

```
$ git commit -m "first update"

[master (root-commit) 07b4f9f] first update
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

git commit命令，-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。  
git commit命令执行成功后会告诉你，1 file changed：1个文件被改动（我们新添加的readme.txt文件）；2 insertions：插入了两行内容（readme.txt有两行内容）。  

### git status

查看仓库当前的状态  （文件是否被修改过）
 修改readme.txt文件

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

 modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

### git diff

查看修改内容

```
$ git diff
diff --git a/readme.txt b/readme.txt
index 4719ba8..edef4fb 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,5 @@
 Git i free software
 hello word
+one
+two
+three
```

```
$ git add readme.text
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   readme.txt

$ git commit -m "add txt"
[master 26dc555] add txt
 1 file changed, 3 insertions(+)

$ git status
On branch master
nothing to commit, working tree clean
```

### git log

查看提交历史，以便确定要回退到哪个版本。

```
$ git log
commit ddd7388edf2402301b8b7edef58596c522c3c3ca (HEAD -> master)           一大串类似ddd7388edf24...的是commit id（版本号），用来退回版本
Author: tangxiangdong <63951240@qq.com>
Date:   Tue Dec 1 10:06:04 2020 +0800

    six

commit 26dc555a07aa1e28b461055840d144bf7a4ad806
Author: tangxiangdong <63951240@qq.com>
Date:   Tue Dec 1 10:02:28 2020 +0800

    add txt

commit 07b4f9f0016cf71ab075a8f81052754f0a2cfb8e
Author: tangxiangdong <63951240@qq.com>
Date:   Tue Dec 1 09:53:45 2020 +0800

    first update
    
# 整理为一行    
$ git log --pretty=oneline
ddd7388edf2402301b8b7edef58596c522c3c3ca (HEAD -> master) six
26dc555a07aa1e28b461055840d144bf7a4ad806 add txt
07b4f9f0016cf71ab075a8f81052754f0a2cfb8e first update
```

### git reset

回退版本  
上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

```
$ git reset --hard HEAD^
HEAD is now at 26dc555 add txt

$ cat readme.txt #查看文件，发现果然被还原了

$ git log
commit 26dc555a07aa1e28b461055840d144bf7a4ad806 (HEAD -> master)
Author: tangxiangdong <63951240@qq.com>
Date:   Tue Dec 1 10:02:28 2020 +0800

    add txt

commit 07b4f9f0016cf71ab075a8f81052754f0a2cfb8e
Author: tangxiangdong <63951240@qq.com>
Date:   Tue Dec 1 09:53:45 2020 +0800

最新的那个版本append GPL已经看不到了！好比你从21世纪坐时光穿梭机来到了19世纪，想再回去已经回不去了，肿么办？

办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个append GPL的commit id是ddd73...，于是就可以指定回到未来的某个版本：
$ git reset --hard ddd73
HEAD is now at ddd7388 six
```

### git reflog

查看命令历史，以便确定要回到未来的哪个版本。  
如果已经关掉窗口，可以用这个命令找到 commit id

```
$ git reflog
ddd7388 (HEAD -> master) HEAD@{0}: reset: moving to ddd73
26dc555 HEAD@{1}: reset: moving to HEAD^
ddd7388 (HEAD -> master) HEAD@{2}: commit: six
26dc555 HEAD@{3}: commit: add txt
07b4f9f HEAD@{4}: commit (initial): first update
```

### 工作区和暂存区

![工作区和暂存区](http://gitlab.nbpitech.com/tangxd/photo/raw/master/0.jpg)  
><http://gitlab.nbpitech.com/tangxd/photo/raw/master/0.jpg>  
是分两步执行的：  
第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区(stage)。  
第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。

### 管理修改

Git跟踪并管理的是修改，而非文件。  
第一次修改 -> git add -> 第二次修改 -> git commit  
Git管理的是修改，当你用git add命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，git commit只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。  

### git checkout -- file

可以丢弃工作区的修改

```
git checkout -- readme.txt     //命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令，
```

一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。  
总之，就是让这个文件回到最近一次git commit或git add时的状态。

### git reset HEAD <file>

可以把暂存区的修改撤销掉（unstage），重新放回工作区。  

```
$ git reset HEAD readme.txt
Unstaged changes after reset:
M readme.txt
```

git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。  
再用git status查看一下，现在暂存区是干净的，工作区有修改。  
假设你不但改错了东西，还从暂存区提交到了版本库，怎么办呢？还记得版本回退一节吗？可以回退到上一个版本。不过，这是有条件的，就是你还没有把自己的本地版本库推送到远程。还记得Git是分布式版本控制系统吗？我们后面会讲到远程版本库，一旦你把stupid boss提交推送到远程版本库，你就真的惨了……  

### 删除文件

```
$ git add test.txt

$ git commit -m "add test.txt"
[master b84166e] add test.txt
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
 
 $ rm test.txt       #直接在文件管理器中把没用的文件删了，或者用rm命令删了
 
 #Git知道你删除了文件，因此，工作区和版本库就不一致了，git status命令会立刻告诉你哪些文件被删除了
 $ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

 deleted:    test.txt

no changes added to commit (use "git add" and/or "git commit -a")

#从版本库中删除该文件，那就用命令git rm删掉，并且git commit
$ git rm test.txt
rm 'test.txt'

$ git commit -m "remove test.txt"
[master d46f35e] remove test.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt
 
 # 另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本
 $ git checkout -- test.txt
 ```

### 远程仓库

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key

```
ssh-keygen -t rsa -C "youremail@example.com"
```

你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。  
如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。  
第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面。  

为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。  
最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。

### 添加远程库和git push

```
$ git remote add origin git@github.com:michaelliao/learngit.git
#origin 是你为远端仓库所起的名字，一般都是叫origin，其实你也可以要Ceres 或者Earth
# git@github.com:michaelliao/learngit.git  是你的远端仓库的真实地址          

$ git push -u origin master  #把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
```

我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
`$ git push origin master`

### 从远程库克隆

git clone    -b {{develop}}   {ssh地址}

### 创建与合并分支

```
$ git checkout -b dev              #创建dev分支，然后切换到dev分支： 或者 git switch <name>
Switched to a new branch 'dev'
```

git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：

```
$ git branch dev
$ git checkout dev
Switched to branch 'dev'
```

然后，用git branch命令查看当前分支

```
$ git branch
* dev
  master
  
$ git add readme.txt 
$ git commit -m "branch test"
$ git checkout master                 #dev分支的工作完成，我们就可以切换回master分支

$ git merge dev                         #把dev分支的工作成果合并到master分支上
Updating d46f35e..b17d20e
Fast-forward
 readme.txt | 1 +
 1 file changed, 1 insertion(+)         
 
 $ git branch -d dev                 #删除dev分支
 Deleted branch dev (was 6e6626d).
```

**切换分支：`git checkout <name>或者git switch <name>`**

### 解决冲突

两个分支修改同一个文件

```
# 创建一个新分支修改文件，并提交
$ git switch -c feature1
Switched to a new branch 'feature1'

$ git add readme.txt

$ git commit -m "AND simple"
[feature1 14096d0] AND simple
 1 file changed, 1 insertion(+), 1 deletion(-)
 
 # 切换到master分支，修改文件并提交
$ git switch master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
  
$ git add readme.txt 
$ git commit -m "& simple"
[master 5dc6824] & simple
 1 file changed, 1 insertion(+), 1 deletion(-)

#合并发生冲突
$ git merge feature1
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.

#需要人工手动修改问题，在add和commit

$ git log --graph --pretty=oneline --abbrev-commit     #看到分支的合并情况：
*   cf810e4 (HEAD -> master) conflict fixed
|\  
| * 14096d0 (feature1) AND simple
* | 5dc6824 & simple
|/  
* b17d20e branch test
* d46f35e (origin/master) remove test.txt
* b84166e add test.txt
* 519219b git tracks changes
* e43a48b understand how stage works
* 1094adb append GPL
* e475afc add distributed
* eaadf4e wrote a readme file
```

### 分支管理策略

通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。  
如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

准备合并dev分支，请注意--no-ff参数，表示禁用Fast forward：

```
$ git merge --no-ff -m "merge with no-ff" dev
Merge made by the 'recursive' strategy.
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
 
 $ git log --graph --pretty=oneline --abbrev-commit
*   e1e9c68 (HEAD -> master) merge with no-ff
|\  
| * f52c633 (dev) add merge
|/  
*   cf810e4 conflict fixed
```

### Bug分支

```
//将保留一个现场  
git stash  
  
--------------  
  完成另外一个任务  
--------------   
  
//列出现场  
git stash list  
  
//恢复现场  
git stash apply <stash@{id}> //恢复现场，现场列表依旧存在该现场,如果没有stash@{id}则删除栈顶
git stash pop    //弹出现场，栈顶现场删除了

//删除现场
git stash drop <stash@{id}>

----------------------------------------------------

//在bug分支在自己分支部分合并
 git cherry-pick <branch id>    
```

### Feature分支

开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过git branch -D name 强行删除。

### 多人协作

要查看远程库的信息，用git remote：

```
$ git remote
origin

git remote -v
origin  git@github.com:txd688/Git.git (fetch)
origin  git@github.com:txd688/Git.git (push)
```

推送分支

```
git push origin master
```

如果要推送其他分支，比如dev，就改成：

```
git push origin dev
```

抓取分支

```
git clone git@github.com:txd688/Git.git
```

默认情况下，你的小伙伴只能看到本地的master分支和创建远程origin的dev分支到本地，

```
$ git branch
* master

$ git checkout -b dev origin/dev
```

有时候报这个错误，是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接

```
$ git pull
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dev
    
$ git branch --set-upstream-to=origin/dev dev
```

因此，多人协作的工作模式通常是这样：  
首先，可以试图用git push origin \<branch-name>推送自己的修改；  
如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；  
如果合并有冲突，则解决冲突，并在本地提交；  
没有冲突或者解决掉冲突后，再用git push origin \<branch-name>推送就能成功！  
如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to \<branch-name> origin/\<branch-name>。  
这就是多人协作的工作模式，一旦熟悉了，就非常简单。  

### 创建标签

发布一个版本时，我们通常先在版本库中打一个标签（tag），这样，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。

Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的。

Git有commit，为什么还要引入tag？

“请把上周一的那个版本打包发布，commit号是6a5819e...”

“一串乱七八糟的数字不好找！”

如果换一个办法：

“请把上周一的那个版本打包发布，版本号是v1.2”

“好的，按照tag v1.2查找commit就行！”

所以，tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起。

```

$ git branch
* dev
  master
$ git checkout master
Switched to branch 'master'

#创建一个标签
$ git tag v1.0

#查看所有标签：
git tag

#如果忘了打标签，找到历史commit id，再打上
$ git log --pretty=oneline --abbrev-commit
12a631b (HEAD -> master, tag: v1.0, origin/master) merged bug fix 101
4c805e2 fix bug 101
e1e9c68 merge with no-ff
f52c633 add merge
cf810e4 conflict fixed
5dc6824 & simple
14096d0 AND simple
b17d20e branch test
d46f35e remove test.txt
b84166e add test.txt
519219b git tracks changes
e43a48b understand how stage works
1094adb append GPL
e475afc add distributed
eaadf4e wrote a readme file

$ git tag v0.9 f52c633

#git show <tagname> 查看标签信息
$ git show v0.9
commit f52c63349bc3c1593499807e5c8e972b82c8f286 (tag: v0.9)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:56:54 2018 +0800

    add merge

diff --git a/readme.txt b/readme.txt

#还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：
$ git tag -a v0.1 -m "version 0.1 released" 1094adb
```

### 操作标签

删除标签

```
git tag -d v0.1
```

因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

如果要推送某个标签到远程，使用命令git push origin \<tagname>：  

```
$ git push origin v1.0
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:txd688/Git.git
 * [new tag]         v1.0 -> v1.0

#一次性全部推送tag
git push origin --tags
```

如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：

```
$ git tag -d v0.9
Deleted tag 'v0.9' (was f52c633)

$ git push origin :refs/tags/v0.9
To github.com:michaelliao/learngit.git
 - [deleted]         v0.9
```
