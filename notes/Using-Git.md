### intro to Git

What is Git?

[Git](https://git-scm.com/)是一个分布式版本控制系统（[Distributed Version Control System](https://en.wikipedia.org/wiki/Distributed_version_control)）

* 客户端并不只提取最新版本的文件快照， 而是把代码仓库完整地镜像下来，包括完整的历史记录。

* 特点：
  * 直接记录快照，而非差异比较；
  * 近乎所有操作都是本地执行；
  * Git 保证完整性；
  * Git 一般只添加数据；

* [关系图示](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)

  An image from ruanyifeng's blog is placed here for your convenience:

  <img src="./pics/git/relationships.png" width="700">

  

Git has excellent [documentation](http://git-scm.com/documentation) so we highly encourage those who are interested to read more about what will be summarized in the rest of this guide.

---

### Local Repositories  (Overview)

#### intro

三种状态：

* Git 有三种状态，你的文件可能处于其中之一：
  * `modified`：表示修改了文件，但还没保存到数据库中。
  * `staged`：表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。
  * `committed`：表示数据已经安全地保存在本地数据库中。
  
  <img src="./pics/git/areas.png" width=550 height=250>

This leads us to the three main sections of a Git project： the working tree, the staging area, and the
Git directory.

基本的 Git 工作流程如下：
1. 在工作区中修改文件。
2. 将你想要下次提交的更改选择性地暂存，这样只会将更改的部分添加到暂存区。
3. 提交更新，找到暂存区的文件，将快照永久性存储到 Git 目录。

#### Git Setup

1. Your Identity

   设置你的用户名和邮件地址

   ```bash
   $ git config [--global] user.name "John Doe"
   $ git config [--global] user.email "johndoe@example.com"
   ```

   Git的设置文件为`.gitconfig`，它可以在用户主目录下（全局配置），也可以在项目目录下（项目配置）。

2. Checking Your Settings

   ```bash
   # 列出所有 Git 当时能找到的配置
   $ git config --list
   ```

   

#### get a Git Repository

通常有两种获取 Git 项目仓库的方式：

1. 将尚未进行版本控制的本地目录转换为 Git 仓库；
2. 从其它服务器 **克隆** 一个已存在的 Git 仓库。

---

1. Initializing a Repository in an Existing Directory

   ```bash
   $ cd /c/user/my_project
   ```

   在当前目录新建一个Git代码库：

   ```bash
   $ git init
   ```

2. Cloning an Existing Repository

   * Git 克隆的是该 Git 仓库服务器上的几乎所有数据，而不是仅仅复制完成你的工作所需要文件。

   克隆仓库：

   ```bash
   $ git clone https://github.com/libgit2/libgit2
   ```

   这会在当前目录下创建一个名为 “libgit2” 的目录，并在这个目录下初始化一个 `.git` 文件夹， 从远程仓库拉取下所有数据放入 `.git` 文件夹，然后从中读取最新版本的文件的拷贝。 

   如果你想在克隆远程仓库的时候，自定义本地仓库的名字，你可以通过额外的参数指定新的目录名：

   ```bash
   $ git clone https://github.com/libgit2/libgit2 mylibgit
   ```

   这会执行与上一条命令相同的操作，但目标目录名变为了 `mylibgit`。

#### Tracked vs. Untracked Files

The Git documentation has an excellent section on [recording changes](http://git-scm.com/book/en/Git-Basics-Recording-Changes-to-the-Repository). An image from that section is placed here for your convenience:

<img src="./pics/git/lifecycle.png" width= 550 height=250>

* 如上图所示，你工作目录下的每一个文件都不外乎这两种状态：**tracked** 或 **untracked**。 

The following Git command allows you see the status of each file, i.e. whether it is untracked, unmodified, modified, or stageds:

```bash
$ git status
```

#### Staging & Committing

A *commit* is a specific snapshot of your working directory at a particular time. Users must specify what exactly composes the snapshot by *staging* files.

The `add` command lets you stage a file.

```bash
# 添加指定文件到暂存区
$ git add [file1] [file2] ...
# 添加指定目录到暂存区，包括子目录
$ git add [dir]
```

`git add` 命令使用文件或目录的路径作为参数；

* 如果参数是目录的路径，该命令将递归地跟踪该目录下的所有文件。

Once you have staged all the files you would like to include in your snapshot, you can commit them as one block with a message.

```bash
$ git commit -m MESSAGE
```

在提交了若干更新，又或者克隆了某个项目之后，你也许想回顾下提交历史。

 you can use the log command:

```bash
$ git log
```

The Git reference guide has a helpful section on [viewing commit history](http://git-scm.com/book/en/Git-Basics-Viewing-the-Commit-History) and filtering log results when searching for particular commits. It might also be worth checking out `gitk`, which is a GUI prompted by the command line.

#### Undoing Changes

The Git reference has a great section on [undoing things](http://git-scm.com/book/en/Git-Basics-Undoing-Things). Please note that while Git revolves around the concept of history, it is possible to lose your work if you revert with some of these undo commands. Thus, be careful and read about the effects of your changes before undoing your work.

* Unstage a file that you haven’t yet committed:

```bash
  $ git reset HEAD [file]
```

This will take the file’s status back to modified, leaving changes intact. Don’t worry about this command undoing any work. This command is the equivalent of deleting one of the temporary images that you’re going to combine into a panorama.

Why might we need to use this command? Let’s say you accidentally started tracking a file that you didn’t want to track. (an embarrassing video of yourself, for instance.) Or you were made some changes to a file that you thought you would commit but no longer want to commit quite yet.

* Amend latest commit (changing commit message or add forgotten files):

```bash
  $ git add [forgotten-file]
  $ git commit --amend
```

Please note that this new amended commit will replace the previous commit.

* Revert a file to its state at the time of the most recent commit:

```bash
  $ git checkout -- [file]
```

This next command is useful if you would like to actually undo your work. Let’s say that you have modified a certain `file` since committing previously, but you would like your file back to how it was before your modifications.

---

### Remote Repositories

#### Adding Remotes

Adding a remote repository means that you are telling git where the repo is located. 

```bash
$ git remote add [short-name] [remote-url]
```

The remote URL will look something like `https://github.com/berkeley-cs61b/skeleton.git` if you are using HTTP or `git@github.com:berkeley-cs61b/skeleton.git` if you are using SSH.

By convention, the name of the primary remote is called `origin` (for original remote repository). So either of the following two commands would allow me to add the `berkeley-cs61b/skeleton` repository as a remote.

```bash
$ git remote add origin https://github.com/berkeley-cs61b/skeleton.git
$ git remote add origin git@github.com:berkeley-cs61b/skeleton.git
```

After adding a remote, all other commands use its associated short name.

#### Renaming, Deleting, & Listing Remotes

- You can rename your remote by using this command:

  ```bash
    $ git remote rename [old-name] [new-name]
  ```

- You can also remove a remote if you are no longer using it:

  ```bash
    $ git remote rm [remote-name]
  ```

- To see what remotes you have, you can list them. The `-v` flag tells you the URL of each remote (not just its name).

  ```bash
    $ git remote -v
  ```

You can read more about [working with remotes](http://git-scm.com/book/en/Git-Basics-Working-with-Remotes) in the Pro Git book.

#### Cloning a Remote

There are often remote repos with code that you would like to copy to your own computer. In these cases, you can easily download the entire repo with its commit history by cloning the remote:

```bash
$ git clone [remote-url]
$ git clone [remote-url] [directory-name]
```

The top command will create a directory of the same name as the remote repo. The second command allows you to specify a different name for the copied repository.

When you clone a remote, the cloned remote because associated with your local repo by the name `origin`. This is by default because the cloned remote was the `origin` for your local repo.

#### Pushing Commits

You may wish to update the contents of a remote repo by adding some commits that you made locally. You can do this by `pushing` your commits:

```bash
$ git push [remote-name] [remote-branch]
```

Note that you will be pushing to the remote branch from the branch your `HEAD` pointer is currently referencing. For example, let’s say that I cloned a repo then made some changes on the `master` branch. I can give the remote my local changes with this command:

```bash
$ git push origin master
```

#### Fetching & Pulling Commits

There are also times that you’d like to get some new commits from a remote that are not currently on your local repo. For example, you may have cloned a remote created by a partner and wish to get his/her newest changes. You can get those changes by fetching or pulling from the remote.

- `fetch`: This is analogous to downloading the commits. It does not incorporate them into your own code.

  ```bash
    $ git fetch [remote-name]
  ```

  Why might you use this? Your partner may have created some changes that you’d like to review but keep separate from your own code. Fetching the changes will only update your local copy of the remote code but not merge the changes into your own code.

  For a more particular example, let’s say that your partner creates a new branch on the remote called `fixing-ai-heuristics`. You can view that branch’s commits with the following steps:

  ```bash
    $ git fetch origin
    $ git branch review-ai-fix origin/fixing-ai-heuristics
    $ git checkout review-ai-fix
  ```

  The second command creates a new branch called `review-ai-fix` that *tracks* the `fixing-ai-heuristics` branch on the `origin` remote.

- `pull`: This is equivalent to a `fetch + merge`. Not only will `pull` fetch the most recent changes, it will also merge the changes into your `HEAD` branch.

  ```bash
    $ git pull [remote-name] [remote-branch-name]
  ```

  Let’s say that my boss partner has pushed some commits to the `master` branch of our shared remote that fix our AI heuristics. I happen to know that it won’t break my code, so I can just pull it and merge it into my own code right away.

  ```bash
    $ git pull origin master
  ```

---

### Extra Reading

1. [Git Documentation](http://git-scm.com/doc) is really quite good and clear, and there is a great Pro Git book by Scott Chacon.
2. [Hacker’s Guide to Git](http://wildlyinaccurate.com/a-hackers-guide-to-git) is a very friendly introduction to how Git works. It gives a peek at the structure of commits & branches and explains how some commands work.
3. [Git Magic](http://www-cs-students.stanford.edu/~blynn/gitmagic/) is a fun and useful turtorial.
4. [Using Git Guide](https://sp19.datastructur.es/materials/guides/using-git.html) is very good and friendly to beginners, and written by Sarah Kim. 
   * 本文其实是这篇文章的总结归纳。
5. [猴子都能懂的GIT入门](https://backlog.com/git-tutorial/cn/)：寓教于乐。
6. [Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)：廖雪峰老师的Git教学。
7. [Git cheat sheet](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)：阮一峰老师总结的常用Git命令清单，非常实用。







