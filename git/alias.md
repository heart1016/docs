# 别名

两种实现方法

一 在配置文件中添加 alias 的配置 配置中把想设置成别名的写在里面
```bash
[alias]
        st = status # 别名=实际名称
```

二 使用alias 命令
```bash
# hack@hack: ~/demo <main ✔ >                                                                                                                             (21:33:02)
ζ alias gst='git status'                                                                                                                                   [ea9f79f]
# hack@hack: ~/demo <main ✔ >                                                                                                                             (21:33:18)
ζ gst                                                                                                                                                      [ea9f79f]
位于分支 main
您的分支与上游分支 'origin/main' 一致。

无文件要提交，干净的工作区
# hack@hack: ~/demo <main ✔ >                                                                                                                             (21:33:21)
# hack@hack: ~/demo <main ✔ >                                                                                                                             (21:34:17)
ζ alias | grep gst                                                                                                                                         [ea9f79f]
gst='git status'
gsta='git stash push'
gstaa='git stash apply'
gstall='git stash --all'
gstc='git stash clear'
gstd='git stash drop'
gstl='git stash list'
gstp='git stash pop'
gsts='git stash show --text'
gstu='gsta --include-untracked'
# hack@hack: ~/demo <main ✔ >
ζ
# alias 别名=实际名称
# unalias gst 删除别名
```