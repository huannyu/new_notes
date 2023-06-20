# 搭建用git, github管理markdown文档环境



## 软件准备

> 下载typora，git，注册github账号并创建一个repository



> - Git Bash：Unix与Linux风格的命令行，使用最多，推荐最多
> - Git CMD：Windows风格的命令行
> - Git GUI：图形界面的Git，不建议初学者使用，尽量先熟悉常用命令



## 配置公钥

> git使用https协议，每次pull, push都要输入密码，相当的烦。
>
> 使用git协议，然后使用ssh密钥，这样就可以省去每次都输密码。

- 用 ssh-keygen命令生成公钥
- 将公钥复制到github设置里
- 用git clone把github里自己的repository地址克隆到本地，就可以通过本地git bash操作repository文件了。



```
ssh-kengen -t rsa
# -t指定生成密钥的类型（rsa\dsa\ecdsa等）
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/huy/.ssh/id_rsa): /c/Users/huy/.ssh_test/id_rsa
# 这里我指定了一个目录，也可以按回车选择默认目录
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
# 密码可填可不填
Your identification has been saved in /c/Users/huy/.ssh_test/id_rsa
Your public key has been saved in /c/Users/huy/.ssh_test/id_rsa.pub
The key fingerprint is:
SHA256:HtIe7Npqyyw7FrPO9DzHN8qx0uam0wmn3+Xvf4Mgou4 huy@CNL21018
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|                 |
|                 |
|       o         |
|      . S        |
|    o .*.+ .     |
|    .+.B*.. o .  |
|   o=**+O+oo . ..|
|   o*EX&Bo...oo.+|
+----[SHA256]-----+

# 提取ssh
huy@CNL21018 MINGW64 ~
$ cat /c/Users/huy/.ssh_test/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDm5EipVhteS91s9Xr60C0Y1VQ0w8cQpp7eP5qS6OwAc2/UFg+KNBgs2tCj1YepRiI0JsjQdLsBXJp3NbAqmJQpdmzU8CwOwtzQl8dZOQZ0QKdnMcEIWtGewJxKdR4lG/1svXIv5iZANXvx4mYge+UjZSyg2lQikr0OjsNK/ynbUaTefzM5VQaqf+6ark3NYGdpysvxdPYeEwyOyNbSjzOptG5H4DkN9HX41JmMbQWKHOowMhLlpKepc9GqNyNon6jw6oACyg6s3yLpiNXzXQCVqwyxl/R26DPaeX5LvgO6NNvVfVbPo7iDkXR65pfF+oBkhGD4zZD2cktf8SSS9zM9aIp2/z8hCF9NTSfVgGK55WebI0h9clZdhGN1aEbpIzWWKPUtO0cvtxaEM6ksHI2KrF2fgWEdJRm7RT7b9zHfQBJdoitNzvQw99nLB/SzPXjd63MMhuSh++yVQaxTSYjMg8UWe0/Tl0o75kCh3d3RhP8faK4QB1U631SauY300es= huy@CNL21018
# 第29行就是完整的一串ssh公钥，复制，粘贴到github的设置里，同时你的注册邮箱也会收到一封ssh公钥添加成功
```



## 创建本地镜像仓库

> github上创建好的仓库会有一个地址，将这个地址用git clone到本地，就可以实现在本地编辑文档，再通过git命令将所有的更改上传至github的repository。

```
# 查看当前工作目录
huy@CNL21018 MINGW64 ~
$ pwd
/c/Users/huy

huy@CNL21018 MINGW64 ~
# 把github里建好的repository克隆到本地当前的工作目录/c/Users/huy下面
$ git clone git@github.com:huannyu/new_notes.git
Cloning into 'new_notes'...
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
warning: You appear to have cloned an empty repository.
```



## 创建文件，上传文件

> 找到正确的目录，开始创建文件，编辑文件，再将更新push到repository的main branch里



**创建文件**

```
# cd表示切换当前目录到new_notes
huy@CNL21018 MINGW64 ~
$ cd new_notes

# 查看当前git状态
huy@CNL21018 MINGW64 ~/new_notes (main)
$ git status
On branch main
# 这个main branch是github默认的一个branch

No commits yet

nothing to commit (create/copy files and use "git add" to track)

# 在new_notes文件夹下面添加一个reading文件夹
huy@CNL21018 MINGW64 ~/new_notes (main)
$ mkdir reading

# 在new_notes文件夹下面添加一个computer文件夹
huy@CNL21018 MINGW64 ~/new_notes (main)
$ mkdir computer

# 切换目录到reading文件夹
huy@CNL21018 MINGW64 ~/new_notes (main)
$ cd reading

# 创建文件file.md
huy@CNL21018 MINGW64 ~/new_notes/reading (main)
$ touch file.md

# 列出当前工作文件夹reading目录下的所有文件
huy@CNL21018 MINGW64 ~/new_notes/reading (main)
$ ls
file.md
```



**上传文件**

```
# 将当前目录下所有文件添加到暂存区
githuy@CNL21018 MINGW64 ~/new_notes/reading (main)
$ git add .

# 将暂存区的文件添加到本地git repo
huy@CNL21018 MINGW64 ~/new_notes/reading (main)
$ git commit -m "updated the file"
[main (root-commit) d56a412] updated the file
 Committer: Huan Yu <huan.yu@sigmatechnology.com>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 6 insertions(+)
 create mode 100644 reading/file.md

# 将本地repo的文件推送到远端repo
huy@CNL21018 MINGW64 ~/new_notes/reading (main)
$ git push
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (4/4), 294 bytes | 294.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:huannyu/new_notes.git
 * [new branch]      main -> main
```



**编辑文件**

```
vim file01.txt
# 进入编辑模式
# 编辑完之后 按esc键后，输入:wq然后回车，退出vim模式

# 复制粘贴快捷键 ctrl+fn+f10insert
```



## 分支管理

> 在开发中，一般有如下分支使用原则与流程：
>
> - master （生产） 分支：线上分支，主分支，中小规模项目作为线上运行的应用对应的分支；
>
> - develop（开发）分支：是从master创建的分支，一般作为开发部门的主要开发分支，如果没有其他并行开发不同期上线要求，都可以在此版本进行开发，阶段开发完成后，需要是合并到master分支，准备上线



**创建分支，在分支内创建新文件**

```
# 新建branch dev01
huy@CNL21018 MINGW64 ~/new_notes (main)
$ git branch dev01

# 新建branch dev02
huy@CNL21018 MINGW64 ~/new_notes (main)
$ git branch dev02

huy@CNL21018 MINGW64 ~/new_notes (main)
$ git branch
  dev01
  dev02
* main

# 切换当前branch至dev01
huy@CNL21018 MINGW64 ~/new_notes (main)
$ git checkout dev01
Switched to branch 'dev01'

# 把本地dev01 push到远端库里，因为远端没创建，所以要--set-upstream origin dev01；如果远端有，直接git push就可以
huy@CNL21018 MINGW64 ~/new_notes (dev01)
$ git push --set-upstream origin dev01
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'dev01' on GitHub by visiting:
remote:      https://github.com/huannyu/new_notes/pull/new/dev01
remote:
To github.com:huannyu/new_notes.git
 * [new branch]      dev01 -> dev01
branch 'dev01' set up to track 'origin/dev01'.

# 在本地dev01里创建新文件file_dev_01
huy@CNL21018 MINGW64 ~/new_notes (dev01)
$ touch file_dev_01.md

# 用git add . git commit git push上传到远端repo
huy@CNL21018 MINGW64 ~/new_notes (dev01)
$ git add .

huy@CNL21018 MINGW64 ~/new_notes (dev01)
$ git commit -m "add file_dev_01"
[dev01 38df5e1] add file_dev_01
 Committer: Huan Yu <huan.yu@sigmatechnology.com>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 7 insertions(+)
 create mode 100644 file_dev_01.md

huy@CNL21018 MINGW64 ~/new_notes (dev01)
$ git push
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 565 bytes | 565.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:huannyu/new_notes.git
   2f7cd29..38df5e1  dev01 -> dev01
```

> 到这里会发现，github的repo里除了main branch，出现了dev01 branch，而新建的file_dev_01这个文件目前只存在在dev01 branch里，不存在在main branch里。

![image-20230606164649680](../../AppData/Roaming/Typora/typora-user-images/image-20230606164649680.png)



**合并分支**

> 合并分支要先回到需合并到的分支，合并之后，各分支都还在，但是分支内的内容合并到了一起



```
# 回到需合并到的分支main branch
huy@CNL21018 MINGW64 ~/new_notes (dev01)
$ git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

# 将dev01 branch合并到main branch
huy@CNL21018 MINGW64 ~/new_notes (main)
$ git merge dev01
Updating 2f7cd29..38df5e1
Fast-forward
 file_dev_01.md | 7 +++++++
 1 file changed, 7 insertions(+)
 create mode 100644 file_dev_01.md

# 将合并内容后的main branch更新到远端repo
huy@CNL21018 MINGW64 ~/new_notes (main)
$ git push
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:huannyu/new_notes.git
   2f7cd29..38df5e1  main -> main
```

> 到这里会发现，github里我的repository里面的main branch里面就也有file_dev_01这个文件了。

![image-20230606165211741](../../AppData/Roaming/Typora/typora-user-images/image-20230606165211741.png)



