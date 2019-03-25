[原文网址][1]
## 版本库
#### 又名仓库，repository，可以简单理解为一个目录。
### 创建版本库，选择一个合适的地方，创建一个空目录 learngit 为仓库名
+ mkdir learngit
+ cd learngit
+ pwd -- 查看当前目录
### 通过git init 将该目录变成Git可以管理的仓库，初始化仓库
+ git init

### 将文件添加到版本库
<big>**版本控制系统可以告诉你每次的改动，但没法跟踪文件的变化**</big>
#### 1 用命令git add 把文件添加到仓库，该文件在创建的仓库下
+ git add readme.txt

#### 2 用命令git commit 把文件提交到仓库
+ git commit -m "wrote a readme file"

### git status 命令可以让我们时刻掌握仓库当前的状态
+ git status

### git diff 查看文件修改内容
+ git diff readme.txt

[1]: https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840038939c291467cc7c747b1810aab2fb8863508000
