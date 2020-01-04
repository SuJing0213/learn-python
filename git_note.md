## git学习笔记

### git基础

#### Git配置
```shell
git config --local    #只对某个仓库有效，local优先级比global高
git config --global   #对当前用户所有仓库有效
git config --system   #对系统所有登陆的用户有效

git config --global user.name''   
git config --global user.email''  #系统会自动发邮件给变更者

git config --system --list
```

#### 创建Git仓库
1. 把已有项目代码纳入Git管理
```shell
cd 项目所在文件夹
git init
```
2. 新建的项目直接用Git管理
```shell
cd 某个文件夹
git init your_project#当前路径下创建和项目名称同名的文件夹
git init your_project

git add 文件名
git commit -m‘’#变更信息
```
#### 工作区和暂存区
工作目录 -> 暂存区 -> 版本历史
untracked files：之前未被管理过的文件
```shell
git add 多个文件/文件夹
git add -u  #工作区中未管理的多个文件一起提交到暂存区
```

#### 给文件重命名的方法
```shell
mv readme readme.md
git add readme.md
git rm readme       #git知道你是重命名

or

git mv readme readme.txt
```
#### git log查看版本历史
```shell
git log --oneline           #commit列表
git log -n4 --oneline       #只查看最近的4个
git log --all               #所有分支的情况
git log --all --graph       #图像化，具有演进关系
git log --oneline -all
git log --oneline -all -n4  #所有分支最近的取四个
```

####图形界面工具查看版本历史
Author：
Commiter：从别的分支拿过来的，Author还是原作者
```shell
gitk
```

分支：独立的开发空间
tag：里程碑
```shell
git checkout 分支名 #切换分支
```
#### 三个对象之间的关系
* commit
* tree
* blob

### 常见场景
#### 删除不需要的分支
```shell
git branch -av       #查看还有多少分支
git branch -d 分支名  #如果报警，用-D，彻底清除不想要的分支
```

#### 修改最新commit的message
```shell
git branch -av     #查看目前在哪个分支
git log -1         #查看commit信息
git commit --amend #进入一个文件直接修改即可
```

#### 修改老旧commit的message
```shell
git rebase -i 待改分支名的父亲 #变基
pick -> r                   #然后在下一个界面里改
```

#### 将连续的多个commit整理成1个
```shell
git rebase -i 待改分支名的父亲id       #要合成commit们的父亲
p -> s(quash)                       #要被合成的commit
```

#### 将间隔的几个commit整理成1个
```shell 
git rebase -i 待改分支名的父亲id #进入下一个页面调整顺序
```

#### 比较暂存区和HEAD所含文件的差异
```shell
git diff --cached   #确认变更没有问题再commit
```

#### 比较工作区和暂存区所含文件的差异
```shell
git diff
git diff -- 文件名
```

#### 暂存区恢复成和HEAD一样
```shell
git reset HEAD
```

#### 工作区恢复成暂存区
```shell
git checkout -- 文件名
```

#### 取消暂存区部分文件的更改
```shell
git reset HEAD --文件名
```

#### 消除最近几次提交的branch
```shell
git reset --hard id   #彻底丢了，慎重
```

#### 不同提交指定文件的差异
```
git diff id1 id2 -- 文件名
```

#### 正确删除文件
```
git rm filename 
```

#### 开发中临时加塞了紧急任务
```shell
git stash       #存到栈里，工作区就干净了
完成紧急工作
git stash apply #工作区恢复，此时stash中的内容还在
or
git reset --hard HEAD
git stash pop   #工作区恢复，此时stash中的内容不在

git stash list
```

#### 不需要Git管理的文件
```shell
.gitignore #git仓库中哪些文件不需要被管理
doc/       #管doc文件夹但是不管他下面的文件
```
为什么要分支？