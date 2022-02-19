# 安装hexo错误： #
----------
> > npm 错误！ 代码 EEXIST
> npm 错误！ 路径 C:\Users\Administrator\AppData\Roaming\npm\hexo
> npm 错误！ EEXIST：文件已经存在
> npm 错误！ 文件存在：C:\Users\Administrator\AppData\Roaming\npm\hexo
> npm 错误！ 删除现有文件并重试，或运行 npm
> npm 错误！ 使用 --force 可以鲁莽地覆盖文件。
>
> npm 错误！ 可以在以下位置找到此运行的完整日志：
> npm 错误！ C:\Users\Administrator\AppData\Local\npm-cache\_logs\2022-02-16T09_19_49_877Z-debug-0.log
> pm install hexo -g #安装Hexo
npm update hexo -g #升级
hexo init #初始化博客

## 命令简写 ##
pm install hexo -g #安装Hexo
npm update hexo -g #升级
hexo init #初始化博客

命令简写
hexo n "我的博客" == hexo new "我的博客" #新建文章
hexo g == hexo generate #生成
hexo s == hexo server #启动服务预览
hexo d == hexo deploy #部署

hexo server #Hexo会监视文件变动并自动更新，无须重启服务器
hexo server -s #静态模式
hexo server -p 5000 #更改端口
hexo server -i 192.168.1.1 #自定义 IP
hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令

刚刚的三个命令依次是新建一篇博客文章、生成网页、在本地预览的操作。

----------

# 把本地文件推到githup #
下一步将我们的Hexo与GitHub关联起来，打开站点的配置文件_config.yml，翻到最后修改为：

deploy:
type: git
repo: 这里填入你之前在GitHub上创建仓库的完整路径，记得加上 .git
branch: master参考如下：




保存站点配置文件。

其实就是给hexo d 这个命令做相应的配置，让hexo知道你要把blog部署在哪个位置，很显然，我们部署在我们GitHub的仓库里。最后安装Git部署插件，输入命令：

npm install hexo-deployer-git --save


这时，我们分别输入三条命令：



hexo clean 
hexo g 
hexo d
错误：
- 
- fatal: unable to access 'https://github.com/wsido/wsido.githup.io.git/': OpenSSL SSL_read: Connection was aborted, errno 10053
FATAL {
  err: Error: Spawn failed


- 原因

Git默认限制推送的大小，运行命令更改限制大小即可


- 解决方法

git config --global http.postBuffer 524288000
# *.githup.io个人网站无法访问 #








# hexo使用 #
hexo init 【名】
cd 博客
hexo g
hexo d
hexo server




# git使用 #

----------

1. git init :git对文件夹取得管理
1. git add -A
1. git commit -m""
1. git push ....
1. git 保存一个快照：commmit
1. cat xxx.xxx： 查看内容
1. git log/git log --pretty=oneline:最近的提交日志
1. git reset --hard commit_id
1. git reflog:记录每次命令
1. git reset -- HEAD^:回退到上一个版本
	HEAD表示单前版本
 git add git commit -m "xxx"暂存区。
git管理修改，而不是文件
git restore/checkout -- file :丢弃工作区更改.
git reset HEAD file :把暂存区修改撤销(unstage)
git rm xx.xx:删除文件
git commit -m "remove xx.xx"
git restore -- xx.xx：回退恢复
git diff 查看本地库与远程库不同
----------

# 远程仓库 #
创建SSH Key:

    $ ssh-keygen -t rsa -C "youremail@example.com"
一路回车，使用默认值即可
根据GitHub的提示，在本地的learngit仓库下运行命令
`$ git remote add origin git@github.com:michaelliao/learngit.git`
把本地库的所有内容推送到远程库上：

    $ git push -u origin master
错误：
`Everything up-to-date
branch 'master' set up to track 'origin/master'.
`
原因：
少了，提交前先从远程仓库主分支中拉取请求这步

1. 添加到本地仓库
1. `git add .`
1. 添加提交描述
1. `git  commit  -m "第一次提交"`
1. 提交前先从远程仓库主分支中拉取请求
1. `git pull origin master`
1. 把本地仓库代码提交
1. `git push -u origin master`

把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。
从现在起，只要本地作了提交，就可以通过命令：

    $ git push origin master

# Git 提示fatal: remote origin already exists #
1、先删除远程 Git 仓库

    $ git remote rm origin

2、再添加远程 Git 仓库

    $ git remote add origin git@github.com:FBing/java-code-generator

# SSH警告 #
当你第一次使用Git的clone或者push命令连接GitHub时，会得到一个警告：

    The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
    RSA key fingerprint is xx.xx.xx.xx.xx.
    Are you sure you want to continue connecting (yes/no)?
这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

    Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
这个警告只会出现一次，后面的操作就不会有任何警告了。
# 删除远程库 #
可以用`git remote rm <name>`命令。使用前，建议先用`git remote -v`查看远程库信息：

    $ git remote -v
    master  git@github.com:wsido/wsido.githup.io.git (fetch)
    master  git@github.com:wsido/wsido.githup.io.git (push)
    origin  git@github.com:wsido/learngit.git (fetch)
    origin  git@github.com:wsido/learngit.git (push)

然后，根据名字删除，比如删除`master`：

    $ git remote rm master

此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。  

# 从远程仓库克隆 #
  要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。

Git支持多种协议，包括https，但ssh协议速度最快。
 Greating a new branch is quick.

# 切换分支 #
Git鼓励大量使用分支：

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`或者`git switch <name>`

创建+切换分支：git checkout -b <name>或者git switch -c <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>

Greating a new branch is quick and simple.

#合并分支#
当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

用`git log --graph`命令可以看到分支合并图。

`git mv olefilename newfilename`:修改文件名。

#分支管理#
Git分支十分强大，在团队开发中应该充分应用。

合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并

Git is a free software.

#bug 分支#
修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。
`git branch -D <name>`:强行删除一个分支.
