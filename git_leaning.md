## Git 命令理解
参考 http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/
http://blog.chinaunix.net/uid-25806493-id-3328322.html
```
The most commonly used git commands are:
  - add        Add file contents to the index
  - bisect     Find by binary search the change that introduced a bug
  - branch     List, create, or delete branches
  - checkout   Checkout a branch or paths to the working tree
  - clone      Clone a repository into a new directory
  - commit     Record changes to the repository
  - diff       Show changes between commits, commit and working tree, etc
  - fetch      Download objects and refs from another repository
  - grep       Print lines matching a pattern
  - init       Create an empty Git repository or reinitialize an existing one
  - log        Show commit logs
  - merge      Join two or more development histories together
  - mv         Move or rename a file, a directory, or a symlink
  - pull       Fetch from and integrate with another repository or a local branch
  - push       Update remote refs along with associated objects
  - rebase     Forward-port local commits to the updated upstream head
  - reset      Reset current HEAD to the specified state
  - rm         Remove files from the working tree and from the index
  - show       Show various types of objects
  - status     Show the working tree status
  - tag        Create, list, delete or verify a tag object signed with GPG
```

按照个人理解优先级理解：
---
+ **git clone** 克隆一个仓库。  Git能在许多协议下使用，所以Git URL可能以ssh://, http(s)://, git://,或是只是以一个用户名（git 会认为这是一个ssh 地址）为前辍. 有些仓库可以通过不只一种协议来访问，例如，Git本身的源代码你既可以用 git:// 协议来访问：git clone git://git.kernel.org/pub/scm/git/git.git
也可以通过http 协议来访问:git clone http://www.kernel.org/pub/scm/git/git.git
git://协议较为快速和有效,但是有时必须使用http协议,比如你公司的防火墙阻止了你的非http访问请求.如果你执行了上面两行命令中的任意一个,你会看到一个新目录: 'git',它包含所有的Git源代码和历史记录.
在默认情况下，Git会把"Git URL"里目录名的'.git'的后辍去掉,做为新克隆(clone)项目的目录名: (例如. git clone http://git.kernel.org/linux/kernel/git/torvalds/linux-2.6.git 会建立一个目录叫'linux-2.6')
+ **git init**  将当前工作目录变成Git可以管理的仓库，Git的版本控制管理之下。会生成.git 的隐藏文件夹标志成功。
+ **git status** 获取仓库当前状态，哪些文件被暂存了(就是在你的Git索引中), 哪些文件被修改了但是没有暂存（git add）, 还有哪些文件没有被跟踪(Untracked).
    ``` 
    $ git status
    On branch master          //默认就直接在 master 分支

    Initial commit

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

            README.md
            git_leaning.md

    nothing added to commit but untracked files present (use "git add" to track)
    ```

+ **git add** 不但是用来添加不在版本控制中的新文件，也用于添加已在版本控制中但是刚修改过的文件; 在这两种情况下, Git都会获得当前文件的快照并且把内容暂存(stage)        到索引中，为下一次commit做好准备。Git跟踪的是内容不是文件。
      warning: LF will be replaced by CRLF in README.md.    // http://blog.csdn.net/feng88724/article/details/11600375
      The file will have its original line endings in your working directory.
+ **git diff** 比较自己项目中任意两个版本的差异，或是用来查看别人提交进来的新分支。显示在当前的工作目录里的，没有staged(添加到索引中)，且在下次提交时不会被提交的修改。如有合并的文件有冲突，输入此命令就可以查看当前有哪些文件产生了冲突。
  + “git diff test”——这会显示你当前工作目录与另外一个叫'test'分支的差别。你也以加上路径限定符，来只比较某一个文件或目录。
  + “git diff master..test”——这条命令只显示两个分支间的差异，如果你想找出 “git diff master... test”——这条命令显示‘master’,‘test’的共有父分支和'test'分支之间的差异，用3个‘.'来取代前面的两个'.' 。
  + “git diff --cached”——看看哪些文件将被提交(commit)。显示你当前的索引和上次提交间的差异；这些内容在不带"-a"参数运行 "git commit"命令时就会被提交。
  + “git diff HEAD”——上面这条命令会显示你工作目录与上次提交时之间的所有差别，这条命令所显示的 内容都会在执行"git commit -a"命令时被提交。
  + “git diff HEAD -- ./lib”——上面这条命令会显示你当前工作目录下的lib目录与上次提交之间的差别(或者更准确的 说是在当前分支)。
  + “git diff --stat”——不查看每个文件的详细差别，只是统计一下有哪些文件被改动，有多少行被改动。
+ **git commit** 把暂存区中记录的要提交的内容提交到Git的对象数据库。这会提示你输入本次修改的注释，完成后就会记录一个新的项目版本。
  + "git commit -a"——这会自动把所有内容被修改的文件(不包括新创建的文件)都添加到索引中，并且同时把它们提交。
  + “git commit -m”——后跟参数表示要接提交内容说明的信息。
+ **git pull**
+ **git push**
+ **git fetch**
+ **git checkout**
