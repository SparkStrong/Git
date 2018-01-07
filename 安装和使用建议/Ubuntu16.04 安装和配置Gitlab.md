[toc]

## 安装Ubuntu16.04 64位的长期支持版
推荐在VM Ware或者Xen Center上安装虚拟机作为实验，等确定会安装了在装在物理机上也不迟。

## 更换源（非必须但强烈推荐）
更换成阿里的或者清华的源，可以更方便的使用Ubuntu系统。以下操作基于Ubuntu16.04 64位LTS桌面版。

+ 确保能上网，连上百度
+ 点击系统设置，然后点击`Software&Updates`
  > ![image](http://note.youdao.com/yws/public/resource/b77392b99ba58e5542f90e339350594f/xmlnote/F47EF8C13B164D378E8BF0778C43D248/3274)
+ 选择`Ubuntu Software`, `Download from`，点击`other...`
  > ![image](http://note.youdao.com/yws/public/resource/b77392b99ba58e5542f90e339350594f/xmlnote/3288901501A84C9CBFE32181B7C924EB/3278)
+ 点击`Select Best Server`，然后等待
  > ![image](http://note.youdao.com/yws/public/resource/b77392b99ba58e5542f90e339350594f/xmlnote/81DFDF247F28408AB2EB3846384F69E0/3291)
  > ![image](http://note.youdao.com/yws/public/resource/b77392b99ba58e5542f90e339350594f/xmlnote/62EF918AD0CF4CFC824F06D2E3FBACE2/3289)

+ 结束后点击`Choose Server`，在弹出的提示框中输入密码，点击`Authenticate`就可
 > ![image](http://note.youdao.com/yws/public/resource/b77392b99ba58e5542f90e339350594f/xmlnote/042503801E3E47438B605F5EF853D0AE/3302)

+ 发现源已经被更改，点击关闭就可
 > ![image](http://note.youdao.com/yws/public/resource/b77392b99ba58e5542f90e339350594f/xmlnote/3B7F6CDF56B94FB5B3C70879941780DD/3305)

+ 随后点击关闭或者重新载入都可以。

此时可以打开控制台输入一些指令进行测试，比如:  
> sudo apt-get install update  
sudo apt-get install upgrade

==备注：以上更换源的方法也常用来解决ubuntu中`sudo apt-get install update`失败的情况。==

## 安装Gitlab

+ [访问Gitlab官网](https://www.gitlab.com.cn/)，选择安装
  > ![image](http://note.youdao.com/yws/public/resource/b77392b99ba58e5542f90e339350594f/xmlnote/59D9A782CC2A419D9C4BFAD0D937549B/3321)
+ 选择对应版本的安装指导
  > ![image](http://note.youdao.com/yws/public/resource/722077cb8c9269531b965c69788ed13a/xmlnote/F952D7DE941444058ECC53D8702D42C6/3327)
+ Ubuntu安装指南，进行如下的三步操作就可，先不要执行配置和启动Gitlab
  > ![image](http://note.youdao.com/yws/public/resource/722077cb8c9269531b965c69788ed13a/xmlnote/783C0AB87CD3455CA09977BE080FBCDD/3333)

## Gitlab配置

### 配置Gitlab IP
进入 `/etc/gitlab/`(`cd /etc/gitlab/`)目录，打开`gitlab.rb`(`sudo gedit gitlab.rb`或者`sudo vim gitlab.rb`)，将`externval_url`之后的域名，修改成本机IP，例如：
> ![image](http://note.youdao.com/yws/public/resource/722077cb8c9269531b965c69788ed13a/xmlnote/3DD9DAC3122F4AD2BBFFD2622E9957EF/3355)

### 修改邮件配置 (非必须)
同上，要修改`/etc/gitlab/gitlab.rb`文件，增加如下配置：
> ![image](http://note.youdao.com/yws/public/resource/722077cb8c9269531b965c69788ed13a/xmlnote/E8CD1A3C19EB4DBC8BF86DB052E7837D/3363)

gitlab_rails['smtp_enable'] = true  
gitlab_rails['smtp_address'] ="smtp.163.com"  
gitlab_rails['smtp_port'] = 25  
gitlab_rails['smtp_user_name'] = "替换为自己的163邮箱"  
gitlab_rails['smtp_password'] = "替换为自己的163授权码"  
gitlab_rails['smtp_domain'] ="163.com"  
gitlab_rails['smtp_authentication']="login"  
gitlab_rails['smtp_enable_starttls_auto'] =true
+ 修改gitlab配置的发信人  
  gitlab_rails['gitlab_email_from'] ="youremail@163.com"  
  user["git_user_email"] ="youremail@163.com"

注意：要使用163提供的SMTP和POP3服务，需要到自己邮箱里做设置，上面的smtp_password不是你的邮箱登录密码，而是你设置的那个授权码。

### 项目Path修改

将`/etc/gitlab/gitlab.rb`中的`external_url`通常会改成一个局域网IP，如下：
> external_url 'http://192.168.5.235'  

但是此时网页中项目的Path路径还没有被修改，此时还需要改动另一个地方，进行以下路径，
> cd /opt/gitlab/embedded/service/gitlab-rails/config  

修改`gitlab.yml`，也有可能没有该文件，只有`gitlab.yml.example`,复制`gitlab.yml.example`并命名为`gitlab.yml`即可, `cp gitlab.yml.example gitlab.yml`，做出如下修改
```
production: &base
  #
  # 1. GitLab app settings
  # ==========================

  ## GitLab settings
  gitlab:
    ## Web server settings (note: host is the FQDN, do not include http://)
    host: 10.108.5.235 // 改成你自己的IP即可
    port: 80
    https: false

```

然后重新启动或者启动Gitlab就可以。


## Gitlab常用命令

```
gitlab-ctl reconfigure  // 一般在修改配置文件后，要执行
gitlab-ctl status   // 查看gitlab的运行状况
gitlab-ctl start   // 启动gitlab
gitlab-ctl restart  // 重启Gitlab
```