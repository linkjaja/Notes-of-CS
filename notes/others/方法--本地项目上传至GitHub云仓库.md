# 本地项目上传至GitHub云仓库

## 通过git上传(use https)

1. 打开git bash的几种方式
   
* 在git bash里打开目标文件夹 or 在目标文件夹右键 `git bash here`
  
2. 输入命令

   ``` bash
   git init
   ```

   目标文件夹中会出现名为.git的隐藏文件夹，也就是本地的Git仓库。

3. 目标文件夹此时就是本地的工作区，可以往工作区内添加项目，或进行项目的改动；之后通过git add命令把项目添加到暂存区内

   ``` bash
   git add .
   ```

4. 用git commit命令将暂存区的项目提交到本地仓库

   ``` bash
   git commit -m"注释内容"
   ```

5. 关联远程云仓库（非初次可跳过）

   ``` bash
   git remote add origin https://github.com/用户名/云仓库名.git
   ```

   * origin后跟云仓库的https地址

   * 报错1 git添加远程库时出现`fatal:remote origin already exists`，通过先删除origin库，然后再次添加即可。

     ```bash
     git remote rm origin
     ```

     

6. 推送

   ``` bash
   git push -u origin master
   ```
   * 报错1云仓库与本地仓库版本不统一，需要先把云仓库的文件pull下来本地。通过命令git pull实现，再上传。

   ``` bash
   git pull --rebase origin master
   ```

   
