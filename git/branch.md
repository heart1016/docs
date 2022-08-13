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

上面已经讲过了 但是在实际开发中 常常会有很多修改 在切换分支时因为没有修改完成或是其它原因无法提交 这个时候切换分支是不会成功的

## 修改分支

## 删除分支

## 推送分支

## 合并分支

