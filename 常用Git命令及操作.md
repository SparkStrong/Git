1. git status   查看状态
2. git clone http://192.168.5.235/zhouwang/learngit.git   // 拉取代码
3. git add <file>....    // git add git_commands.md 
4. git commit -m "提交说明，尽量做到有效备注"
5. git config user.email "youremail.com"  // 设置邮箱
6. git config user.name "yourname"   // 设置该项目的用户名
6. git push <远程主机名> <本地分支名>:<远程分支名>  // 推送代码到远程仓库
7. git push origin develop:develop  // 推送本地develop到远程develop分支
7. git branch  查看当前所在分支
8. git branch <branch_name> // 创建分支
8. git branch -a 查看本地以及远程所有分支
9. git branch -r 查看远程所有分支
10. git fetch <远程主机名> <分支名>   // 获取更新但不自动合并到本地分支
10. git checkout -b develop  // 创建并切换到分支develop
11. git checkout <branchname>  // 切换分支
13. git checkout origin/develop // 切换到远程的develop分支进行工作
14. git checkout -b branch_name tag_name // 根据标签名选择分支进行开发
15. git tag -a v1.0 -m "version 1.0" // 设置标签
16. git push --tags // 推到标签到远端
17. git remote add origin <url> // 添加远程库
18. git push -u origin master  // 首次将本地库推送到远程



参考教程：[《廖雪峰Git教程》](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
