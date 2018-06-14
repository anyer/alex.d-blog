---
title: 多个git托管平台同时使用时SSH Key的生成及添加
categories:
  - 问题处理
tags:
  - Github
  - 码云
  - SSH Key
  - Git
copyright: true
description: 本文记录一台电脑上同时使用多个git托管账号时的处理方法。
abbrlink: 8b4e7cd5
date: 2018-06-13 16:07:22
updated: 2018-06-13 16:07:22
---

使用一个邮箱注册多个git代码托管平台，如：GitHub、Gitlab、码云等。在用户端，生成对应平台的的 `SSH Key` 时，会生成对应的 `id_rsa` 及 `id_rsa.pub` 公钥文件（默认的密钥文件名取决于算法，此处默认使用RSA算法加密），然后在对应的平台上添加用户生成的 `SSH Key` 即可，下文将在此基础延伸多个git托管平台使用时，对应的多个秘钥生成及添加。

### **单个平台SSH key生成及添加**
Windows下需要在 `git bash` 命令行窗口（也可使用 `cmder` )，按照下面命令，来生成对应托管平台的  `SSH Key` 。

``` bash

ssh-keygen -t rsa -C "对应平台注册的邮箱地址" 

```
命令行输出类似如下消息

``` bash
$ ssh-keygen -t rsa -C "maple_6392@163.com"
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in gitee_id_rsa.
Your public key has been saved in gitee_id_rsa.pub.
The key fingerprint is:
SHA256:t86b0RbwMYAVdqGwUQXkuS3ZnL1u4UJBgfjrK7TJkKY maple_6392@163.com
The key's randomart image is:
+---[RSA 2048]----+
|        o*O==o   |
|        o*.=.    |
|        ..=.o    |
|          .O.=   |
|       .S =.B..  |
|      + ...+.... |
|     o + +o.o... |
|    E   =o.+..o  |
|         .*o o.  |
+----[SHA256]-----+

```
此时在 `~/.ssh` 目录下会生成 `id_rsa` 及 `id_rsa.pub` 文件

> .ssh 目录在对应用户的根目录下，即 ： `C:\Users\当前用户名\.ssh`

<span id="add_key"></span>

然后将 `id_rsa.pub` 文件的内的  `SSH Key`  添加到对应的平台（此处以GitHub为例)

![github_setting][1]

![github_ssh_keys][2]

![github_ssh_key_add][3]


设置内后，通过命令进行验证

``` bash

ssh -T git@github.com

```

> **注意**， 此处git@后添加对应平台的主域名，如Github的github.com，码云的gitee.com。

如果上面命令添加执行后，命令行输出类似内容

``` bash

Hi yourname（此处为对应git平台的用户名）! You've successfully authenticated... 

```

或

``` bash

Welcome to xxx.com, yourname（此处为对应git平台的用户名）!...

```

则表示对应平台的SSH key生成及部署成功。

否则，
 - 检查对应的key是否粘贴正确
 - 检查操作步骤是否正确
 - Try again ~~~

> 如出现添加了公钥后仍然无法推送代码，则可以参看[此处][4]
> **注意：** 要使用SSH链接操作远程仓库，Git的Remote要使用SSH地址，关于Remote使用见[这里][5]

---

### **多平台SSH key生成部署**

此处以 [Github][6] 及 [码云][7] 为例，做演示说明。

类似单平台SSH Key的创建，多个平台生成命令做如下调整：

``` bash

ssh-keygen -t rsa -C "平台注册的邮箱地址" -f "生成的rsa文件名"

```

> **注意：** `-f` 后面带的文件名称，不含路径，则生成在当前命令行路径内所在的目录下。更多工具 `ssh-keygen` 的命令说明及使用见[此处][8]

通过此命令，依次生成两个平台的key

``` bash

$ ssh-keygen -t rsa -C "maple_6392@163.com" -f "github_id_rsa"
$ ssh-keygen -t rsa -C "maple_6392@163.com" -f "gitee_id_rsa"

# Generating public/private rsa key pair...
# 三次回车即可生成 ssh key

```

![gitee_ssh_key][9]

此时 `~/.ssh` 目录下，生成的文件如下

![ssh_dir][10]

此时对应的SSH Key生成成功，具体添加平台的步骤参看[上文][11]，添加完成进行验证时，出现如下提示：

``` bash

$ ssh -T git@gitee.com
The authenticity of host 'gitee.com (218.11.0.86)' can't be established.
ECDSA key fingerprint is SHA256:FQGC9Kn/eye1W8icdBgrQp+KkGYoFgbVr17bmjey0Wc.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'gitee.com,218.11.0.86' (ECDSA) to the list of known hosts.
Permission denied (publickey).


```

此时可以参看 [Windows下由于SSH配置文件的不匹配，导致的Permission denied (publickey)及其解决方法][12]

文章内说创建config文件，结合参考文章 [【工具安装和配置】 GIT同时连接gitlab和github**strong text**][13] 尝试后，未解决问题。

此处解决，使用 `ssh-agent` 工具，更多关于此工具的说明见[此处][14]。

--- 

### **ssh-agent解决Permission denied (publickey)问题**

 - 首先确定工具是否可以使用

``` bash

$ eval `ssh-agent`

## 控制台输出类似下面内容，表示该工具可以使用（结果输出为工具的进程PID）
#  Agent pid 7488

```
> **注意：** Windows系统下需在 `git bash` 或 `cmder` 命令行界面下操作

 - 使用 `ssh-add` 工具将 `SSH Key` 添加到 `ssh-agent` 

``` bash

# 添加GitHub的SSH Key
$ ssh-add C:/Users/xxx/.ssh/github_id_rsa
# 添加码云的SSH Key
$ ssh-add C:/Users/xxx/.ssh/gitee_id_rsa

## 此时可能需要输入生成SSH Key时配置的密码（如果有设置的话），成功后输出类似以下内容
# Identity added: C:/Users/xxx/.ssh/github_id_rsa (C:/Users/xxx/.ssh/github_id_rsa)
# Identity added: C:/Users/xxx/.ssh/gitee_id_rsa (C:/Users/xxx/.ssh/gitee_id_rsa)

```

如出现类似下面提示：

``` bash

$ ssh-add C:\Users\xxx\.ssh\gitee_id_rsa
Could not open a connection to your authentication agent.

```

可以使用 `ssh-agent bash --login -i` 命令来启动 `ssh-agent`


- 最后使用 `ssh -T git@xxx.com` 命令验证Key是否添加成功

> 关于SSH的更多命令可以查看[此处][15]

虽然通过上面操作可以使用ssh连接多个git平台，但使用git工具 `TortoiseGit` 进行提交时，依旧会出现 `Please make sure you have the correct access rights
and the repository exists.` 的提示，此时在bash控制台通过 `git push` 命令则正常提交。。。  此问题待解决，有知道怎么处理的朋友，希望可以告知。


  [1]: http://p9uy5dyvc.bkt.clouddn.com/github_setting.png "github_setting.png"
  [2]: http://p9uy5dyvc.bkt.clouddn.com/github_ssh_keys.png "github_ssh_keys.png"
  [3]: http://p9uy5dyvc.bkt.clouddn.com/github_ssh_key_add.png "github_ssh_key_add.png"
  [4]: http://git.mydoc.io/?t=153708
  [5]: https://git-scm.com/book/zh/v1/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8
  [6]: https://github.com
  [7]: https://gitee.com
  [8]: https://www.ssh.com/ssh/keygen/
  [9]: http://p9uy5dyvc.bkt.clouddn.com/gitee_ssh_key.png "gitee_ssh_key.png"
  [10]: http://p9uy5dyvc.bkt.clouddn.com/ssh_dir.png "ssh_dir.png"
  [11]: #add_key
  [12]: http://git.mydoc.io/?t=153707
  [13]: https://www.jianshu.com/p/88005b56fb4d
  [14]: https://www.ssh.com/ssh/agent
  [15]: https://www.ssh.com/ssh/command/