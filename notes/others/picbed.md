# 图床

在Typora中利用PicGo自动上传图片到SM.MS图床

## 准备

1. install `Typora`，`PicGo`，`Git`，`Node.js`

   {% label Typora info %}

   {% label PicGo primary %}

   {% label Git warning %}

   {% label Node.js danger %}

2. register `sm.ms`

3. PicGo 安装 sm.ms 插件

   * app 中`插件设置`搜索 `smms-user`，安装即可

   * picgo 的官方文档写得易懂详细，推荐阅读（[PicGo-Doc](https://picgo.github.io/PicGo-Doc/zh/guide)）。



## PicGo & SM.MS

目的是把图床（SM.MS）的 API Access 给 PicGo。

SM.MS中：

​	-->`dashboard `

​	-->`API Token` 

​	-->click `Generate Secret Token `

​	copy `Secret Token`

PicGo中：

​	-->`图床设置 `

​	-->`SM.MS-登录用户 `

​	-->将 `Secret Token` 输入 `Auth`框内

 

## PicGo & Typora

目的是实现Typora中图片自动地通过 PicGo 上传到图床（SM.MS）。

Typora 中：

​	-->`文件` -->`偏好设置` -->`图像`

​	图像中各种设置的说明易懂，按需勾选即可。

   click `验证图片上传选项`

​	会弹出下图：

* （可能不会成功上传，但现在不要紧）

<img src="https://i.loli.net/2020/06/19/Gc93a52B6XbDxPL.png" alt="111" style="zoom: 67%;" />

​	copy 端口号。

PicGo 中：

​	-->`PicGo 设置` -->`设置 Server `

​	输入刚刚 copy 的端口号。

这时 Typora 中进行验证图片上传就可以成功，说明现在Typora中图片可以自动地通过 PicGo 上传到图床（SM.MS）了！

可以拖一张图片到 Typora 中试验一下。



## PicGo 快捷键

* PicGo 支持快捷键`command+shift+p`（macOS）或者`control+shift+p`（windows\linux）用以支持快捷上传剪贴板里的图片（第一张）。

* 支持自定义快捷键。
* 每次截图之后，按一下`ctrl+shift+p`，截图就可以直接上传到sm.ms图床上，并返回链接。



## 相关链接

1. [PicGo-Doc](https://picgo.github.io/PicGo-Doc/zh/guide)

2. [简书 各种错误排查](https://www.jianshu.com/p/4cd14d4ceb1d)