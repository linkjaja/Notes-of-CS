# Git 设置ssh密钥

git支持https和git两种传输协议：

* git使用https协议，每次pull, push都会提示要输入密码，使用git协议，然后使用ssh密钥，这样免去每次都输密码的麻烦。

初次使用git的用户要使用git协议大概需要三个步骤：

1. 生成密钥对
2. 设置远程仓库（本文以github为例）上的公钥
3. 把git的 remote url 修改为git协议

## 生成密钥对

大多数 Git 服务器都会选择使用 SSH 公钥来进行授权。系统中的每个用户都必须提供一个公钥用于授权，没有的话就要生成一个。生成公钥的过程在所有操作系统上都差不多。

首先你要确认一下本机是否已经有一个公钥。

* SSH 公钥默认储存在账户的主目录下的 ~/.ssh 目录。进去看看：

```bash
$ cd ~/.ssh
$ ls # 列出当前目录下的所有文件和目录
id_rsa   known_hosts   id_rsa.pub
```

看一下有没有`id_rsa`和`id_rsa.pub`(或者是`id_dsa`和`id_dsa.pub`之类成对的文件)，有 .pub 后缀的文件就是公钥，另一个文件则是密钥。

* 假如没有这些文件，甚至连 .ssh 目录都没有，可以用 `ssh-keygen `来创建新的ssh key：

```bash
$ ssh-keygen -t rsa -C "your_email@youremail.com"

Creates a new ssh key using the provided email 
# Generating public/private rsa key pair.

Enter file in which to save the key (/home/you/.ssh/id_rsa):
```

按Enter。

然后，会提示你输入密码，如下(输一个，会安全一点，但是之后每次pull, push都会要求输入这个密码；若不输入，直接回车，就少了一点安全，但是省去了麻烦)：

```bash
Enter same passphrase again: [Type passphrase again]
```

完成之后，大概是这样显示：

```
Your public key has been saved in /home/you/.ssh/id_rsa.pub.
The key fingerprint is: # 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@youremail.com
```

到此为止，本地的密钥对就生成了。

## 添加公钥到你的远程仓库（github）

1. 查看刚刚生成的公钥：

```bash
$ cat ~/.ssh/id_rsa.pub
# 显示文件中的内容
```

2. 登陆GitHub帐户, user settings ` ->` SSH and GPG keys ` -> ` New SSH key

3. 然后复制上面的公钥内容，粘贴进“Key”文本域内。 title域，自己随便起个名字。
4.  Add key。

验证下这个key是不是正常工作：

```bash
$ ssh -T git@github.com
Attempts to ssh to github
```

如果，看到：

```bash
Hi xxx! You've successfully authenticated, but GitHub does not # provide shell access.
```

说明设置成功了。

## 修改git的remote url

使用命令 `git remote -v `查看你当前的 remote url：

```bash
$ git remote -v
origin https://github.com/someaccount/someproject.git (fetch)
origin https://github.com/someaccount/someproject.git (push)
```

如果是以上的结果那么说明此项目是使用https协议进行访问的（如果地址是git开头则表示是git协议）

* 你可以登陆GitHub，在上面可以看到ssh协议相应的url，复制此ssh链接，然后使用命令` git remote set-url `来调整url：

```bash
git remote set-url origin git@github.com:someaccount/someproject.git
```

然后你可以再用命令 `git remote -v` 查看一下，url是否已经变成了ssh地址。

配置完成。

