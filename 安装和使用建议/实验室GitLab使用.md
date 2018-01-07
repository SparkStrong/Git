[toc]

![image](https://www.liaoxuefeng.com/files/attachments/0013848605496402772ffdb6ab448deb7eef7baa124171b000/0)
# 基本概念
+ Git是什么？  Git是目前世界上最先进的分布式版本控制系统（没有之一）。  

下面进入正题。

## 集中式vs分布式

集中式的版本控制系统，版本库集中存放在中央服务器，下图可以简单的描述这种管理方式。
![image](https://www.liaoxuefeng.com/files/attachments/001384860735706fd4c70aa2ce24b45a8ade85109b0222b000/0)

缺点：服务器必须启动；使用者必须能够访问服务器，必须要有网；  
优点：权限控制

分布式版本控制系统不需要连网也能工作，先在本地的仓库中改着，等有网了再上传到服务器。分布式的版本控制系统也比较安全，每个开发者的电脑上都有完整的版本库，某个人的电脑坏了没有关系。
每两个人之间都能进行版本库推送，但这种方式太麻烦了，所以我们建一个“中央服务器”就好了。
![image](https://www.liaoxuefeng.com/files/attachments/0013848607465969378d7e6d5e6452d8161cf472f835523000/0)

## 工作区和暂存区
Git分为工作区和版本库，其中版本库包括一个暂存区Stage和一个Master，HEAD指针指向Mater。 工作区，是还未进行add和commit的文件，此时的通过git status查看，这样的文件是untracked的。

当执行add时，将工作区的文件add到Stage中，接着使用commit就会将stage区中的文件提交到Master分支中。 关系如下图所示。  
![image](https://camo.githubusercontent.com/38ed908d5798214b76d027c60d0fdbd9622d429f/687474703a2f2f7777772e6c69616f78756566656e672e636f6d2f66696c65732f6174746163686d656e74732f30303133383439303737323034353865353637353164663163343734343835623639373537353037336334306165393030302f30)

# 基本使用

## 1. 注册用户
    网址： http://192.168.5.235
    使用常见的邮箱和密码就可以注册。
备注：用户名尽量使用真实姓名的拼音或者可以让大家很容易就分的清楚的昵称。

## 2. 创建工程（仓库）
![image](http://note.youdao.com/yws/public/resource/2b280f6acf38b79cd52e050dd8749252/xmlnote/9830DAAB747047CB889AD3B6A99FE89E/2648)

+ 输入工程名   learngit
+ 工程描述  学习使用git
+ 设定访问权限 - Visibility Level    &emsp;&emsp;推荐使用Private，方便进行权限管理
+ 确定创建
+ 创建成功

![image](http://note.youdao.com/yws/public/resource/2b280f6acf38b79cd52e050dd8749252/xmlnote/FC27E544C6AE42EDBB74D767701A8199/2755)

## 3. 从远程库克隆（以下在Windows环境下进行示范）
3.1. 安装git. &emsp;参见教程：[《安装Git》](http://note.youdao.com/noteshare?id=01deece937082a3765ac0d58a356f1af&sub=825D72C6BFFB44D8BC9761A9982BF879)  
3.2. 使用`git clone`克隆本地库；
+ 在想要放置该仓库的地方打开`Git Bash`(Git Bash中类似于Linux环境，比较方便使用)
+ 在Gitlab网站复制得到工程(仓库)的路径;
> ![image](http://note.youdao.com/yws/public/resource/2b280f6acf38b79cd52e050dd8749252/xmlnote/4B5C016C76AE4A528E8D1240952330A2/2771)
+ 在`Git Bash`中输入`git clone http://10.108.139.133/zhouwang/learngit.git`，等待将远程的版本库拉取到本地；
    + 备注：可能会提示我们输入用户名和密码；
    > ![image](http://note.youdao.com/yws/public/resource/2b280f6acf38b79cd52e050dd8749252/xmlnote/2482799E91B24865B714FFD25C25A4AE/2785)
+ 拉取到本地并查看；
> ![image](http://note.youdao.com/yws/public/resource/2b280f6acf38b79cd52e050dd8749252/xmlnote/E5626C77697A40968856BEABAF4D76A1/2788)

## 4. 开发
+ 新建一个文件“git_commands.md”
+ `git status`
  + 使用`git status`查看一下状态，必须要进入到含有.git目录下，这相当于一个工作区的概念，只有在这个区域内Git才能发挥作用；
   + 比如第一次输入`git status`会提示错误，第二次才成功；
   > ![image](http://note.youdao.com/yws/public/resource/2b280f6acf38b79cd52e050dd8749252/xmlnote/501F6E4481734D21BB7B9D6688A364AC/2832)
+ `git add <file>`
   + 提示我们使用`git add <file>...`进行添加，我们先在文件中写点内容；
   + `git add git_commands.md`
   + 再次输入`git status`查看一下状态，非必须操作；
+ `git commit`
   + 因为我们还没有对git进行过任何设置，所以这次commit会提示一些错误，我们设置一下就行；
   + `git config user.email "zwstrong@126.com"`
   + `git config user.name "zhouwang"`
   + `git commit -m "增加git_commands.md文件并写了两条命令"`
   > ![image](http://note.youdao.com/yws/public/resource/2b280f6acf38b79cd52e050dd8749252/xmlnote/E41FD624A50D487F8C2CADB04B5FBD29/2857)
+ `git push`
   + `git push`命令用于将本地分支的更新，推送到远程主机；
   + `git push origin master:master` 将本地的master分支推送到origin的master分支；
   > ![image](http://note.youdao.com/yws/public/resource/2b280f6acf38b79cd52e050dd8749252/xmlnote/1B093426A6FE49B69F76E9854EB01CD4/2886)

## 5. 同步远程的更新
+ `git fetch`
   + 取回远程版本库的内容，但是不会自动合并到本地仓库；
   > `git fetch <远程主机名> <分支名>`  
   > `git fetch origin master`
   + 可以使用`git diff`或者`git status`看下版本之间的差异，推荐使用`git diff`;
+ `git diff`
   + 比较版本之间差异
   + git diff master origin/master  比较本地master与远程master的区别
+ `git merge`
   + 合并分支
   + `git merge origin/master`  将刚拉取到的远程master分支合并到本地master上

以上操作的截图：
> ![image](http://note.youdao.com/yws/public/resource/2b280f6acf38b79cd52e050dd8749252/xmlnote/FC8A3CD02407470C9F09FD30E8E4FF43/2914)
> ![image](http://note.youdao.com/yws/public/resource/2b280f6acf38b79cd52e050dd8749252/xmlnote/D130C892D2094317B6164DD03A1B5F8B/2929)