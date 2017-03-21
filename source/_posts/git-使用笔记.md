---
title: git 使用笔记
date: 2017-03-13 14:38:56
tags:git
categories：笔记

---
##git常见命令
使用过的命令

- git clone git://github.com/schacon/grit.git <存放路径> 从服务器上将代码给拉下来
<存放路径>  

1.  "." 表示当前路径
2.  "/f/vue"表示f盘的vue文件夹
3.  "f/vue"表示当前路径下的f文件夹的vue文件夹



---
- git clone之后 有一个git文件夹 内部文件内容
[git文件夹内部文件用处](http://blog.sina.com.cn/s/blog_4d9c3fec0102w7g9.html)  
- [Git 常用命令大全](http://blog.csdn.net/dengsilinming/article/details/8000622)
 Git 是一个很强大的分布式版本控制系统。它不但适用于管理大型开源软件的源代码，管理私人的文档和源代码也有很多优势。

Git常用操作命令：

1) 远程仓库相关命令

检出仓库：$ git clone git://github.com/jquery/jquery.git

查看远程仓库：$ git remote -v

添加远程仓库：$ git remote add [name] [url]

删除远程仓库：$ git remote rm [name]

修改远程仓库：$ git remote set-url --push [name] [newUrl]

拉取远程仓库：$ git pull [remoteName] [localBranchName]

推送远程仓库：$ git push [remoteName] [localBranchName]

 

*如果想把本地的某个分支test提交到远程仓库，并作为远程仓库的master分支，或者作为另外一个名叫test的分支，如下：

$git push origin test:master         // 提交本地test分支作为远程的master分支

$git push origin test:test              // 提交本地test分支作为远程的test分支

 

2）分支(branch)操作相关命令

查看本地分支：$ git branch

查看远程分支：$ git branch -r

创建本地分支：$ git branch [name] ----注意新分支创建后不会自动切换为当前分支

切换分支：$ git checkout [name]

创建新分支并立即切换到新分支：$ git checkout -b [name]

删除分支：$ git branch -d [name] ---- -d选项只能删除已经参与了合并的分支，对于未有合并的分支是无法删除的。如果想强制删除一个分支，可以使用-D选项

合并分支：$ git merge [name] ----将名称为[name]的分支与当前分支合并

创建远程分支(本地分支push到远程)：$ git push origin [name]

删除远程分支：$ git push origin :heads/[name] 或 $ gitpush origin :[name] 

 

*创建空的分支：(执行命令之前记得先提交你当前分支的修改，否则会被强制删干净没得后悔)

$git symbolic-ref HEAD refs/heads/[name]

$rm .git/index

$git clean -fdx

 

3）版本(tag)操作相关命令

查看版本：$ git tag

创建版本：$ git tag [name]

删除版本：$ git tag -d [name]

查看远程版本：$ git tag -r

创建远程版本(本地版本push到远程)：$ git push origin [name]

删除远程版本：$ git push origin :refs/tags/[name]

合并远程仓库的tag到本地：$ git pull origin --tags

上传本地tag到远程仓库：$ git push origin --tags

创建带注释的tag：$ git tag -a [name] -m 'yourMessage'

 

4) 子模块(submodule)相关操作命令

添加子模块：$ git submodule add [url] [path]

   如：$git submodule add git://github.com/soberh/ui-libs.git src/main/webapp/ui-libs

初始化子模块：$ git submodule init  ----只在首次检出仓库时运行一次就行

更新子模块：$ git submodule update ----每次更新或切换分支后都需要运行一下

删除子模块：（分4步走哦）

 1) $ git rm --cached [path]

 2) 编辑“.gitmodules”文件，将子模块的相关配置节点删除掉

 3) 编辑“ .git/config”文件，将子模块的相关配置节点删除掉

 4) 手动删除子模块残留的目录

 

5）忽略一些文件、文件夹不提交

在仓库根目录下创建名称为“.gitignore”的文件，写入不需要的文件夹名或文件，每个元素占一行即可，如

target

bin

*.db

 

=====================
	
	Git 常用命令
	
	git branch 查看本地所有分支
	git status 查看当前状态 
	git commit 提交 
	git branch -a 查看所有的分支
	git branch -r 查看本地所有分支
	git commit -am "init" 提交并且加注释 
	git remote add origin git@192.168.1.119:ndshow
	git push origin master 将文件给推到服务器上 
	git remote show origin 显示远程库origin里的资源 
	git push origin master:develop
	git push origin master:hb-dev 将本地库与服务器上的库进行关联 
	git checkout --track origin/dev 切换到远程dev分支
	git branch -D master develop 删除本地库develop
	git checkout -b dev 建立一个新的本地分支dev
	git merge origin/dev 将分支dev与当前分支进行合并
	git checkout dev 切换到本地dev分支
	git remote show 查看远程库
	git add .
	git rm 文件名(包括路径) 从git中删除指定文件
	git clone git://github.com/schacon/grit.git 从服务器上将代码给拉下来
	git config --list 看所有用户
	git ls-files 看已经被提交的
	git rm [file name] 删除一个文件
	git commit -a 提交当前repos的所有的改变
	git add [file name] 添加一个文件到git index
	git commit -v 当你用－v参数的时候可以看commit的差异
	git commit -m "This is the message describing the commit" 添加commit信息
	git commit -a -a是代表add，把所有的change加到git index里然后再commit
	git commit -a -v 一般提交命令
	git log 看你commit的日志
	git diff 查看尚未暂存的更新
	git rm a.a 移除文件(从暂存区和工作区中删除)
	git rm --cached a.a 移除文件(只从暂存区中删除)
	git commit -m "remove" 移除文件(从Git中删除)
	git rm -f a.a 强行移除修改后文件(从暂存区和工作区中删除)
	git diff --cached 或 $ git diff --staged 查看尚未提交的更新
	git stash push 将文件给push到一个临时空间中
	git stash pop 将文件从临时空间pop下来
	---------------------------------------------------------
	git remote add origin git@github.com:username/Hello-World.git
	git push origin master 将本地项目给提交到服务器中
	-----------------------------------------------------------
	git pull 本地与服务器端同步
	-----------------------------------------------------------------
	git push (远程仓库名) (分支名) 将本地分支推送到服务器上去。
	git push origin serverfix:awesomebranch
	------------------------------------------------------------------
	git fetch 相当于是从远程获取最新版本到本地，不会自动merge
	git commit -a -m "log_message" (-a是提交所有改动，-m是加入log信息) 本地修改同步至服务器端 ：
	git branch branch_0.1 master 从主分支master创建branch_0.1分支
	git branch -m branch_0.1 branch_1.0 将branch_0.1重命名为branch_1.0
	git checkout branch_1.0/master 切换到branch_1.0/master分支
	du -hs
	
	-----------------------------------------------------------
	mkdir WebApp
	cd WebApp
	git init
	touch README
	git add README
	git commit -m 'first commit'
	git remote add origin git@github.com:daixu/WebApp.git
	git push -u origin master

##github使用
	作者：Fadeoc Khaos
	链接：https://www.zhihu.com/question/20070065/answer/30521531
	来源：知乎
	著作权归作者所有，转载请联系作者获得授权。
	
	Repository：你和我一起做“知乎首页”，“知乎首页”就是Repository，即项目或者”未来武器T2级425mm磁轨炮“之类，怎么叫随你，你只需知道Repository是个放项目的地方就行。有时候会出现Repositories，是多个Repository的意思。
	Fork：我们把制作“知乎首页“的工作分开，你负责美工，我负责前端开发，但我们还需要数据服务器高手。你找来了一位php大牛，这位大牛很快搞定了服务器端，闲来无事，就看了看我的前端代码，一看，“我靠，这怎么一点也不语义化呢？全是尼玛的清一色的<div>啊，将来做交互js还搞不搞dom了……”于是这大牛在Repository中找到了我写的“zhi.html”，Fork了一份，也就是授权拷贝。
	Branch：Fork之后，在大牛的Github上出现了一个同样叫做“知乎首页”的Repository，但是这个Repository是复制品，只归他，这就是他的Branch，也就是分支。
	Pull Request：大牛做完了一份全新的高端zhi.html，点了Pull Request，也就是推送请求。我接受了，看了一眼，顿时惊讶爆表，“中国足球——高，实在是高！”
	现在你懂了，Github的结构是Repository-Branch-(获取/推送)文件。你又发现Github可以比较两个文件的异同，新增的部分用绿色标记，删除的部分用红色标记。Pull Request还可以控制，甚至可以合并Branch，这就是团队合作利器啊，真乃高大上也，手痒了吧？心动了吧？


	注册Github并登录。
	下载客户端并登录，客户端负责你硬盘上的数据与Github服务器数据的交互，然后设置存储目录。为了表现你的才华，你决定将此目录命名为“诸神之爹”。
	既然有这么多的国外开源项目，我们国内哪有不自主的道理。必须要实践一下这个顶好赞的Fork功能。现在你来到了Fadeoc/frontend · GitHub，你看到了这是用户Fadeoc的一个叫做“frontend”的Repository，你笑了，这家伙学习前端知识不过十天，代码一片渣，竟然有的代码里只写了“土豆”和“二狗子”几个汉字。你点了一下右上角的Fork，然后clone in desktop，保存到“诸神之爹”，哇！文件已经在你电脑里了，完全免费耶！+10086！
	一个小时后，你对Fadeoc的渣代码颇有心得，决定帮他改良，不然他这项目就完了。你改好之后，Pull Request，这丫的竟然说你的代码太渣，不吸收。贱人！老子自己做，抢你市场份额！
	你点了右上角自己头像后面的+号，选择了第一个New repository，即新建repository，并且起了个名字，叫做“完爆Fadeoc”，然后点击绿色按钮set up in desktop，弹出保存框，选择“诸神之爹”。于是“诸神之爹”下出现了一个“完爆Fadeoc”的文件夹。
	你自己写了一份“神爹首页.html”，把它放在了“完爆Fadeoc”文件夹下。
	你打开了客户端，看到客户端界面中master Branch（主人分支，这名字太云端了）出现了一个Uncommitted changes，即未提交的变动，也就是你刚写的“神爹首页.html”。你点开show按钮，在summary（摘要）的部分添上“滚你丫的Fadeoc”，在Description（细节描述）的位置是没必要写的，但你还是决定添上“爆你菊花”四个大字。然后选择“Commit to 你的用户名”。
	为了把这个提交上传到Github上让贱人Fadeoc看到，你点击了客户端右上角的后面显示了一个“+1”的Sync，即同步，过了几秒，Sync前的两个曲线箭头停止了转动，同步成功了，“+1”消失，表示一个文件成功上传。
	你来到Github，刷新自己的个人页，“完爆Fadeoc”这个Repository出现在页面上，点开它，在里面你看到了”神爹首页.html”。
	为了让这个项目的初始目的更加浅显易懂，你决定添加一个Readme.txt，虽然从前下载的N多软件的文件夹里总是有一个Readme.txt，你一个都没打开过。但在圈里混，就得混的人模狗样的，于是你在“完爆Fadeoc”下新建了一个Readme.txt，里面写上，“Fadeoc，没错，说的就是你，看我口型，你个贱人！”
	同样使用客户端commit，然后sync，过了几秒，刷新github，你看到又多出了一个readme.txt。而且在下面又多出一个文字显示框，里面显示的就是readme.txt里面的内容“Fadeoc，没错，说的就是你，看我口型，你个贱人！”，避免了Fadeoc这个贱人不想打开readme.txt也就看不到你亲切问候的尴尬局面。Github真是贴心呐。
	你复制了这个Repository的地址，Email给了Fadeoc。
	Fadeoc不是那么容易被打败的，于是他Fork了你的Repository，修改了readme.txt，然后pull request，你看到fadeoc新生成的branch下的readme.txt被改成了“你才是贱人”。你拒绝了合并请求。
	Fadeoc再次pull request，readme.txt改成了“敢不做恶吗？”
	你有点烦了，这他妈的怎么才能不让他pull request，将来大项目N多陌生人菜鸟pull request烦不烦，就不能不开源，转私有吗？你终于找到了Github的升级服务，你笑了，将这个Repository从Public转成了Private。Fadeoc肯定会继续pull request，得不到你回应的他只会渐渐被复仇的怒火烧尽理智，可是，谁在乎呢？


##参考
[怎样使用 GitHub？-知乎](https://www.zhihu.com/question/20070065)


