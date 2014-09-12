Git
===
学习的环境是在电脑的E盘下，有一个Github的文件夹，文件夹下面有一个叫做test的文件夹。文件夹里有两个文档，一个是hi.txt，一个是hi2.txt.


- ls
- pwd
- cd \<project file>
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




