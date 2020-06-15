# 网站搭建

## 组成部分

1. 框架
2. web服务器
3. 图床
4. 域名备案
5. DNS解析
6. 页面美化
7. 评论功能
8. 流量统计

## 框架

* 静态：Hexo、Jekyll、Octopress、Hugo
* 动态：WordPress、FarBox、Ghost

### **安装Node.js**

Hexo基于Node.js。

npm是Node.js的包管理工具（package manager）。

注意安装Node.js会包含环境变量及npm的安装，安装后，检测Node.js是否安装成功，检查安装版本，命令行输入`node --version`，可以看到Node.js的版本，同理，看一下npm是否安装成功。

### 安装Hexo

Hexo是博客的框架。

电脑中任选盘符新建一个文件夹作为博客网站的根目录，文件名好不要是中文。

进入该文件夹，空白处右键点击`Git Bash here`

* 使用npm命令安装Hexo：

```bash
$ npm install -g hexo-cli 
```

* 安装完成后，初始化我们的博客、创建根目录：

```bash
$ hexo init <根目录名>
```

此时Hexo框架的本地搭建已经完成了。为了检测网站雏形，在根目录下，依次输入命令：

```bash
# hexo g == hexo generate #生成网页
$ hexo g
#hexo s == hexo server #启动服务预览
$ hexo s
```

浏览器中打开http://locakhost:4000或者127.0.0.1:4000
若可以看到网页，说明Hexo博客已经成功在本地运行。



## web服务器

Github Page托管，新建一个Repo，仓库名称必须为：`<user>.github.io`

### ssh密匙

省去输入账号密码的麻烦

[Git 设置ssh密钥](./notes/others/setting_SSH_keys.md)

### 网站配置文件

站点根目录下的`_config.yml`文件是**站点配置文件**。

修改一下title跟url等，url修改为`https://<用户名>.github.io`，例如我的用户名是example的话，就应该输入`https://example.github.io`

* 安装Git部署插件，输入命令：

```bash
npm install hexo-deployer-git --save
```

拉到文件最底部，对deploy的repo项 和branch项做修改：

```bash
type: git
repo: git@github.com:<Github用户名>/<github用户名>.github.io.git
branch: master
```

保存站点配置文件。

* 其实就是给hexo d 这个命令做相应的配置，让hexo知道你要把博客部署在哪个位置，很显然，我们部署在我们GitHub的仓库里。

最后，生成页面上传至Github，依次输入：

```bash
#清除缓存，若是网页正常情况下可以忽略这条命令
$ hexo clean 
# 生成网页
$ hexo g 
# 部署网站
$ hexo d
```


上传完成后，浏览器打开`https://<用户名>.github.io`查看网页，如果页面变成了之前本地调试时的样子，说明网站已经上线，可以在网络上被访问了。

## 域名与解析

现在网页已经部署上了服务器，但是只能通过服务器绑定的IP地址访问站点。这种域名相对难以记忆，这时，就可以绑定个性化域名。

### 购买域名

* 域名代理厂商（国内）：阿里云万网，腾讯云。

注意：在国内购买域名，需要进行实名认证，一些特定的域名（.com/.site）需要进行域名备案。

### DNS解析

* 域名管理

在域名列表中，进入解析，添加解析记录

1. 类型：`CNAME`；记录值格式：`<github用户名>.github.io`；主机记录：`www`；解析路线：`default`；
2. 类型：`A`；记录值格式：`解析IP地址`；主机记录：`@`；解析路线：`default`；
   * ping  `<github用户名>.github.io`，即可知IP地址。
   * 也可以使用在线DNS查询工具，这里推荐[IPIP.NET](https://tools.ipip.net/dns.php)。

* 设置GitHub Pages

进入托管网站的GitHub repository，-->settings，-->GitHub Pages，--->Custom domain，输入购买的个性化域名，举例：

```test
latehour.site
```

* 设置本地站点源文件

进入本地站点根目录，在`./source`目录下，创建记事本，写入之前购买的个性化域名，举例：

```test
latehour.site
```

保存为CNAME，注意该文件无后缀。

最后，生成页面上传至Github，依次输入：

```bash
$ hexo clean 
$ hexo g 
$ hexo d
```

现在网站可以通过个性化域名访问。



原理

设置对应DNS解析，目的是告诉所有访问这个域名的浏览器，应该访问哪个IP地址的主机。

* DNS过程简述：
  1. 用户主机上运行着DNS的客户端，即我们的PC或手机客户端运行着DNS客户端。
  2. 浏览器将接收到的URL中抽取出域名字段，就是访问的主机名，比如`http://www.baidu.com/`, 并将这个主机名传送给DNS应用的客户端。
  3. DNS客户端向DNS服务器发送一份查询报文，报文包括：要访问的主机名字段（包括一些列缓存查询，分布式DNS集群的工作）
  4. 该DNS客户端最终会收到一份回答报文，其中包含有该主机名对应的IP地址。
  5. 一旦该浏览器收到来自DNS的IP地址，就可以向该IP地址定位的HTTP服务器发起TCP连接。



## 配置SSL证书

HTTPS 相比HTTP 增加了一层加密，用于防止其他人窥探或篡改您的站点的流量。 

* GitHub Pages 站点可以强制实施 HTTPS，从而将所有 HTTP 请求透明地重定向到 HTTPS。

具体如下：

1. 在 GitHub 上，导航到站点的仓库。
2. 在仓库名称下，单击 **Settings（设置）**。
3. Under "GitHub Pages", select **Enforce HTTPS**.



## 界面美化

补theme，plugins，icon

