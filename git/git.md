# git
## git官方文档
 >Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

>Git is easy to learn and has a tiny footprint with lightning fast performance. It outclasses SCM tools like Subversion, CVS, Perforce, and ClearCase with features like cheap local branching, convenient staging areas, and multiple workflows.

//git是一个开源的分布式版本控制系统，以快速高校的方式应对大大小小的项目<br/>
//git方便易学，有很小的足迹也能快速执行，和其他的SCM工具（Subversion,CVS,Perforce,ClearCase）具有方便的本地分支功能，方便的分段操作功能，可多人作业工作流

## 特性

Branching and Merging:分支和合并，在同一目录下就能切换分支方便合并<br/>
Small and Fast<br/>
Distributed：分布式管理，版本本地化，支持离线提交，相对独立吧不影响协同开发<br/>
Data Assurance：把内容按元数据方式存储，完整克隆版本库，所有信息都在.git目录中，它是处于你机器上的一个克隆版本库，它拥有中心版本库所有的东西，比如分支、标签、版本记录等<br/>
Staging Area：首先在本地上的版本控制是离线阶段，普要commit到staging（缓存区）管理好本地的.git后再push上去。<br/>
Free and Open Source<br/>

## 上传流程
获得repository===修改删查仓库里的文件===>添加状态到staging（缓存区中）====>更新缓存区的commit状态 =====>push到remote的服务器库中<br/>

//所有的思路分两个阶段的操作<br/>
//1.在本地的.git目录的操作，更新缓存，提交commit。<br/>
//2.和远程服务器的链接
##### tips：在代码本地和远程服务器连接的方式是以ssh的方式
```
//ssh的设置获取设置
1.配置用户信息
$ git config --global user.name "xuhaiyan"
$ git config --global user.email "haiyan.xu.vip@gmail.com"
//全局设置git的用户名和用户邮箱，这个会嵌入到你的每次提交中。
要是不想全局设置就不要用参数global，这个config文件在gitconfig文件夹中，
这两个是可以重设的
2.生成密钥
$ ssh-keygen -t rsa -C “haiyan.xu.vip@gmail.com”
查看ssh密钥：cd ~/.ssh
最后得到了两个文件：id_rsa和id_rsa.pub
添加密钥到ssh：ssh-add 文件名（私钥）
在github上添加ssh“id_rsa.pub”里面的公钥。

//ssh的运行机制不懂，但是，可以这么说，ssh密钥生成一个公钥一个私钥。
将公钥配置到远程服务器后，再上传的时候，git就会将私钥去配对远程服务器的公钥，配对成功后才可以上传

```

-----

```
//上传流程命令行
在你需要保存代码的空文件夹运行
git init            
git clone git@uri   //这样文件夹内就有了.git目录

git add <file> // 将工作文件修改提交到本地暂存区
git add . // 将所有修改过的工作文件提交暂存区

git commit -am “string” //对这个commit做一个说明，提交到了.git目录的元数据更新
//两个概念，一个是代码（文件）的改变，一个是描述这次改变的元数据是

git remote add origin git@uri  //添加远程库到git。origin只是一个描述git@uri的变量，可以取任何名字。
git push -u origin master // 客户端首次提交
```
----

#### 分支流程
在本地新建一个branch =====>远程分支新建 =====>提交分支代码<br/>
//这是在master的情况下建立的分支。


```
git branch new-branch //在当前分支上新建分支
git checkout new-branch //切换分支
git push -u origin new-branch //上传分支

```
----


#### 分支合并
1. 明白一个概念，分支合并只是把分支的代码合并到了master的代码中，branch还是在的，要是继续再向这个分支push代码。照样有自己的代码版本流。<br/>
2. 其次在合并代码的过程中，master和branch（pull最新版本代码）代码发生冲突的时候（把远程的master合并到本地的branch），在master merge branch的时候，冲突了，查到到报错的文件，文件会以```>>>>>HEAD=====<<<<<```的方式显示冲突的部分，删除不需要的代码，再次添加缓存，commit。
//目的是把branch的代码作为最新的master代码

```
git pull|fetch //（建议用后者，不自动合并代码）
git merge master //把主干的代码合并到本地，解决冲突后再把新的代码提交上去
```
----
#### 版本回溯
查看所在项目+版本流（master|branch）的commit状态的id =====>本地回到的版本====>1、强制提交到到remote库中(中间的所有commit都会消失)2.当作另外一次新的提交更新代码

```
git log -l 5 //查看最新的几次commit状态获取它的id

git reset HEAD
git reset --hard commit-id
一样要更新.git的状态
git push -f origin new-branch //强制上传,中间会断了几个commit
git revert commit-id//回到该id后就行再常规上传了
```
----
