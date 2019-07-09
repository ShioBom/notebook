
[TOC]
#### git配置指令
##### 删除git中缓存的用户名和密码
- 运行一下指令缓存输入的用户名和密码：

```
git config --global credential.helper wincred
```

- 清除掉缓存在git中的用户名和密码

```
git credential-manager uninstall
```
##### 常用git操作
1. `git reflog`: 历史记录
2. `git reset --soft e79fcfb`: 回退到某次提交，gi并且把commit的内容撤回到暂存区
4. `git status`：查看git状态
##### 撤销修改
- 没有执行add指令
    1. `git checkout -- <file>`
- 执行了add指令，没执行commit指令
    1. `git reset HEAD <file> ` ：暂存区内容回退
    2. `git checkout -- <file>`：丢弃工作区修改
- 执行了commit，未提交到远程
    1. `git reset --hard <commit_id>`：版本回退
##### 版本回退
1. `git log`：查看提交历史
2. `git reset --hard <commit_id> `：版本回退
3. `git reflog`：查看命令历史
4. `git diff`：查看工作区与版本库中的不同
5. `git diff HEAD -- <file>`：查看某个文件的不同

##### 删除文件
- 文件被提交到版本库，想删除，有两步
    - `rm <file>` 删除工作区文件
    - `git rm <file>`删除版本库的文件
    - `git commit -m "remove file"`
##### 解决冲突
- `git pull`拉取代码
- 使用vscode打开冲突文件
- 解决冲突
- `git commit -m "解决冲突“
##### 分支管理
##### 分支暂存
1. `git stash [save "msg"]`：储藏当前暂存的文件，[并提交储藏信息],[]是选填的内容
2. `git stash list`: 储藏列表
3. `git stash apply stash@{0}`: 应用某次储藏(不会删除那一次)
4. `git stash pop`: 应用并弹出栈顶的储藏
5. `git stash drop stash@{0}`:删除某次储藏

