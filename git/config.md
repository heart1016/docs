# 配置

在每个git 项目中的根目录都有一个隐藏的文件夹 .git 这个是必须有切不能删除的 与这个项目有关的一些配置都存储在里面 路径就是.git/config

## 文件位置

配置文件可以被存储在三个不同的位置

- /etc/gitconfig 包含了适用于系统所有用户和所有库的值 如果你传递参数选项--system 给 git config 它将明确的读和写这个文件

- ~/.gitconfig 具体到你的用户 你可以通过传递--global 选项使Git 读或写这个特定的文件

- 位于git目录的config文件 (也就是 .git/config) 无论你当前在用的库是什么 特定指向该单一的库 每个级别重写前一个级别的值 因此 在.git/config中的值覆盖了在/etc/gitconfig中的同一个值

## 用户名和邮箱

在一个项目刚提交的时候 往往会出现下面这样的提示

```bash
您的姓名和邮件地址基于登录名和主机名进行了自动设置。请检查它们正确
与否。您可以对其进行设置以免再出现本提示信息：

    git config --global user.name "Your Name"
    git config --global user.email you@example.com

设置完毕后，您可以用下面的命令来修正本次提交所使用的用户身份：

    git commit --amend --reset-author
```
我在新电脑是选择了中文的所以提示也是中文的 大概率你的会是英文的提示 但意思是一样的 需要我们设置一个邮箱和姓名
如果你是刚开始学习Git 那么可能还不会疑问 我学了好久之后回头看的时候才发现了疑问

> 1、为什么要配置用户名和邮箱？

因为Git是分布式版本控制系统 所以 每个机器都必须自报家门 你的名字和邮箱地址 (名字和邮箱都不会进行验证) 这样远程仓库才知道哪次提交是由谁完成的

你也许会担心 如果有人故意冒充别人怎么办 这个不必担心 首先我们相信大家都是善良无知的群众 其次 真的有冒充的也是有办法可查的

> 2、配置的用户名和邮箱对push代码到远程仓库有什么影响？

首先 配置的用户名和邮箱对push代码到远程仓库时的身份验证没有作用 即不用他们进行身份验证 他们仅仅会出现在远程仓库的commits里

其次 按正常操作来说 你应该配置你的真实用户名和邮箱l这样一来在远程仓库的commits里可以看到哪个操作是你所为

最后 这个用户名和邮箱是可以随便配置的(不提倡) 如果你配置的邮箱是github里真实存在的邮箱 则commits里显示的是这个邮箱对应的账号 如果配置的邮箱是一个在github里不存在的邮箱 则commits里显示的是你配置的用户名

```bash
# hack@hack: ~/demo <main ✔ >                                                                                                                             (20:33:22)
ζ git config --global user.name "hack"                                                                                                                     [a35f1e1]
# hack@hack: ~/demo <main ✔ >                                                                                                                             (20:39:11)
ζ git config --global user.email "heart10162115@foxmail.com"                                                                                               [a35f1e1]
# hack@hack: ~/demo <main ✔ >                                                                                                                             (20:39:29)
ζcat ~/.gitconfig
[user]
        name = hack
        email = heart10162115@foxmail.com
```
这是执行命令之后的配置文件 也可以直接添加到配置文件 效果相同

## 记住密码

```bash
git config --global credential.helper store

# 执行之后配置文件会多出这个配置

[credential]
        helper = store

# 或是直接添加也可以
```

## 编辑器

如果你不喜欢默认的 可以用这个命令替换成vi 或 emacs
```bash
git config --global core.editor vi

#  配置文件长这样
[core]
        editor = vi
```
