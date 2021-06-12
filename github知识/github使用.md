## github使用

* 注册github，创建github仓库

* 安装git

* 创建github仓库

* 提交代码

  

## 注册github

* 打开[github.com][https://github.com]，注册github账号
* 注册成功后在页面上方用户菜单上选择`+` `->`New repository ,创建一个新的仓库，为仓库填入一个名字，点击创建，将创建一个新的仓库



## 安装git客户端

* 因为github是一个服务端，想要在自己电脑上使用git我们还需要一个git客户端

* windows安装：[windows-git-下载地址][https://git-scm.com/download/win]

* mac安装：[mac-git-下载地址][https://git-scm.com/download/mac]

* linux安装：[linux-git-下载地址][https://git-scm.com/download/linux]

* 安装一路next，可以选择自己想要安装的目录比如`D:\soft\git`目录下，安装完成后右键鼠标会出现如：git bash、git gui，说明安装成功

  

## 配置git

* 现在自己电脑项目目录新建一个mytest目录，命令行进入mytest目录

  1. 执行下面命令：

     ```she
     git init
     ```

     执行效果输出：

     Initialized empty Git repository in 你的项目地址/mytest.git/

  2. 在本地创建ssh  key 

     ```she
     ssh-keygen -t rsa  -C "your_eamil@youremail.com"
     ```

     后面的邮箱是github注册时的邮箱。

     后续一路按回车（也可以输入密码，这个要记住），之后会生成ssh key 生成成功

     然后进入提示的地址查看ssh key 文件，比如：`C:\user\diff\.ssh`,diff是当前电脑的名称，打开id_rsa.pub，复制里面的内容

     回到github网站，进入Account Settings -> ssh key  -> add  ssh key ,填个title标记，粘贴key，点击确定。

  3. 验证是否成功，在命令行输入

     ```she
     ssh -T git@github.com
     ```

     回车看到返回：you ...successfully ...  表示成功了

* 上传代码到github仓库

  1. 需要配置username 和 email

     ```shel
     git config  --global user.name ”你的名字“
     git config  --global user.email "你的邮箱地址"
     ```

  2. 添加远程地址

     ```she
     git remote add origin git@github.com:yourname/youRepo.git 
     ```

     yourname = 你github 上的用户名，youRepo = 你刚刚创建的 仓库。

  3. 提交代码

     创建文件readme.md 执行命令

     ```she
     git add readme.md 
     git commit -m "第一次提交代码"
     ```

     上传到github,push 会把本地仓库推送到远程github服务器

     ```she
     git push origin main
     ```



## gitignore文件

* gitignore 是告诉git要忽略的文件





