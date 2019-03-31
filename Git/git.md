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
