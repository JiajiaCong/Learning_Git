Git
===
学习的环境是在电脑的E盘下，有一个Github的文件夹，文件夹下面有一个叫做test的文件夹。文件夹里有两个文档，一个是hi.txt，一个是hi2.txt.

更为详细的Git的基本命令，请见这个网址\(https://github.com/progit/progit/blob/master/zh/02-git-basics/01-chapter2.markdown)

# 配置一个新的电脑连接到我的Github账户

首先改变电脑的两个设定。control panel-appearance and personalization-folder options-view 中，设定为show hidden files, folders, and drivers; 将hider extensions for known file types前面的勾去掉。

假如这个电脑以前从来没有连接过github，或者已经连接过github，你现在想设定一下或者重新设定一下，让这个电脑能够连接到你的github账户。那么你必须需要一个ssh key, 这个ssh key必须同时在你的电脑里，这个key也需要在你github账户ssh key中。

首先打开C:\Users\用户名 这个文件夹，查看这个文件夹下是否有一个.ssh的文件。如果已经有了，说明这个电脑曾经能够连接到自己的github账户，删除这个.ssh 文件夹。下面我们要生成一个新的.ssh文件。

在bash中输入生成ssh key的命令     
ssh-keygen -t rsa -C "jiajiacong@gmail.com"     
press enter 并且输入一个密码之后，在C:\Users\用户名下面就会生成一个.ssh的文件夹。打开其中的id_rsa.pub，复制全部内容。浏览器打开自己的github账户，在setting中找到SSH Keys这个选项，然后Add SSH Key，这样你的电脑就受到github的认可了。

在bash中输入    
ssh -T git@github.com    
来查看电脑是否已经能够连接到github账户了


# 基本的Git命令

- ls
- pwd
- mkdir filename 创建新的文件夹
- cd \<project file\>
- cd .. 回到上一级的目录
- git init \<project file>  将某个project file变为repository
- git status 

  git status will tell you:
  - what branch you are on
  - what files have changed
  - what files are not tracked (其中红色字体显示的file就是没有被tracked的file)
  - hints on want to do next
- git status -s 这个相当是获得一个short的git status，就是一些不太有用的信息不在git status中显示了

- git add . (add和.之间要有一个空格！)  add all files to staging. 是一次将所有未被tracked的加到git的track中. Remeber when you stage files with "git add", you are copy/duplicating files.

- git add \<filename> 添加某一个指定的文件

- git rm --cached \<filename> 删除某一个指定的文件，如 git rm --cached hi2.txt

- git commit -m "your message". 但目录下有的文件被重新编辑之后，想要进行git commit，先git add . 或者git add \<filename> 来添加这个文档.
- git commit -a -m "your message", 这个-a表示的大概就是git add .的意思，所以这个命令就不用提前git add .来添加文件了。

- git log，如果git log中的log太长，可能只显示其中的一部分，可以按shift+z键来不断显示没显示的log. 
- git log --oneline会给出简略的log

- git diff 这个命令是为了显示你修改前和修改后的文档有什么不同。比如我修改了hi.txt中的内容，git diff就会显示出hi.txt中修改的部分。
	如果我先用了git add . , 那么再使用git diff就不能够显示出修改的部分了，因为修改后的文件已经被staged了。那么这种情况下可以使用git diff --cached来显示不同的地方。

- git mv hi.txt hey.txt,这个命令是修改文件名, 把文件由hi.txt改名为了hey.txt
  - git mv -f oldfolder newfolder  
  If there’s already a newfolder in your repo and you’d like to overwrite it use –force
  - git add -u newfolder  
  The -u option at the add command is important here, it’ll update already tracked files/folders.  
  关于重新命名文件夹和文件的命令，可以参见[这个网址][http://www.patrick-wied.at/blog/rename-files-and-folders-with-git]
  


#Git远程仓库的使用

但git clone 某个项目之后，至少可以看到一个名为origin的远程库，Git默认使用这个名字来标识所克隆的原始仓库。

- cd \<copied project\> 进入到克隆到本地的项目
- git remote 查看远程库的名字，会返回origin这个git默认的该项目的原始仓库
- git remote -v 可以显示对应的克隆地址，如果有多个远程仓库，那么这个命令会列出所有的远程仓库。但是只有地址是以SSH URL的远程仓库才能推送数据上去。
- git remote add [shortname] [url], 要添加一个新的远程仓库，可以指定一个简单的名字，以便将来方便引用。运行命令 git remote add [shortname] [url]之后，就会有shortname来指代这个远程仓库的名字。比如，git remote add pandoc git@github.com:JiajiaCong/Pandoc.git，或者git remote add origin git@github.com:JiajiaCong/Pandoc.git
- git fetch shortname/remote-name，从shortname说指代的仓库中来获取本地仓库中还没有的东西。
- git pull shortname/remote-name,将远程仓库中的内容抓取下来，并且将远端分支自动合并到本地仓库中。
- git remote rename originalname newname,这个名字是将远程仓库改名，由原来的名字改为新名字
- git remote rm remote-name/shortname，将remote-name或shortname代表的远程仓库移除。


# 一些小技巧

- 在本地删除了一些文件之后，如何通过命令行删除在github网站上的文件？
  比如想在本地删除hi.txt的文件，可以通过如下的命令来删除github网站上的文件。  
  - 先通过命令行删除本地文件，再通过命令行删除github上的文件
	 git rm hi.txt  
	 git commit -m"test"  
  	git push origin master  
  	这样就把本地和github上的hi.txt文件删除了。   
  - 没有通过命令行就先删除了本地文件，再通过命令行删除github上的文件   
  	git rm hi.txt(虽然已经被删除了，但还是要加上这一行，要让git知道hi.txt已经被删除了)   
	git add .（这一行可有可无）   
	git commit -m"test"   
	git push origin master   


- github上有的文件，本地没有，怎么把这些文件复制下来？
	- 办法1：将先有的本地内容给删除掉，然后再git clone一份下来
	- 办法2：目前还没有想到

- 删除本地的一个文件夹
	首先进入该文件夹所在的目录，然后运行rm filename -rf，这样就删除了整个文件夹

