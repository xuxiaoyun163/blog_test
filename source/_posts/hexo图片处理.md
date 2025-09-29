---
title: hexo图片处理
date: 2025-09-29 20:39:34
tags:
    - hexo
---

# 图片

我们在配置文件中打开组织化的方式管理资源文件

```
_config.yml
post_asset_folder: true
```

这个时候我们创建一个文章时，会自动给我创建对应的文件夹

![](2025-09-29-20-42-40-image.png)

但是这个时候我们插入图片必须使用规定的assets语法进行图片的导入

```
{% asset_img example.jpg This is an example image %}
{% asset_img "spaced asset.jpg" "spaced title" %}
```

但是这样的引入方法会很麻烦，而且图片在本地编辑的时候时不可见的，并且插入图片比较费事

hexo也给我们提供了更方便的方法我们可以使用markdown嵌入图片

[hexo-renderer-marked](https://github.com/hexojs/hexo-renderer-marked) 3.1.0 引入了一个新的选项，其允许你无需使用 `asset_img` 标签插件就可以在 markdown 中嵌入图片

如需启用：

```
_config.yml
post_asset_folder: true
marked:
  prependRoot: true
  postAsset: true
```

启用后，资源图片将会被自动解析为其对应文章的路径。 例如： `image.jpg` 位置为 `/2020/01/02/foo/image.jpg` ，这表示它是 `/2020/01/02/foo/` 文章的一张资源图片， `![](image.jpg)` 将会被解析为 `<img src="/2020/01/02/foo/image.jpg">`

开启这个配置之后我们就可以将图片放在文章同名的文件夹下面并且可以使用`!()[image.jpg]`去导入图片

但是这样的话也还是有一个弊端，就是本地在编写博客的时候，我们插入的图片就不可见，只有部署之后才可以在网站上看见，不利于本地编写，并且如果以后要做博客的迁移的时候我们的博客中的所有图片的路径都是错误的，修改起来很麻烦

那我们有没有一种方法，既可以让图片在本地显示，也可以在网站上显示呢？

我们需要安装一个依赖

```
npm install https://github.com/xcodebuild/hexo-asset-image.git
```

这个依赖的作用就是我们在导入图片资源的时候可以导入完整的路径

例如我们的博客名称是 demo01.md 存放资源的文件夹叫demo01, 如果我们有一张图片叫abc.jpg

我们可以直接在demo01.md中引用`demo01/abc.jpg` 这样的话我们就可以完美将图片在本地和网站中展示了
