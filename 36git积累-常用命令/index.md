# Git 积累 & 常用命令


# Git 积累 & 常用命令



本文最新原文在 [Github](https://github.com/Staok/Git-Learning) / [Gitee](https://gitee.com/staok/Git-Learning) 仓库，其它地方不会跟进。



## 开始



Git & Github 学习：

- https://learngitbranching.js.org/?locale=zh_CN。
- [git - the simple guide - no deep shit!](https://rogerdudler.github.io/git-guide/index.zh.html)。
- [GitHub 入门文档 - GitHub 文档](https://docs.github.com/zh/get-started)。

Gerrit 学习：https://www.cnblogs.com/111testing/p/9450530.html。



## Git 配置

注意：Git 仓库，要么在 Win 要么在 Linux（两个平台文件换行符不同），不要都用。



### 信息

查看：

```bash
git config --global --list
```



基本信息配置：

```bash
# 要换成自己邮箱和名字
git config --global user.name "<name>"
git config --global user.email <email link>
```



### 环境配置

PC（这里默认指 Win）、linux host、gerrit、github/gitee 等互相访问。



- 给 Linux HOST 添加 PC 的 SSH Key，自己 PC 才能访问到 Linux HOST。

  给 Linux HOST 添加 PC 本地 SSH Key，用于 使用 VsCode + Remote-SSH 插件 进行远程开发。

  确保 SSH 等插件 和 VsCode 都是最新的（新版 VsCode 和 老版的 SSH 插件 也是失败的原因）。
  
  各种 VScode Remote SSH 连接失败，见 VsCode 右下角的当前卡在哪一步 和 `~/.vscode-server/<commit-id>.log` 日志文件的报错，来具体网搜方法。
  
  下面为产生 ssh key 的命令。
  
  ```bash
  # 对于 Linux，即在 ~/.ssh/ 下生成 ssh-key（.pub 文件）。
  # 对于 Win，即在 C:\Users\<用户名>\.ssh\ 下生成 ssh-key（.pub 文件）。
  # 一路默认回车即可。
  ssh-keygen -t rsa
  ```

- 也给 Gitghub 或 Gitee 添加自己的 ssh-key，通过 SSH and GPG keys -> New SSH key。

  即可访问 Github 仓库。

- 给 CI/CD（持续集成 / 部署） 服务器上的 Gerrit（或其他 仓库管理平台） 添加 本地（PC 和  自己的 Linux HOST 服务器） SSH Key，自己的 PC 和 Linux HOST 才能访问到 Gerrit。




### ssh 额外配置相关

ssh 配置相关集合 https://blog.csdn.net/weixin_47661174/article/details/126020594。

ssh 免密登录 https://blog.xieqiaokang.com/posts/3517905979.html，如下。

```bash
# 使用下述命令将 id_rsa.pub 这个 ssh-key 文件 加入到 例如 192.168.xx.xxx 机器的 xxx 用户里
# 即机器的 ~/.ssh/authorized_keys 文件里面
ssh-copy-id -i id_rsa.pub xxx@192.168.xx.xxx
```

ssh 快速登录

```bash
# 在 C:\Users\<用户名>\.ssh\config 文件里面添加快速登录选项，下面例子：
# Read more about SSH config files: https://linux.die.net/man/5/ssh_config
Host ti3	                                    # 主机名，随便取
    HostName 202.38.xx.xxx                      # 主机IP（机器B）
    Port xxxxx                                  # 若为默认端口22，可不设定此项
    User hhqingwa	                            # 在机器B上的用户名
    IdentityFile C:\Users\<用户名>\.ssh\id_rsa     # 本机私钥路径，若为默认的 id_rsa，则可不填

# 配置了 config 文件后，快速登陆命令
ssh ti3     # 等效于 ssh hhqingwa@202.38.xx.xxx
```



### Win 挂载 Linux 服务器 文件系统

Win 上连接到远程 Linux HOST 用于 一些 查看文件、操作文件、推拉文件 等 杂活儿。方便 win 上使用脚本 将 Linux 服务器端的一些编译生成的文件（Win 可直接访问）等直接推到 Linux 板子（scp 命令）里等。

推荐 Windows 下使用 SSHFS 通过 samba 协议挂载远程 Linux 服务器 文件系统。



在计算机页面上边栏找到 `映射网络驱动器`，填入地址，且 注意勾选 `使用其他凭据链接`。

地址如：`\\<Linux 服务器 IP 地址>\<Linux 服务器上自己用户名>`。

https://blog.csdn.net/qq_53517370/article/details/128757935。



## Git 命令日常其它

下面的都是比较重要的，建议都熟悉。



### 下载仓库

```bash
# 一般情况
git clone <仓库链接>

# 下载整个仓库，包括子仓库
git clone --recurse-submodules https://github.com/your-github-userid

# 更新已经存在的仓库，包括子仓库
git submodule update --init --recursive
```



### 日常更新仓库

```bash
# 推荐使用 git pull --rebase，在 pull 时候若本地 git 目录不干净会提示而不会强行 merge

# 对于 repo 管理的各个仓库

# 首先保证所有仓库在各自分支最后一次提交
# 若误改动了文件，则删掉该文件（链接文件也要删掉源文件），再 repo sync 即可恢复
repo sync -j4
repo forall -c git checkout master
repo forall -c git pull --rebase

# 一条命令
(repo sync -j4) && (repo forall -c git checkout master) && (repo forall -c git pull --rebase)
```



### 提交

```bash
git add <文件名>             # 只添加<文件名>文件
    git add -u              # 添加所有修改过的文件
    git add .               # 添加所有更改

git commit  -m "..."        # 提交一次
```



提交代码 commit 加上 -s：https://www.coder.work/article/7800053

> 上传patch的人不一定是作者，提交commit需要签名，如果几个人一起写一个commit，原则上需要追加 signed-off



```bash
git commit --amend          # 把新的内容添加到上一次 commit 里面，参考 https://www.jianshu.com/p/7d40838883af
# 有的会打开 vim 编辑器，有的会打开 nano 编辑器，都是编辑后再保存并退出后即可。
```

git commit --amend 修改 commit 后，保存和退出方法：

https://blog.csdn.net/u010168781/article/details/81902689

下面是 git 默认的文本编辑器是 nano 的操作：

- 若不修改 commit，直接 ctrl + x 退出。

- 若修改了 commit，ctrl + x，提醒是否保存，输大写的 Y，再回车。

- 这种方法推荐：

  > 修改 commit 记录中，修改好后，按 ctrl+o，出现 .git /commit_editmsg 界面，回车，然后按下 ctrl + x 就可以保存修改了。

- ```bash
  # git 默认的文本编辑器是 nano，执行下面的命令将 git 的文本编辑器改为我们熟悉的 vim
  git config --global core.editor vim
  ```



### 推送

```bash
# 往 目标 remote 仓库 的 目标 branch 上面推
git push <remote name> <remote branch>
```



注意：若 本地提交之后，再 push 到远端显示失败，则可能是 本地在修改代码的中途 远端更新了代码，这时，`git pull --rebase` 拉取远端最新的，若不冲突则会合并，并且本地最后一次提交会成为本地最新的提交，这时候再 push 即可。



### More



```bash
# 查看所有分支
git branch -a

# 切换到某个分支比如 XX（本地或远程的）
git checkout XX 或者 git switch XX

# 注意，要修改远程某分支，则本地先切换到目标远程分支，修改后，git push 到 对应的远程分支！

# 切回 main 分支
git checkout main 或者 git switch main

# 删除某个分支 xxx（本地或远程的）
git branch -d xxx
```



status       显示当前修改、提交状态

diff            显示差异：https://blog.csdn.net/qq_39505245/article/details/119899171

stash         暂存：https://blog.csdn.net/weixin_42433094/article/details/124603640

blame       单个文件当前里面每一行的修改人：https://blog.csdn.net/young_old_boy/article/details/121792481

log             单个文件的修改历史记录：https://blog.csdn.net/sunxiaopengsun/article/details/129227548

Git 修改历史提交 https://www.php.cn/faq/487568.html

​			`git commit --amend`

​			`git rebase -i HEAD~<上移节点数>`

如果您想丢弃本地的修改并还原到最近一次提交的状态

​	`git reset --hard HEAD`



git 中 rebase 和 merge 的区分

- https://blog.csdn.net/weixin_42310154/article/details/119004977
- https://zhuanlan.zhihu.com/p/558666061



win 没有编辑文件 复制到 linux 端 后 git 显示 文件 mode 修改了，让 git 忽略

https://blog.csdn.net/Lekaor/article/details/132804005

```bash
git config core.filemode false
git config --global core.filemode false
```



### Git 设置默认配置

以下直接在 bash 或 cmd 或 powerShell 里面键入



```bash
git config --global pull.rebase true
git config --global push.default simple
git config --global core.autocrlf input
git config --global core.quotepath false
```



Git 设置命令简写

```bash
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.br branch
git config --global alias.di diff
git config --global alias.sw show
git config --global alias.hist 'log --pretty=format:"%h %ad | %s:d[%an]" --graph --date=short'
git config --global alias.type 'cat-file -t'
git config --global alias.dump 'cat-file -p'
```



## Git 团队协作中常用术语

WIP PTAL CC LGTM 等解释 https://blog.csdn.net/kunyus/article/details/93472646。

- **WIP** —  Work in progress, do not merge yet —  开发中。
- LGTM —  Looks good to me —  Riview 完别人的 PR ，对我来说，觉得没有问题。
- PTAL —  Please take a look —  帮我看下，一般都是请别人 review 自己的 PR。
- **CC** —  Carbon copy —  一般代表抄送别人的意思。
- RFC  —  request for comments —  我觉得这个想法很好，我们来一起讨论下。
- IIRC  —  if I recall correctly —  如果我没记错。
- ACK  —  acknowledgement —  我确认了或者我接受了，我承认了。
- NACK/NAK — negative acknowledgement —  我不同意。



## 提交 Patch 和 规范



- 严重注意：每一个在 Gerrit 上的提交内的文件是要本次开发内容或功能全部的相关文件，不要分两次等提交，这样拉下来一次就可以编译本次的功能，而不必拉取多次拼起来。



Patch 的 commit 撰写规范

- 手把手教你给Linux内核发patch		https://zhuanlan.zhihu.com/p/87955006。

- Patch提交规范！重要，圈内文章 	https://confluence.bbl.com/pages/viewpage.action?pageId=4688712。

- 提交编写信息规范：

  https://docs.scipy.org/doc/scipy/dev/contributor/development_workflow.html

  https://www.conventionalcommits.org/zh-hans/v1.0.0/

  > ```
  > eg. ENH: add functionality X to SciPy.<submodule>.
  > 
  > API: an (incompatible) API change
  > BENCH: changes to the benchmark suite
  > BLD: change related to building SciPy
  > BUG: bug fix
  > DEP: deprecate something, or remove a deprecated object
  > DEV: development tool or utility
  > DOC: documentation
  > ENH: enhancement
  > MAINT: maintenance commit (refactoring, typos, etc.)
  > REV: revert an earlier commit
  > STY: style fix (whitespace, PEP8)
  > TST: addition or modification of tests
  > REL: related to releasing SciPy
  > ```

提交 patch 撰写 描述可以丰富一些，如

```
ENH: <模块名>:简述

<详细描述>

JIRA: AAA-42 （带上 测试人员 在 比如 jira 的 bug 管理系统里面报问题的 jira 编号）
TEST: <测试情况>
```



## Git & Gerrit 常见问题解决



### 修改 Gerrit 上某次提交

注，下面只文字描述备忘，第一次最好找人给演示一遍就好了，只文字描述很抽象。

1. 保证 自己 本地 git 仓库 与 远程仓库 为一致的。即 `git log` 后，本地最近的提交显示 `"HEAD -> <本地分支>, <远程分支>."`。

   如果本地已经有修改但没有 `add`，如果要暂存可以用 `git stash` 命令（具体查相关教程），然后，先 `git reset --hard HEAD` 恢复到本地最后一次提交，然后 `git pull --rebase` 保持本地仓库与远程一致。

   若本地仓库 比远程仓库多提交好几次，首先确保是否已经提交防丢，然后，要先 回退，使用 `git reset --hard HEAD^^..`（一个^是回退一次），然后 `git pull --rebase` 保持本地仓库与远程一致。

2. 在保证本地仓库与远程仓库一致后，在 Gerrit 上 某个提交的页面，右上角 三个点 找出 `Download patch`，在 `Cherry Pick` 右边点 复制图标，粘贴 到 本地仓库下的命令行 执行。

   这一步是下载一次 暂存 在 Gerrit 上的一个提交记录 到本地 而且作为 一个 新的提交。

3. 修改文件，`git add <添加所有改动的文件，选项可以是 -u 或 . 等>`，`git commit --amend（与最近一次提交合并）`，再 `git push <remote name> <remote branch>`，这样 Gerrit 上那个提交的页面就会多一次提交（Patchset）.

4. 然后本地仓库恢复 Download Cherry  patch 之前的、与远程仓库 最新的状态：`git reset --hard HEAD^`。




### 修改 Gerrit 上某次提交的冲突

1. 通过 cherry-pick 下载该 patch，会提示冲突文件，cherry-pick 会 “卡” 在这里等待解决冲突。
2. 显示冲突的地方 `git diff`。若显示没有冲突，则就是没冲突，再提交一次，gerrit 上面就好了。
3. 修改冲突。
4. 添加 `git add -u`。
5. 让 cherry-pick 继续 `git cherry-pick --continue`。再看看状态 `git status`。
6. 推送 `git push <remote name> <remote branch>`。



### 准备推送远端但是远端比本地节点更新 & 各状态之间切换

如果已经 add 但还没有 commit，直接 `git stash`（用 `git stash show` 查看）保存到栈区，再 `git pull`，再 `git stash pop`。

若已经 commit，先 `git reset --soft HEAD^` 撤回本次 commit 到暂存区，再就和上面一样操作。



如果回退到 暂存区（add 之后的状态） 也不想要了，先 `git reset` 取消文件处于暂存区，如果有 Untracked files 则 `git clean -f` 删除 Untracked files，然后 `git reset --hard HEAD` 回到最后一次提交的状态。



git stash 各个命令 https://blog.csdn.net/qq_44333320/article/details/128538380。



更多 git 仓库各个状态间切换

可以参考 https://blog.csdn.net/2301_82244279/article/details/140393081

若文件处于修改但未 add 的 状态，使用 `git checkout -- <file(s)>` 来恢复文件为未修改的状态。

commit 后 的状态恢复到 add 后的状态：`git restore --staged <file(s)>`。

commit 后 的状态 恢复到 上一次 提交（丢弃这个文件在这个 commit 的 修改）：`git checkout HEAD^ -- <file(s)>`。



### 多个 git 提交 合并为 一个

https://www.cnblogs.com/Simoon/p/18535021



如果要调整最新的两个提交，执行

`git rebase -i HEAD~2`



打开编辑后，将除了第一个pick后面的pick都改为 squash，例如

```
pick abc1234 Commit 1
squash def5678 Commit 2
squash aefsg48 Commit 3
squash ...
```



提交

`git push --force-with-lease`

> 使用 `--force-with-lease` 比 `--force` 更安全，因为它会确保在你推送之前，远程仓库没有其他人提交的更改。



### git 已经将个别文件夹添加到了 gitignore 中 但是 git 仍提示文件有修改

参考：

https://blog.csdn.net/qq_40028324/article/details/141716530



设置 `.gitignore` 文件 https://www.php.cn/faq/680791.html



### clone 仓库后，push 时 提示 miss hooks

提示错误例子：

```bash
remote: ERROR: commit xxxxx: missing Change-Id in message footer
remote:
remote: Hint: to automatically insert a Change-Id, install the hook:
remote:   gitdir=$(git rev-parse --git-dir); scp -p -P 11111 XXX1@gerrit.AAA.com:hooks/commit-msg ${gitdir}/hooks/
remote: or, for http(s):
remote:   f="$(git rev-parse --git-dir)/hooks/commit-msg"; curl -o "$f" https://gerrit.AAA.com/tools/hooks/commit-msg ; chmod +x "$f"
remote: and then amend the commit:
remote:   git commit --amend --no-edit
remote: Finally, push your changes again
```



按照上面例子提示的，看自己的实际报错信息，执行 类似这两句话 ：

```bash
gitdir=$(git rev-parse --git-dir); scp -p -P 11111 XXX1@gerrit.AAA.com:hooks/commit-msg ${gitdir}/hooks/

git commit --amend --no-edit
```



若第一句话执行提示错误：

```
subsystem request failed on channel 0
scp: Connection closed
```

参考这个 https://www.cnblogs.com/0xcafebabe/p/17960208，在 scp 命令后加一个 `-O` 选项，即可成功。

即执行：

```bash
gitdir=$(git rev-parse --git-dir); scp -O -p -P 11111 XXX1@gerrit.AAA.com:hooks/commit-msg ${gitdir}/hooks/
```



### 别的 win 账户 clone 的仓库，自己账户再操作仓库的安全提示

```bash
PS D:\AAA> git status
fatal: detected dubious ownership in repository at 'D:/AAA'
'D:/AAA' is owned by:
        XXX1 (<sn>)
but the current user is:
        XXX2 (<sn>)
To add an exception for this directory, call:

        git config --global --add safe.directory D:/AAA
```

这里就是别的 win 账户 clone 的仓库，自己账户再操作仓库的安全提示，按照提示执行命令添加白名单就行了。


