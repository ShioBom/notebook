### Git


##### 初次使用Git
###### Git 全局设置:

    - git config --global user.name "ASxx" 
    - git config --global user.email "123456789@qq.com"

###### 创建 git 仓库:
- 开始创建项目
    - mkdir wap
    - cd wap
    - git init
    - touch README.md
    - git add README.md
    - git commit -m "first commit"
    - git remote add origin https://git.oschina.net/name/package.git
    - git push -u origin master

- 已有项目
    - cd existing_git_repo
    - git remote add origin https://git.oschina.net/name/package.git
    - git push -u origin master

##### 基本命令
-  `git init`：
初始化一个Git仓库

- 添加文件到Git仓库
    - `git add file.txt` ：
    可反复多次使用，添加多个文件，或者提交修改。

    - `git commit -m 'xxx'` ：
    xxx是本次提交的说明
    > git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执⾏行git commit就可以⼀一次性把暂存区的所有修改提交到分⽀支。 
-  `git status`：
随时掌握工作区的状态。

- `git diff` ：
查看具体修改了什么内容，查看difference 。
- `git log`:
 查看提交历史记录，显示从最近到最远的提交日志。以便确定要回退到的哪个版本
- git reflog 
 查看命令历史，以便确定要回到未来的哪个版本
###### 版本回退
- `git reset --hard HEAD^`:
`HEAD^`表示上一个版本，上上一个版本就是`HEAD^^`,往上100个版本`HEAD~100`
- `git reset --hard 3628164`
指定到具体的版本，3628164是版本号
 > 版本号没必要写全，前⼏几位就可以了，Git会⾃自动去找。当然也不能只写前⼀一两位，因为Git 可能会找到多个版本号，就⽆无法确定是哪⼀一个了。

###### 撤销修改
- `git checkout -- readme.txt`
丢弃工作区的修改，让这个文件回到最近一次git commit或git add时的状态.
- `git reset HEAD readme.txt`
把暂存区的修改回退到工作区。当我们⽤用HEAD时， 表⽰示新的版本。 
> 场景1：当你改乱了⼯工作区某个⽂文件的内容，想直接丢弃⼯工作区的修改时，⽤用命令git checkout -- file。 
场景2：当你不但改乱了⼯工作区某个⽂文件的内容，还添加到了暂存区时，想丢弃修改，分两 步，第⼀一步⽤用命令git reset HEAD file，就回到了场景1，第⼆二步按场景1操作。 
场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退⼀一节，不 过前提是没有推送到远程库。

### Git基本使用

@(Git)

#### 将本地项目上传到码云
1、码云上创建一个项目 testgit (名字随你)

2、本地创建一个文件夹D:/testgit，然后使用git bash    

3、cd 到本地文件夹中D:/testgit，

4、使用 `git init` 命令 ，初始化一个git 本地仓库（项目）,会在本地创建一个 .git 的文件夹

5、使用`git remote add origin https://gitee.com/你的码云用户名/testgit`      //添加远程仓库

6、使用 `git pull origin master` 命令，将码云上的仓库pull到本地文件夹

7、将要上传的文件，添加到刚刚创建的文件夹

8、使用`git add .` 或者 `git add + 文件名` (将文件保存到缓存区)

9、使用`git commit -m '描述新添加的文件内容'`  (就是注释)   （文件保存到本地仓库）

10、使用`git push origin master` ，将本地仓库推送到远程仓库
如果失败 ：`git push -f -u origin master`
#### 克隆
1、cd 到你想要保存远程仓库项目的文件夹
2、使用 git clone 远程仓库地址
####push& pull
##### `远程分支`
>远程分支有一个命名规范 —— 它们的格式是:`
<remote name>/<branch name>
`因此，如果你看到一个名为 `origin/master` 的分支，那么这个分支就叫 `master`，远程仓库的名称就是 `origin`。只有当远程仓库更新后，origin/master分支才会更新。
##### `git fetch`
- 从远程仓库下载本地仓库中缺失的提交记录
- 更新远程分支指针(如 `origin/master`)
- git fetch 并==不会改变你本地仓库的状态==。它==不会更新你的 master 分支==，也==不会修改你磁盘上的文件==。
- 如果要更新本地分支，需要`git merge origin/master`

> 远程分支反映了远程仓库在你最后一次与它通信时的状态，git fetch 就是你与远程仓库通信的方式了

##### `git pull`
- **git pull** 就是 `git fetch` 和 `git merge <just-fetched-branch>` 的缩写！
- **git pull --rebase**就是`git  fetch` 和`git  rebase <just-fetched-branch>` 的简写！
- 推送主分支
####在本地创建、删除、发布项目分支
过程
1. 在本地新建一个分支： `git branch newBranch`
2. 切换到你的新分支: `git checkout newBranch`
3. 创建并切换到新分支： `git checkout -b newBranch`
4. 将新分支发布在github上： `git push origin newBranch`
5. 在本地删除一个分支： `git branch -d newBranch`
6. 在github远程端删除一个分支： `git push origin :newBranch`   (分支名前的冒号代表删除)

>创建一个新的分支同时切换到新创建的分支 `git checkout -b <your-branch-name>`

#### 合并分支
#####方式一：git merge
1. 切换回主分支：`git checkout master`
2. 合并分支：`git merge origin/index-swiper`
3. 推送到远程仓库：`git push`
##### 方式二 ：git rebase 目标分支
#### 在git提交树上移动
##### HEAD（指定提交记录的哈希值）
head总是指向当前分支上最近一次==提交记录==，大多数修改提交树的git命令都是从改变head的指向开始的，通常指向分支名，
git commit  此时head指向提交代码的分支名
##### 分离HEAD
git checkout 提交记录
指向具体的提交记录
##### git log
查看提交记录的哈希值
##### 相对引用
- 使用 `^` 向上移动 1 个提交记录，如`git checkout master^`
- 使用 `~<num>` 向上移动多个提交记录，num默认为1，如 `~3`,git checkout master~3
- 也可以把HEAD作为相对引用的参照，`git checkout HEAD^`,移动到上一个提交记录，我们可以一直使用 `HEAD^` 向上移动
###### 强制修改分支位置
`git branch -f master HEAD~3`，将 master 分支强制指向 HEAD 的第 3 级父提交。
###### 撤销变更
- 方式一：git reset

> git reset 通过把分支记录回退几个提交记录来实现撤销改动。你可以将这想象成“改写历史”。git reset 向上移动分支，原来指向的提交记录就跟从来没有提交过一样

- 方式二：git revert

> 虽然在你的本地分支中使用 git reset 很方便，但是这种“改写历史”的方法对大家一起使用的远程分支是无效的哦！为了撤销更改并分享给别人，我们需要使用 git revert。实际就是撤销更改后重新提交一次，revert 之后就可以把你的更改推送到远程仓库与别人分享啦。

 