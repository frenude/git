# Git

### 1.`git init `

- 创建当前目录为本地仓库
- `git init  <catalogue> `创建catalogue目录为本地仓库

### 2.`git add`

- `git add <path>`命令将文件内容添加到索引(将修改添加到暂存区)

### 3.`git clone` 

- `git clone <版本库的网址> <本地目录名>`从远程主机克隆一个版本库

### 4.`git status`

- 用于显示工作目录和暂存区的状态

### 5.`git diff`

- 显示提交和工作树等之间的更改

### 6.`git commit`

- 将更改记录(提交)到存储库
- 使用前提该文件已经被`git add`
- `git commit -m ' 描述信息 '`添加描述
- 修改后再次提交可以简写成`git commit -am '描述信息'`

### 7.`git reset`

- 命令用于将当前`HEAD`重置到指定状态。一般用于撤消之前的一些操作 相当于`ctrl +z`
- `git reset --soft HEAD^` 回滚到最近一次提交 相当于版本`HEAD`的切换(本地仓库)
- `git reset --hard HEAD~3  `回滚三次提交 ，并删除后三次删除

### 8.`git rm`

- 从工作区和索引中删除文件。
- 使用 `git rm` 来删除文件，同时还会将这个删除操作记录下来；而使用 `rm` 来删除文件，仅仅是删除了物理文件，没有将其从 `git` 的记录中剔除

### 9.`git mv`

- 移动或重命名文件，目录或符号链接。

### 10.`git branch`

- 用于列出，创建或删除分支。
- `git branch`列出本地仓库的分支
- `git branch -r`查看远程分支
- `git branch -a`查看本地和远程分支（远程分支基本为`origin/dev`这种类型）
- `git branch newName`创建一个`newName` 的分支
- `git branch -m <name>  <changName>` 给分支改名字
- `git branch -d [branchname]`删除本地已合并的分支
- `git branch -D [branchName]`强制删除分支
- `git branch -vv`看本地分支关联（跟踪）的远程分支之间的对应关系
- 查看当前远程仓库信息 `git remote -vv`
- git手动建立关系`git branch --track xx origin/newbranch`本地xx和远程dev 建立关系(本地没有的分支)
- `git branch --set-upstream-to=origin/<branch> branchName` 设置本地分支追踪远程分支

### 11.`git checkout`

- 切换分支或恢复工作树文件
- `rm -rf files`删除了某个文件且没有`git commit 提交`可以使用`git checkout files`通过所以恢复 

### 12.`git merge`

- 将两个或两个以上的开发历史加入(合并)一起。

### 13.`git log`

- 显示提交日志信息。

### 14.`git stash`

- 将更改储藏在脏工作目录中。
- 此时操作会和上一次操作有冲突但是不想丢弃本次操作可以保存至脏读目录中
- 这个命令所储藏的修改可以使用`git stash list`列出，使用`git stash show`进行检查，并使用`git stash apply`恢复(可能在不同的提交之上)。调用没有任何参数的`git stash`相当于`git stash save`

### 15.`git tag`

- 打标签
- `git tag` 列出现有的标签
- 创建轻量级标签lw`git tag xx`
- `git tag -a v1.4 -m 'my version 1.4'` `-a` 指定标签名字，`-m `指定描述
- `git show `展示版本信息
- `git tag -d v1.4`删除标签
- 打完标签推到远程`git push origin [tagname]`
- 一次性推送本地所以标签`git push origin --tags`

### 16.`git fetch`

- 从另一个存储库下载对象和引用。（取回）
- `git fetch <远程主机名>`将某个远程主机的更新
- 更新所有分支` git fetch`

### 17.`git pull`

- 从另一个存储库或本地分支获取并集成(整合)

- `git pull <远程主机名> <远程分支名>:<本地分支名>`下载远程主机的分支到本地分支如果没有新建本地分支

- 如果远程分支想合并当前分支合并` git pull origin <远程分支名>`相当于`git fetch origin`+` git merge origin/分支名`

- 如果当前分支与远程分支存在追踪关系，`git pull`就可以省略远程分支名` git pull origin`

- 如果合并需要采用`rebase`模式，可以使用`–rebase`选项。`git pull --rebase <远程主机名> <远程分支名>:<本地分支名>`

- `git fetch`和`git pull`的区别

  - `git fetch`：相当于是从远程获取最新版本到本地，不会自动合并。

    ```shell
    $ git fetch origin master
    $ git log -p master..origin/master
    $ git merge origin/master
    ```

  - 以上命令的含义：

    - 首先从远程的`origin`的`master`主分支下载最新的版本到`origin/master`分支上
    - 然后比较本地的`master`分支和`origin/master`分支的差别
    - 最后进行合并

  -  `git pull`：相当于是从远程获取最新版本并`merge`到本地

    - `git pull origin master`
    - `git fetch` 和 `git merge`

### 18.`git push`

- 用于将本地分支的更新，推送到远程主机.

- 创建远程分支`git push <通常为origin> <本地分支名>:<远程分支名>`

- 删除远程分支:

  - `git push origin :master`把空的推到远程去就相当于删除远程的分支了
  - `git push origin --delete master`删除远程master分支

- 如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。`git push origin`

- 不管是否存在对应的远程分支，将本地的所有分支都推送到远程主机，这时需要使用`–all`选项

  ```shell
  $ git push --all origin
  ```

- 如果远程主机的版本比本地版本更新，推送时Git会报错，要求先在本地做`git pull`合并差异，然后再推送到远程主机。这时，如果你一定要推送，可以使用`–force`选项。

  ```shell
  $ git push --force origin
  ```

- `git push`不会推送标签(tag)，除非使用`–tags`选项。`git push origin --tags`

- 将当前分支推送到远程的同名的简单方法，如下 - 

  ```shell
  $ git push origin HEAD
  ```

### 19.`git remote`

- 管理一组跟踪的存储库。
- `git remote`不带参数，列出已经存在的远程分支
- ``git remote -v | --verbose` 列出详细信息，在每一个名字后面列出其远程url`
- 添加远程库`git remote add <库名字> <url>`
- 模仿  `git clone`，但只跟踪选定的分支`git remote add -f -t master -m master origin git://example.com/git.git/`

### 20.`git show`

- 显示各种类型的对象。

### 21.`git shortlog`

- 命令用于汇总`git`日志输出
- 统计人员的`commit`:`git shortlog -s -n`

### 22.`git describe`

- 显示离当前提交最近的标签。

### 23.`git rebase`

- 另一个分支基础之上重新应用，用于把一个分支的修改合并到当前分支
- 相当于`merge` 但是更明显 是一串 比较清晰
- `git rebase branch1 branch2`

### 24.`git cherry-pick `

- 快速复制合并分支