# 本地项目上传至GitHub云仓库

## 通过git上传(use https)

1. 打开git bash的几种方式
   
* 在git bash里打开目标文件夹 or 在目标文件夹右键 `git bash here`
   
2. 输入命令

   ``` git
   git init
   ```

   目标文件夹中会出现名为.git的隐藏文件夹

3. 目标文件夹此时就是本地的Git仓库，可以往本地仓库内添加项目，或进行项目的改动；之后通过git add命令把项目添加到项目上

   ``` git
   git add .
   ```

4. 用git commit命令把项目提交到本地仓库

   ``` git
   git commit -m"注释内容"
   ```

5. 关联云仓库

   ``` git
   git remote add origin https://github.com/用户名/云仓库名.git
   ```

   * origin后跟云仓库的https地址

6. 推送

   ``` git
   git push -u origin master
   ```
   * 报错1云仓库与本地仓库不统一，需要先把云仓库的文件pull下来本地。通过命令git pull实现，再上传。

   ``` git
   git pull --rebase origin master
   ```

   