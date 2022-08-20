# 标签

标签是Git的对象 包含了对commit对象的引用 另外每个标签都会有一个标签相同名称的ref文件存储在.git/refs/tags/目录下 文件内容为Git对象的SHA值 此处有两种情况
- 若为轻量级标签 Git不会真正建立tag对象 而由tag的ref文件直接引用commit的SHA值
- 若为含有附注的标签 则Git会建立tag对象 tag对象包含commit的引用 而tag的ref文件则包含tag对象的引用

## 创建标签

```bash
git tag tag_name [commit] # 创建一个轻量标签 默认不指定commit 为最后最近一次
git tag -a tag_name -m "message" [commit] # 创建含有附注标签
```

## 查看标签
```bash
git tag # 查看所有标签
git tag -l "tag_name*" # 查找指定标签
git show tag_name # 查看标签详细
```
## 推送标签

```bash
git push origin tag_name # 推送指定标签
git push origin --tags # 推送所有标签
```

## 删除标签

```bash
git tag -d tag_name # 删除本地标签
git push origin :refs/tags/tag_name # 删除远程标签
```