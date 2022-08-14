# 分支管理

在真实的项目中 所有的开发工作总是同时进行的 并且其每一个主题都处于一个特定的上下文环境下

- 当你为了完成一个新的用户需求 你对这个页面准备了2套设计方案(主题 1 主题 2)
- 同时你也想尝试的去修复一些错误(主题 3)
- 另一方面 你还想升级一下你的 FAQ 页面(主题 4) 或者
- 团队中的另外一些开发人员正在为在线购物车添加一些新的功能(主题 5)
- 还有其他一些同事正在尝试开发一种新的用户登录功能(主题 6)

## 创建分支

```bash
git branch 分支名 # 创建一个分支 但不会切换过去
git checkout -b 分支名 # 创建一个分支并切换过去
```

```bash
# hack@hack: ~/demo <main ✘ [*?]>                                                                                                                         (17:25:58)
ζ git branch hello                                                                                                                                         [fa85957]
# hack@hack: ~/demo <main ✘ [*?]>                                                                                                                         (17:26:05)
ζ git branch
  hello
* main

# 可以看到branch 只是创建并没有切换到新的分支上

# hack@hack: ~/demo <main ✘ [*?]>                                                                                                                         (17:26:05)
ζ git checkout -b test                                                                                                                                     [fa85957]
切换到一个新分支 'test'
# hack@hack: ~/demo <test ✘ [*?]>

# checkout -b 创建了新的分支 并切换过来了
```

## 查看分支
```bash
git branch # 查看本地分支
git branch -r # 查看远程分支
git branch -a # 查看所有本地与远程分支
```

```bash
# hack@hack: ~/docs <main ✘ [*]>                                                                                                                          (17:23:36)
ζ git status .                                                                                                                                             [6be0994]
位于分支 main
您的分支与上游分支 'origin/main' 一致。

尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
        修改：     git/basic_operations.md
        修改：     git/branch.md

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）

# 第一行 显示了此时位于哪个分支上
# hack@hack: ~/demo <test ✘ [*?]>                                                                                                                         (17:40:20)
ζ git branch                                                                                                                                               [fa85957]
ζ
 hello
  main
* test

# 查看本地分支
# 星号是表示此时所在的分支

# hack@hack: ~/demo <test ✘ [*?]>                                                                                                                         (17:40:20)
ζ git branch -r                                                                                                                                              [fa85957]
 origin/main

 # 查看远程分支

 # hack@hack: ~/demo <test ✘ [*?]>                                                                                                                         (17:43:04)
ζ git branch -a
 hello
  main
* test
  remotes/origin/main
# 查看所有分支
```

## 切换分支

上面已经讲过了 但是在实际开发中 常常会有很多修改 在切换分支时因为没有修改完成或是其它原因无法提交 这个时候切换分支是不会成功的 **仅限于修改相同的文件有覆盖操作的这种 如两个分支各自修改各自的无交集文件不会提示冲突**

```bash
# 首先创建一个分支并推送到云端
# hack@hack: ~/demo <main ✔ >                                                                                                                             (20:4[10/47]
ζ git checkout -b test                                                                                                                                     [9391489]
切换到一个新分支 'test'
# hack@hack: ~/demo <test ✔ >                                                                                                                             (20:43:56)
ζ git push                                                                                                                                                 [9391489]
fatal: 当前分支 test 没有对应的上游分支。
为推送当前分支并建立与远程上游的跟踪，使用

    git push --set-upstream origin test

# 此时提示要用这个命令设置跟踪 设置好之后  pull 与 push  就都是针对当前 分支了  如果 不设置 那么也可以用 `git push origin test` 建议设置跟踪
# hack@hack: ~/demo <test ✔ >                                                                                                                             (20:44:07)
ζ git push --set-upstream origin test                                                                                                                      [9391489]
总共 0（差异 0），复用 0（差异 0），包复用 0
remote:
remote: Create a pull request for 'test' on GitHub by visiting:
remote:      https://github.com/heart1016/demo/pull/new/test
remote:
To https://github.com/heart1016/demo.git
 * [new branch]      test -> test
分支 'test' 设置为跟踪来自 'origin' 的远程分支 'test'。
# hack@hack: ~/demo <test ✔ >                                                                                                                             (20:55:01)
ζ

# 此时这个文件长这样
# hack@hack: ~/demo <test ✔ >                                                                                                                             (20:59:53)
ζ cat README.md                                                                                                                                            [9391489]
# 这是我的第一个git 仓库
123
456
789
000
999
888
# 修改一下 重新上传
ζ cat README.md                                                                                                                                            [be66ae0]
# 这是我的第一个git 仓库

# 这是修改后的样子 此时再修改
ζ cat README.md                                                                                                                                            [be66ae0]
# 这是我的第一个git 仓库
123
# hack@hack: ~/demo <test ✘ [*]>                                                                                                                          (21:03:53)
ζ git checkout main                                                                                                                                        [be66ae0]
error: 您对下列文件的本地修改将被检出操作覆盖：
        README.md
请在切换分支前提交或贮藏您的修改。
正在终止
# 这个时候就提示冲突了 一是恢复这个文件到原始的样子 checkout  二是储存起来 stash
# hack@hack: ~/demo <test ✘ [*]>                                                                                                                          (21:05:39)
ζ git stash save 'test'                                                                                                                                    [be66ae0]
保存工作目录和索引状态 On test: test
# hack@hack: ~/demo <test ✔ >                                                                                                                             (21:05:45)
ζ git checkout main                                                                                                                                        [be66ae0]
切换到分支 'main'
您的分支与上游分支 'origin/main' 一致。
ζ git checkout test                                                                                                                                        [9391489]
切换到分支 'test'
您的分支与上游分支 'origin/test' 一致。

# hack@hack: ~/demo <test ✔ >                                                                                                                             (21:06:23)
ζ git stash pop
位于分支 test
您的分支与上游分支 'origin/test' 一致。

尚未暂存以备提交的变更：
  （使用 "git add <文件>..." 更新要提交的内容）
  （使用 "git restore <文件>..." 丢弃工作区的改动）
        修改：     README.md

修改尚未加入提交（使用 "git add" 和/或 "git commit -a"）
丢弃了 refs/stash@{0}（bb9aa17e05c18f4239e1b195b3ebc78c9dc20cb3）
# hack@hack: ~/demo <test ✘ [*]>                                                                                                                          (21:06:26)
ζ
```

## 修改分支
```bash
git branch -m old-branch-name new-branch-name # 修改分支的名称


# hack@hack: ~/demo <test ✘ [*]>                                                                                                                          (21:17:00)
ζ git branch -m test test22                                                                                                                                [be66ae0]
# hack@hack: ~/demo <test22 ✘ [*]>                                                                                                                        (21:17:10)
ζ
```


## 删除分支

```bash
git branch -d branch-name # 删除分支
git branch -D branch-name # 强制删除分支
```
```bash
# hack@hack: ~/demo <main ✔ >                                                                                                                             (21:21:39)
ζ git branch -d test22                                                                                                                                     [9391489]
warning: 将要删除的分支 'test22' 已经被合并到
         'refs/remotes/origin/test'，但未合并到 HEAD。
已删除分支 test22（曾为 be66ae0）。
# 删除本地分支
# hack@hack: ~/demo <main ✔ >                                                                                                                             (21:22:19)
ζ git push origin -d test                                                                                                                                  [9391489]
To https://github.com/heart1016/demo.git
 - [deleted]         test
# 删除远程分支
```

## 推送分支
刚创建的分支都是本地分支 需要push 云端才可以看见 称为远程分支
```bash
ζ git checkout -b test                                                                                                                                     [9391489]
切换到一个新分支 'test'
# hack@hack: ~/demo <test ✔ >                                                                                                                             (21:28:04)
ζ git push --set-upstream origin test                                                                                                                      [9391489]
总共 0（差异 0），复用 0（差异 0），包复用 0
remote:
remote: Create a pull request for 'test' on GitHub by visiting:
remote:      https://github.com/heart1016/demo/pull/new/test
remote:
To https://github.com/heart1016/demo.git
 * [new branch]      test -> test
分支 'test' 设置为跟踪来自 'origin' 的远程分支 'test'。
# hack@hack: ~/demo <test ✔ >                                                                                                                             (21:28:15)
ζ
# 也可以用git push origin branch-name
```

## 合并分支

在实际开发中 经常会根据业务的需求创建一个独立的分支进行开发 开发完成后合并到主分支中 或是修复问题 修复完毕 合并到主分支发布

```bash
# hack@hack: ~/demo <main ✔ >                                                                                                                             (21:32:41)
ζ cat README.md                                                                                                                                            [9391489]
# 这是我的第一个git 仓库
123
456
789
000
999
888
# 这是main 分支上的

# hack@hack: ~/demo <test ✔ >                                                                                                                             (21:37:02)
ζ cat README.md                                                                                                                                            [f9cb6a5]
# 这是我的第一个git 仓库
000
# 这是test 分支
# 比如说 test 分支修复了一个bug 修复好了 需要合并到main分支上  首先要切换到main分支上 执行merge操作

# hack@hack: ~/demo <main ✔ >                                                                                                                             (21:38:49)
ζ git merge test                                                                                                                                           [9391489]
更新 9391489..f9cb6a5
Fast-forward
 README.md | 5 -----
 1 file changed, 5 deletions(-)
# 这样表示 自动合并成功了 并无冲突 之后 直接push 就可以了

README.md
# hack@hack: ~/demo <test ✔ >                                                                                                                             (21:55:58)
ζ cat README.md                                                                                                                                            [f6af5c6]
# 这是我的第一个git 仓库
120
450
780
000
999
888


# hack@hack: ~/demo <main ✘ [*]>                                                                                                                          (21:59:08)
ζ cat README.md                                                                                                                                            [9391489]
# 这是我的第一个git 仓库
000

# hack@hack: ~/demo <main ✘ [*]>                                                                                                                          (21:59:01)
ζ git merge test                                                                                                                                           [9391489]
更新 9391489..1bb5cc0
error: 您对下列文件的本地修改将被合并操作覆盖：
        README.md
请在合并前提交或贮藏您的修改。
正在终止
# 这种是合并过的分支修改了相同的文件 但是还没有提交 它并不知道保留哪个 所有没有自动合并


# hack@hack: ~/demo <main ✔ >                                                                                                                             (22:01:54)
ζ git merge test                                                                                                                                           [1a0d659]
自动合并 README.md
冲突（内容）：合并冲突于 README.md
自动合并失败，修正冲突然后提交修正的结果。

#  这种就是 两个分支的内容部分不一样了根据行号
# hack@hack: ~/demo <main ✘ [=]>                                                                                                                          (22:01:59)
ζ cat README.md                                                                                                                                            [1a0d659]
# 这是我的第一个git 仓库
<<<<<<< HEAD
=======
120
450
121212121212
>>>>>>> test
000
# 此时HEAD 到 === 表示当前分支 === 到test 表示test 分支的 但是都出现在相同的行号 这时就需要人为解决冲突了 并删掉对应的标记就可以了
# hack@hack: ~/demo <main ✘ [=]>                                                                                                                          (22:05:40)
ζ cat README.md                                                                                                                                            [1a0d659]
# 这是我的第一个git 仓库
120
450
000
```
