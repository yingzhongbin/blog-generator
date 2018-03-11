---
title: 如何部署hexo博客
date: 2018-03-11 18:59:51
tags:
---

Hexo 博客搭建经历了一个不算平顺的过程。在这个过程中，需要学习命令行，github，Hexo和md编辑。

## 命令行学习过程

#### 命令行基本符号意义
符号 | 意义
-|-
~  | 用户目录
/  |  整个硬盘
.   | 当前目录
..  | 父目录
$  | 可以输入命令了

#### 命令行英语必备单词
英文 | 翻译   
-|-   
directory | 目录、文件夹   
file | 文件   
make | 新建   
remove | 删除   
move | 移动   
copy | 复制
list | 罗列
link | 链接
find | 查找
echo | 发出回音、重复
touch | 触摸
change | 改变

#### 命令行单词缩写

命令 | 全写 | 缩写
-|-|-
创建目录 | make directory | mkdir
删除 | remove | rm
移动 / 重命名 | move | mv
复制 | copy | cp
罗列 | list | ls
改变目录 | change directory | cd

#### 基本命令行及意义
命令行 | 意义
-|-
cd ~  | 进入用户目录  
pwd   | 显示当前目录  
mkdir demo-1   | 建立文件夹  
mkdir -p “demo1/demo2/demo3”  | 建立嵌套文件夹 可以不加引号  
mkdir demo 2  | 创建demo 2 两个文件夹  
mkdir “demo 2”  | 创建demo 2 这个文件夹  
whoami   |  显示用户名  
ls   | 显示当前目录  
ls  demo-2  |  显示demo-2目录  
ls  -a   |  显示当前目录  并显示隐藏文件   .文件   
touch  .frank  |  创建隐藏文件.frank   
touch frank  |   创建文件frank   
ls -l   |  显示当前目录文件的详细信息   
ls -al  |  是 ls - a 和  ls -l 的合并版   
echo “hello”>1.txt  |   将hello写入1.txt中   
echo “ring”>>1.txt  |   将ring追加到1.txt中   
touch 1.txt   |   创建文件1.txt   会改变更新时间  
 cp 1.txt 99.txt   |   将1.txt 复制到99.txt   
cp -r demo-1 demo-9  |   递归地将demo-1复制到demo-9   
mv 99.txt 44.txt  |   将99.txt重命名为44.txt  
rm 1.txt   |   删除文件  
rm -r demo-9  |  递归删除文件夹     
ln -s 444.txt 444-copy.txt  |  建立软链接  替身  
curl -L https://www.baidu.com>baidu.html  |  下载文件保存到baidu.html  

## github学习

### github命令行学习
#### 使用 git 有三种方式
 1.	只在本地使用    
 2.	将本地仓库上传到 GitHub    
 3.	下载 GitHub 上的仓库   
### 1.只在本地使用    
##### 1.1 初始化
 1.	创建目录作为项目目录：mkdir git-demo-1
 2.	进入目录 cd git-demo-1
 3.	git init，这句命令会在 git-demo-1 里创建一个 .git 目录
 4.	ls -la 就会看到 .git 目录，它就是一个「仓库」
 5.	在 git-demo-1 目录里面添加任意文件，假设添加了两个文件，分别是 index.html 和 css/style.css
	 i.	touch index.html
	 ii.	mkdir css
	 iii.	touch css/style.css
 6.	运行 git status -sb 可以看到文件前面有 ?? 号 ## Initial commit on master
 7.	 ?? css/
 8.	 ?? index.html
 9.	
这个 ?? 表示 git 一脸懵逼，不知道要怎么对待这些变动。
 10.	使用 git add 将文件添加到「暂存区」
	 i.	你可以一个一个地 add
		 a.	git add index.html
		 b.	git add css/style.css
	 ii.	你也可以一次性 add .     
		 a.	git add . 意思是把当前目录（.表示当前目录）里面的变动都加到「暂存区」
 11.	再次运行 git status -sb，可以看到 ?? 变成了 A ## Initial commit on master
 12.	 A  css/style.css
 13.	 A  index.html
 14.	
A 的意思就是添加，也就是说告诉 git，这些文件我要加到仓库里
 15.	使用 git commit -m "信息" 将你 add 过的内容「正式提交」到本地仓库（.git就是本地仓库），并添加一些注释信息，方便日后查阅
	 i.	你可以一个一个地 commit
		 a.	git commit index.html -m '添加index.html'
		 b.	git commit css/style.css -m "添加 css/style.css"
	 ii.	你也可以一次性 commit
		 a.	git commit . -m "添加了几个文件"
 16.	再再次运行 git status -sb，发现没有文件变动了，这是因为文件的变动已经记录在仓库里了。
 17.	这时你使用 git log 就可以看到历史上的变动：
以上就是 git add / git commit 的一次完整过程。

##### 1.2 文件变动
如果想继续改文件，应该怎么做呢？     
 1.	start css/style.css 会使用默认的编辑器打开 css/style.css（macOS 上对应的命令是 open css/style.css）   
 2.	然后在 css/style.css 里写入 body {background: red}，保存退出   
 3.	运行 git status -sb 发现提示中有一个 M ## master   
 4.	 M css/style.css  
 5.	 这个 M 的意思就是 Modified，表示这个文件被修改了   
 6.	此时如果想让改动保存到仓库里，需要先 git add css/style.css 或者也可以 git add 。 
注意，由于这个 css/style.css 以前被 add 过，往文章上面看，是 add 过 css/style.css 的，所以此处的 git add 操作可以省略。  
换句话说，每一次改动，都要经过 git add 和 git commit 两个命令，才能被添加到 .git 本地仓库里。    
 7.	再次运行 git status -sb 发现 M 有红色变成了绿色。  
 8.	运行 git commit -m "更新 css/style.css"，这个改动就被提交到 .git 本地仓库了。   
 9.	再再次运行 git status -sb，会发现没有变更了，这说明所有变动都被本地仓库记录在案了。   
git status 是用来显示当前的文件状态的，哪个文件变动了，方便进行 git add 操作。-sb 选项的意思：-s 的意思是显示总结（summary），-b 的意思是显示分支（branch），所以 -sb 的意思是显示总结和分支。 
  
### 1.3总结
至此，来总结一下用到的命令    
 1.	git init，初始化本地仓库 .git   
 2.	git status -sb，显示当前所有文件的状态   
 3.	git add 文件路径，用来将变动加到暂存区   
 4.	git commit -m "信息"，用来正式提交变动，提交至 .git 仓库    
 5.	如果有新的变动，我们只需要依次执行 git add xxx 和 git commit -m 'xxx' 两个命令即可。先 add 再 commit。     
 6.	git log 查看变更历史  
    
### 2将本地仓库上传到 GitHub
如何将这个 git-demo-1 上传到 GitHub 呢？    
 1.在 GitHub 上新建一个空仓库，名称随意，一般可以跟本地目录名一致，也叫做 git-demo-1     
 ![我是图片](如何部署hexo博客/cre-repo.png)     
按照截图所示，除了仓库名，其他的什么都别改，这样你才能创建一个空仓库     
 2.点击创建按钮之后，GitHub 就会把后续的操作全告诉你     
![我是图片](如何部署hexo博客/ssh.png)     
 1.点击 SSH 按钮。千万不要使用 HTTPS 地址，因为 HTTPS 地址使用起来特别麻烦，每次都要输入密码，而 SSH 不用输入用户名密码。
为什么 SSH 不用密码呢，因为已经上传了 SSH public key。     
 2.由于已经有本地仓库了，所以看图，图中下面半部分就是需要的命令，一行一行拷贝过来执行     
i.	找到图中的「…or push an existing repository from the command line」这一行，你会看到 git remote add origin https://github.com/xxxxxxxxxx/git-demo-1.git， 要使用 SSH 地址，GitHub 的 SSH 地址是以 git@github.com 开头的。     
ii.	再次点击 SSH 按钮，整个世界就会变得美好起来。     
iii.	得到新的命令 git remote add origin git@github.com:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/git-demo.git，复制并运行它     
	 iv.	复制第二行 git push -u origin master，运行它     
	 v.	刷新当前页面，仓库就上传到 GitHub 了！      
	 
### 3 直接在 GitHub 创建一个仓库，然后下载到本地     
上面两步讲了     
 1.	在本地创建仓库
 2.	将本地仓库上传到 GitHub     
这里讲第三种用法，那就是直接在 GitHub 创建一个仓库，然后下载到本地。     
 1.	在GitHub 上新建一个仓库 git-demo-3，这次就不创建空仓库了，而是自带 README 和 Lisence 的仓库，创建截图如下：     
 ![我是图片](如何部署hexo博客/gt3.png)     
  请按图中所示，填写一模一样的内容，然后点击创建按钮。     
 2.	这样一来，这个仓库就会自动拥有三个文件：     
  ![我是图片](如何部署hexo博客/3files.png)     
 3.	这三个文件的作用请自行了解：.gitignore 的作用、README.md 的作用 以及 LISENCE 的作用     
 4.	好了，现在远程仓库已经创建好了，怎么下载到本地（也就是我们的电脑上）呢？答案是使用 git clone 命令     
 5.	点击页面中唯一的绿色按钮「clone or download」，会看到一个弹出层     
  ![我是图片](如何部署hexo博客/clone.png)     
 6.	请确保弹出层里的地址是 SSH 地址，也就是 git@github.com 开头的地址，如果不是，就点击 Use SSH 按钮。然后复制这个地址。     
 7.	打开 Git Bash，找一个安全的目录，比如 ~/Desktop 桌面目录就很安全：cd ~/Desktop。运行。     
 8.	运行 git clone 你刚才得到的以git@github.com开头的地址，运行完就会发现，桌面上多出一个 git-demo-3目录。       
 9.	进入这个多出来的目录，对的，你肯定会忽略这一步。    
 10.	运行 ls -la 会看到，远程目录的所有文件都在这里出现了，另外还看到了 .git 本地仓库。就可以添加文件，git add，然后 git commit 了。     
 
 
三种方式都说完了，它们分别是：     
 1.	在本地创建仓库     
 2.	将本地仓库上传到 GitHub     
 3.	下载 GitHub 上的仓库到本地          
再回顾一遍已经学到的命令：（这次只多了一个 git clone 命令）     
 1.	git clone git@github.com:xxxx，下载仓库     
 2.	git init，初始化本地仓库 .git     
 3.	git status -sb，显示当前所有文件的状态     
 4.	git add 文件路径，用来将变动加到暂存区     
 5.	git commit -m "信息"，用来正式提交变动，提交至 .git 仓库     
 6.	如果有新的变动，只需要依次执行 git add xxx 和 git commit -m 'xxx' 两个命令即可。先 add 再 commit，行了，学会 git 了。     
 7.	git log 查看变更历史     

### 如何上传更新
在本地目录有任何变动，只需按照以下顺序就能上传：     
 1.	git add 文件路径     
 2.	git commit -m "信息"     
 3.	git pull （相信我，你一定会忘记这一个命令）     
 4.	git push     
 5.	
#### 下面是例子
 1.	cd git-demo-1     
 2.	touch index2.html     
 3.	git add index2.html     
 4.	git commit -m "新建 index2.html"     
 5.	git pull     
 6.	git push     
然后去 git-demo-1 的 GitHub 页面，就能看到 index2.html 出现在里面了。

### 其他     
#### 还有一些有用的命令     
 •	git remote add origin git@github.com:xxxxxxx.git 将本地仓库与远程仓库关联     
 •	git remote set-url origin git@github.com:xxxxx.git 上一步手抖了，可以用这个命令来挽回     
 •	git branch 新建分支     
 •	git merge 合并分支     
 •	git stash 通灵术     
 •	git stash pop 反转通灵术     
 •	git revert 后悔了     
 •	git reset 另一种后悔了     
 •	git diff 查看详细变化     
 
 
## 学习Hexo

### 步骤
 1.	进入一个安全的目录，比如 cd ~/Desktop 或者 cd ~/Documents。   
 2.	在 GitHub 上新建一个空 repo，repo 名称是「你的用户名.github.io」（请将你的用户名替换成真正的用户名）     
 3.	npm install -g hexo-cli，安装 Hexo     
 4.	hexo init myBlog     
 5.	cd myBlog     
 6.	npm i     
 7.	hexo new 开博大吉，会看到一个 md 文件的路径     
 8.	open xxxxxxxxxxxxxxxxxxx.md，编辑这个 md 文件（Ubuntu 系统用 xdg-open xxxxxxxxxxxxxxxxxxx.md 命令）     
 9.	open _config.yml，编辑网站配置     
	 i.	把第 6 行的 title 改成想要的名字     
	 ii.	把第 9 行的 author 改成大名     
	 iii.	把最后一行的 type 改成 type: git     
	 iv.	在最后一行后面新增一行，左边与 type 平齐，加上一行 repo: 仓库地址 （将仓库地址改为「用户名.github.io」对应的仓库地址，仓库地址以 git@github.com: 开头）     
	 v.	第 4 步的 repo: 后面有个空格，不要眼瞎。     
 10.	npm install hexo-deployer-git --save，安装 git 部署插件     
 11.	hexo deploy     
 12.	进入「用户名.github.io」对应的 repo，打开 GitHub Pages 功能，如果已经打开了，就直接点击预览链接     
 13.	看到博客！     

#### 第二篇博客
 1.	hexo new 第二篇博客     
 2.	复制显示的路径，使用 start 路径 来编辑它     
 3.	hexo generate     
 4.	hexo deploy     
 5.	去看你的博客，应该能看到第二篇博客了     
 
 
#### 上传源代码
注意「你的用户名.github.io」上保存的只是博客，并没有保存「生成博客的程序代码」，需要再创建一个名为 blog-generator 的空仓库，用来保存 myBlog 里面的「生成博客的程序代码」。     
 1.	在 GitHub 创建 blog-generator 空仓库     
 2.	按照截图中的命令执行即可，记住，别 用 HTTPS 地址。     
这样一来，博客就发布在「用户名.github.io」，而「生成博客的程序代码」发布在了 blog-generator。所有数据万无一失，就不会因为误删 myBlog 目录而痛哭了。     
以后每次 hexo deploy 完之后，博客就会更新；然后还要 add / commit /push 一下「生成博客的程序代码」，以防万一。     
这个 blog-generator 就是用来生成博客的程序，而「用户名.github.io」仓库就是博客页面。     

## md编辑学习

md编辑学习找到一篇比较好的他人[博客](https://www.cnblogs.com/liugang-vip/p/6337580.html) 。以此学习编辑md文件。

## 提交文件后发现图片显示不出来了！这就很难受了，于是又找到一个[方法](http://blog.csdn.net/sugar_rainbow/article/details/57415705)!

## 至此，搭建好hexo博客！
