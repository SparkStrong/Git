[toc]

# 关于Gitlab若干权限问题
## 访问权限 - Visibility Level
在建立项目时就需要选定的(后期可修改)，主要用于决定哪些人可以访问此项目，包含3种。
+ Private - 私有，只有属于该项目成员才有权限查看
+ Internal - 内部，用个Gitlab账号的人都可以clone
+ Public - 公开，任何人可以clone

## 行为权限
行为权限是指对该项目进行某些操作，比如提交、创建问题、创建新分支、删除分支、创建标签、删除标签等，行为权限的前提是具有访问权限。

## 角色
Gitlab定义了以下几个角色:  
+ Guest - 访客
+ Reporter - 报告者; 可以理解为测试员、产品经理等，一般负责提交issue等
+ Developer - 开发者; 
+ Master - 主人; 一般是组长，负责对Master分支进行维护
+ Owner - 拥有者; 

## 权限
不同角色，拥有不同权限。  

> ==对于我们实验室使用来说，一般只需要区分master和developer就行了，Master负责维护master分支（默认的保护分支，一般用于放稳定版本），普通开发者授予developer权限就行了.==


## 成员添加和权限分配

+ 进入项目，点击`members`，添加成员`Add member`;
   + 选择要添加的成员;
   + 授予的权限，一般都授予`Developer`;
   + 期限，默认为空就行
   > ![image](http://note.youdao.com/yws/public/resource/b77392b99ba58e5542f90e339350594f/xmlnote/84EFB06B2F9F4D7BACEE1EC1E9ACB0D4/2977)
   > ![image](http://note.youdao.com/yws/public/resource/b77392b99ba58e5542f90e339350594f/xmlnote/F9F0EB7FF7ED47DDAC0A031548FE26C6/2988)

# 分支管理

## 项目分支设置
+ master  作为稳定分支，存放稳定版本的代码并设置标签方便区分，master和owner进行维护
+ develop 新功能开发分支，所有开发者都能往该分支merge和push，由master将该分支代码向master分支合并，或者也可以将此分支设置为保护分支，视情况考虑；
+ own dev 每个开发者自己本地的新功能分支，在本地进行新功能开发时，先建立新的分支，开发完成后往develop进行合并，然后merge到develop分支；
+ 用下图来解释更生动形象：
    > ![image](https://camo.githubusercontent.com/64ee45ca6222cfce64ec679d18b0c9e6ab0862d0/687474703a2f2f7777772e6c69616f78756566656e672e636f6d2f66696c65732f6174746163686d656e74732f30303133383439303932333933393064333535656230376439643634333035623633323261616634656461633165333030302f30)

  + 这样开发的好处是保持了项目整体上稳定，然后每个开发者又有自己的空间。
  + 自己的分支就相当于你的小庭院，种点花养个猫，都随意啦，不要让人看见就好，你要是不介意别人看当然也可以提交到远程，但是建议自己的小庭院自己知道就好。
+ Tips
  > 合并分支时，加上**--no-ff**参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

## 设置保护分支
+ 选择工程，点击Settings,然后点击Repository，选择Protected Branches,EXpand进行设置就可，可以增加保护分支也可以将某些保护分支不再保护。
> ![image](http://note.youdao.com/yws/public/resource/b77392b99ba58e5542f90e339350594f/xmlnote/A88EFC74B1AD4F93B2BBB0152C21182F/3028)

## 操作演示
1. 添加成员并赋予相应角色权限
2. 拉取代码进行开发：
   + `git clone http://192.168.5.235/zhouwang/learngit.git`
   + `git branch -r`  // 查看远程仓库分支设置情况
   + `git checkout origin/develop` // 选择远程的develop分支继续开发，也可以根据tag进行选择 `git checkout -b branch_name tag_name`
   + `git checkout mybranch`  // 在开发分支的基础上创建自己的新分支进行功能开发
   + ..... 进行一些开发工作
   + `git checkout develop` // 转到develop分支
   + `git merge mybranch`  // 将mybranch分支合并到develop分支
   + `git push origin develop:develop` // 本地develop分支推送到远程develop分支
   + `git branch -d mybranch` // 删除mybranch分支，==可选操作，以下操作都非必须==
   + `git tag -a v1.0 -m "version 1.0"` // 设置标签
   + `git push --tags`  // 推到远端
   + `git push origin develop:master` // 尝试将本地develop分支推送到远程，正常情况会发现失败
