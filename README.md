# 一些常用的Git命令
分布式版本控制系统
[下载安装程序](https://git-scm.com/downloads)

### 配置名字和邮箱
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
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
>http://gitlab.nbpitech.com/tangxd/photo/raw/master/0.jpg
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
$ git checkout -- readme.txt     //命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令，
```
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态； 

一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。 
总之，就是让这个文件回到最近一次git commit或git add时的状态。

### git reset HEAD <file>
可以把暂存区的修改撤销掉（unstage），重新放回工作区。 
```
$ git reset HEAD readme.txt
Unstaged changes after reset:
M	readme.txt
```
git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。  
再用git status查看一下，现在暂存区是干净的，工作区有修改。   
假设你不但改错了东西，还从暂存区提交到了版本库，怎么办呢？还记得版本回退一节吗？可以回退到上一个版本。不过，这是有条件的，就是你还没有把自己的本地版本库推送到远程。还记得Git是分布式版本控制系统吗？我们后面会讲到远程版本库，一旦你把stupid boss提交推送到远程版本库，你就真的惨了……  

### 删除文件 （git rm file）
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
$ ssh-keygen -t rsa -C "youremail@example.com"
```
你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。  
如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。  
第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面。  

为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。  
最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。

### 添加远程库 和 git push
```
$ git remote add origin git@github.com:michaelliao/learngit.git
#origin 是你为远端仓库所起的名字，一般都是叫origin，其实你也可以要Ceres 或者Earth
# git@github.com:michaelliao/learngit.git  是你的远端仓库的真实地址          

$ git push -u origin master  #把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
```
我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
`$ git push origin master`

### 从远程库克隆（ git clone ）
git clone    -b {{develop}}   {ssh地址}
