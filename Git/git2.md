
[TOC]
#### git配置命令
###### 删除git中缓存的用户名和密码
- 运行一下命令缓存输入的用户名和密码：

```
git config --global credential.helper wincred
```

- 清除掉缓存在git中的用户名和密码

```
git credential-manager uninstall
```
###### 常用git操作
1. `git reflog`: 历史记录
2. `git reset --soft e79fcfb`: 回退到某次提交，并且把commit的内容撤回到暂存区
3. `git stash [save "msg"]`：储藏当前暂存的文件，[并提交储藏信息]
   1. `git stash list`: 储藏列表
   2. `git stash apply stash@{0}`: 应用某次储藏(不会删除那一次)
   3. `git stash pop`: 应用并弹出栈顶的储藏
4. `git status`：查看git状态

