妙味课堂玩转git与github目前学到第9节,8,9节多人协作与解决冲突已经开始懵逼了
## git管理的是修改,而不是文件 
ctr +cls可以清屏
git其实是一个工具,作用是版本控制
svn与git的区别
svn 集成式 一个中央服务器,所有人都是
git 分布式版本控制
### git的三个区
工作区:将工作区里面的内容提交到暂存区,再通过暂存区提交到版本库
暂存区:保护工作区和版本库
版本库(区):
### 
`git init `初始化一个本地仓库,里面会生成一个.git的文件夹,记住,千万不要修改里面的东西
### 如何将github上的项目拉到本地:
0. `git status `可以查看工作区的状态,`git log`可以查看提交日志,显示顺序是从最近到最远,`git log --oneline`可以查看提交记录的简短日志,,`git log -n`展示最近的n条提交日志,比如`git log -3`可以查看最近提交的三条日志,`git log -3 --oneline`查看最近提交的三条日志的简短版本,`git reflog`可以用来记录每一次命令,从而实现在不同版本之间进行穿梭
1. 首先在github上建立一个仓库,复制项目的地址如https://xxx,在bash中,先用cd进入项目将要存储的路径,然后使用命令 `git clone https://xxx`即可,在本地不需要初始化仓库,拉下来的就是一个仓库,如果是自己github上的项目,那么以后就可以直接提交
2. 设置贡献者 `git config --global user.name "11Josey"`  `git config --global user.email "2535051276@qq.com"`,删除配置的用户名和邮箱`git config --global unset user.name` `git config --global unset user.name`,也可以重新执行配置用户名和密码命令,进行覆盖
3. 其中,不写内容就是参看名字和邮箱,可以利用`git config --list`命令查看所有的配置
3. 通过 `git add file.txt`将file.txt从工作区的修改放到暂存区,通过 git status命令可以查看添加的状态,再通过`git commit -m "message"`命令将暂存区的**所有**修改提交到版本库,同时添加说明信息,说明一点,`git add .` 是全部添加到暂存区,而不用一个个的添加
4. 无法通过工作区向版本库里面直接添加文件,但是有一个连写的命令 `git commit -a -m "message"`,这个命令的本质还是先将工作区的文件添加到暂存区,再从暂存区提交到版本库
5. 对比  `git diff`指的是工作区与暂存区的对比 `git diff --cached(staged)`指的是暂存区与版本库之间的差异对比 `git diff master`工作区与版本库之间的差异对比
6. 改动文件,已经添加到暂存区了,后续发现想撤销这次改动,使用 `git reset HEAD file.txt`,那么暂存区的版本就会回退到上一次的版本,但是工作区依然是修改后的版本,再使用 `git checkout -- file.txt`(其实是用版本库里面的版本替换工作区的版本),就可以将工作区的版本恢复到上一次,如果你不但改错了东西,还从暂存区提交到了版本库,那么就版本回退,使用版本回退,那么三个区的修改都会被丢掉

### git中的忽略文件

.gitignore文件里面写忽略的文件,那么git就不会跟踪这些文件
在windows下新建一个无名文件.gitignore有以下四种方法(这些方法对其他任何无名文件都可以)

1. 使用git命令行,输入命令`touch gitignore`
2. shift+鼠标右键,打开当命目录下的命令行,输入`echo test>.gitignore`
3. 直接新建文本文档,命名为.gitignore.,会有弹窗提示,点击确定即可
4. sublime等直接另存为给个.gitignore可以

.gitignore中书写文件需要一行一行书写

- '/index.html'忽略根目录(.git文件所在的目录)下的index.html文件
- '/js/*.*/`忽略下一级js文件中的所有文件
- '/js/*.js/''忽略下一级js文件中的所有js文件
- '/.gitigonre '忽略.gitignore文件

 将file.txt文件添加到暂存区,如果工作区中删除了file.txt文件,运用`git rm file.txt`可以删除暂存区中的这个文件,但是如果工作区中的相应文件没有删除,此命令无法删除暂存区中的对应文件,此时需要调用 `git rm -f file.txt`,但是这个命令会将工作区的文件也删掉,`git rm --cached file.txt`只删掉暂存区中的文件,工作区中的对应文件不会被删掉
8. 指定文件回退 ` git checkout -- 123fyfg file.txt `,丢掉工作区的修改,
9. 版本回退(回到过去) `git resest --hard 123dey45`
   `git reset --hard HEAD^ `向前回退一个版本
   `git reset --hard HEAD~num `向前回退num个版本
   `git reflog` 回到未来,在不同版本之间穿梭
10. **本地电脑文件同步到github**
	git remote
	git remote -v
	git fetch将github上的仓库拉取到本地,然后使用git diff master origin/master命令来查看本地与远程的区别

## 创建分支与合并分支
查看分支 git branch 
创建分支 git branch name
切换分支 git checkout name
创建+切换分支 git checkout -b name
删除分支 git branch -d name,**但是必须切到别的分支才执行删除这个分支**,就像360不可以卸载360一样
处在merge分支状态下,合并dev分支到merge分支 git merge dev



 
