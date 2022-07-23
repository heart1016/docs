# 基本操作
> 命令总结

 | 命令                       | 说明                                |
 | -------------------------- | ----------------------------------- |
 | [git init](#初始化-init)   | 初始化仓库                          |
 | [git clone](#克隆-clone)   | 拷贝一份远程仓库 也就是下载一个项目 |
 | [git status](#状态-status) | 查看仓库当前的状态 显示有变更的文件 |
 | [git add](#添加-add)       | 添加文件到暂存区                    |
 | [git commit](#提交-commit) | 提交暂存区到本地仓库                |
 | [git push](#推送-push)     | 推送代码到远端                      |

首先来到 [GitHub](https://github.com/) 网站注册账号 国内无法访问可以用 [Gitee](https://gitee.com/)

这里以 `GitHub` 为例

![123](./img/2022-07-19_234313.png)

![123](./img/2022-07-19_234446.png)

![123](./img/2022-07-19_234827.png)

![123](./img/2022-07-19_235028.png)

经过上面的步骤 就已经创建好了一个仓库
有两种方法推送 一是直接在本地初始化一个仓库 推送到对应的地址上 二是直接克隆已经创建好的仓库地址 进行推送
## 初始化 (init)
git init 命令用于在目录中创建新的 Git 仓库

在目录中执行 git init 就可以创建一个 Git 仓库了
```bash
ζ mkdir demo1
# hack@hack: ~                                                                                                                  (22:41:32)
ζ cd demo1
# hack@hack: ~/demo1                                                                                                            (22:41:39)
ζ ls
# hack@hack: ~/demo1                                                                                                            (22:41:40)
ζ la
总用量 0
# hack@hack: ~/demo1                                                                                                            (22:41:42)
ζ git init
提示：使用 'master' 作为初始分支的名称。这个默认分支名称可能会更改。要在新仓库中
提示：配置使用初始分支名，并消除这条警告，请执行：
提示：
提示：  git config --global init.defaultBranch <名称>
提示：
提示：除了 'master' 之外，通常选定的名字有 'main'、'trunk' 和 'development'。
提示：可以通过以下命令重命名刚创建的分支：
提示：
提示：  git branch -m <name>
已初始化空的 Git 仓库于 /home/hack/demo1/.git/
# hack@hack: ~/demo1 <master ✔ >                                                                                                (22:41:45)
ζ la
总用量 4.0K
drwxr-xr-x 7 hack hack 4.0K  7月 23 22:41 .git
# hack@hack: ~/demo1 <master ✔ >                                                                                                (22:41:49)
ζ
```
此时看到已经创建一个.git 文件夹就表示 已经初始化成功了
之后把云端的仓库地址关联上本地的这个仓库 就可以了
```bash
git remote add origin https://github.com/heart1016/demo.git
```
!> 如果已经克隆了 就不用进行上面的操作了 如果没有克隆可以进行上述操作
## 克隆 (clone)
git clone 拷贝一个 Git 仓库到本地 让自己能够查看该项目 或者进行修改
```bash
git clone [url] # url 是你要克隆的仓库地址
```
首先把仓库地址复制下来 `https://github.com/heart1016/demo.git`
```bash
 ________________________________________________
/ グランドエスケープ:                      \
\ “めまぐるしい景色の中,君だけが止まって見えた.” /
 ------------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
# hack@hack: ~                                                                                                                  (19:01:42)
ζ git clone https://github.com/heart1016/demo.git
正克隆到 'demo'...
warning: 您似乎克隆了一个空仓库。
# hack@hack: ~                                                                                                                  (19:02:02)
ζ ls
demo  docs  soul1.json  soul.sql  soul.sql:Zone.Identifier
# hack@hack: ~                                                                                                                  (19:02:08)
ζ
```

在本地看到了demo 文件夹 就说明已经 **克隆(clone)** 下来了

进入demo上传一个文件
```bash
# hack@hack: ~                                                                                                                  (19:02:08)
ζ cd demo
# hack@hack: ~/demo <main ✔ >                                                                                                   (19:06:24)
ζ ls
# hack@hack: ~/demo <main ✔ >                                                                                                   (19:06:26)
ζ la
总用量 4.0K
drwxr-xr-x 7 hack hack 4.0K  7月 23 19:02 .git
# hack@hack: ~/demo <main ✔ >                                                                                                   (19:06:28)
ζ
```
当用ls看到一个文件没有 但是有la 看到了一个文件夹 `.git` 看到前面的点了吗 这个文件夹是个隐藏的 是git的配置文件 这个放在后面讲

创建一个README.md 文件 可以用echo  touch vi  等等
```bash
# hack@hack: ~/demo <main ✔ >                                                                                                   (19:10:38)
ζ echo "# 这是我的第一个git 仓库" > README.md
# hack@hack: ~/demo <main ✘ [?]>                                                                                                (19:11:33)
ζ ls
README.md
# hack@hack: ~/demo <main ✘ [?]>                                                                                                (19:11:35)
ζ cat README.md
# 这是我的第一个git 仓库
# hack@hack: ~/demo <main ✘ [?]>                                                                                                (19:11:41)
ζ
```
此时文件有了 可以用 `git status`   查看下当前仓库的状态

## 状态 (status)
git status 命令用于查看在你上次提交之后是否有对文件进行再次修改
通常我们使用 -s 参数来获得简短的输出结果
```bash
# hack@hack: ~/demo <main ✘ [*]>                                                                                                (22:25:48)
ζ git status -s                                                                                                                  [fa85957]
 M README.md
# hack@hack: ~/demo <main ✘ [*]>                                                                                                (22:25:51)
ζ
```
```bash
ζ git status
位于分支 main

尚无提交

未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）
        README.md

提交为空，但是存在尚未跟踪的文件（使用 "git add" 建立跟踪）
# hack@hack: ~/demo <main ✘ [?]>                                                                                                (19:18:54)
ζ
```

可以看到文件是红色的 结合git 给的提示 证明现在这个文件还没有在版本控制里 接下来 就把这个文件加入到版本控制

## 添加 (add)
git add 命令可将该文件添加到暂存区

```bash
git add [file1] [file2] [dir] ... # 添加一个或多个文件 或文件夹到暂存区
git add . # 添加当前目录下的所有文件到暂存区
```
```bash
# hack@hack: ~/demo <main ✘ [?]>                                                                                                (19:21:35)
ζ git add README.md
# hack@hack: ~/demo <main ✘ [+]>                                                                                                (19:21:40)
ζ git status
位于分支 main

尚无提交

要提交的变更：
  （使用 "git rm --cached <文件>..." 以取消暂存）
        新文件：   README.md </p>

# hack@hack: ~/demo <main ✘ [+]>                                                                                                (19:21:44)
ζ
```
此时文件变成了绿色 表示文件已经提交到暂存区了

## 提交 (commit)
git commit 命令将暂存区内容添加到本地仓库中

```bash
git commit -m [message] # -m 此次提交的备注信息
```
```bash
# hack@hack: ~/demo <main ✘ [+]>                                                                                                (22:03:56)
ζ git commit -m "first"
[main （根提交） fa85957] first
 Committer: hack <hack@hack.localdomain>
您的姓名和邮件地址基于登录名和主机名进行了自动设置。请检查它们正确
与否。您可以对其进行设置以免再出现本提示信息：

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

设置完毕后，您可以用下面的命令来修正本次提交所使用的用户身份：

    git commit --amend --reset-author

 1 file changed, 1 insertion(+)
 create mode 100644 README.md
# hack@hack: ~/demo <main ✔ >                                                                                                   (22:04:22)
ζ
```

此时已经提交成功`-m` 是提交的备注信息 可以用`git status` 查看下文件的状态

```bash
# hack@hack: ~/demo <main ✔ >                                                                                                   (22:05:26)
ζ git status .                                                                                                                   [fa85957]
位于分支 main
您的分支基于 'origin/main'，但此上游分支已经不存在。
  （使用 "git branch --unset-upstream" 来修复）

无文件要提交，干净的工作区
# hack@hack: ~/demo <main ✔ >                                                                                                   (22:05:30)
ζ
```



## 推送 (push)
git push 命令用于从将本地的分支版本上传到远程并合并
```bash
git push <远程主机名> <本地分支名>:<远程分支名> # 默认git push 是推送到默认分支上
git push <远程主机名> <本地分支名> # 如果本地分支名与远程分支名相同，则可以省略冒号：
```
此时的文件只是提交到了本地成功了  还并没有提交到云端

```bash
ζ git push                                                                                                                       [fa85957]
枚举对象中: 3, 完成.
对象计数中: 100% (3/3), 完成.
写入对象中: 100% (3/3), 240 字节 | 240.00 KiB/s, 完成.
总共 3（差异 0），复用 0（差异 0），包复用 0
To https://github.com/heart1016/demo.git
 * [new branch]      main -> main
# hack@hack: ~/demo <main ✔ >                                                                                                   (22:10:45)
ζ
```

这样就推送到云端 可以去网页上查看一下

![123](./img/2022-07-23_221315.png)

## 日志 (log)
Git 提交历史一般常用两个命令
```bash
git log # 查看历史提交记录
git blame <file> # 以列表形式查看指定文件的历史修改记录
```
在使用 Git 提交了若干更新之后 又或者克隆了某个项目 想回顾下提交历史 我们可以使用 git log 命令查看
```bash
git log
commit fa85957ecda67e9feb304b417add361df16a1ef8 (HEAD -> main)
Author: hack <hack@hack.localdomain>
Date:   Sat Jul 23 22:04:22 2022 +0800

    first

git blame README.md

^fa85957 (hack              2022-07-23 22:04:22 +0800 1) # 这是我的第一个git 仓库
00000000 (Not Committed Yet 2022-07-23 23:06:33 +0800 2) 12
```