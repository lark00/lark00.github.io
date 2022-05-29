---
layout: hexo指令
title: HEXO指令
date: 2021-12-04 20:57:18
---

### 1.创建一个[md文件](https://www.zhihu.com/search?q=md文件&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A156915260})

md文件也就是`Markdown`文件，通过以下命令来创建：

```text
$ hexo new <title>
$ hexo new "我的第一篇文章"
```

<!--more-->

### 2.布局（layout）

- 创建md文件时，我们可以指定布局

```
$ hexo new [layout] <title>$ hexo new page "我的页面"
```

- 布局有三种：`post`（文章）、`draft`（草稿）、`page`（页面）

在新建文件时，Hexo 会根据 `scaffolds` 文件夹内相对应的文件（可以理解为模板）来建立md文件：

![img](https://pic2.zhimg.com/80/v2-2683cfb7e862381166e609ef37210a99_720w.png)



- 如果没有指定布局类型，则为默认布局`post`，可以在站点配置文件修改 `default_layout` 参数来修改默认布局。
- 当我们创建不同布局的md文件时，它们会存储在不同路径：

![img](https://pic3.zhimg.com/80/v2-81c1aa7b55f1ae6767b3563127a22156_720w.jpg)

> 对于独立页面来说，Hexo 会创建一个以标题为名字的目录，并在目录中放置一个 `index.md` 文件，页面布局顾名思义就是用来DIY我们博客页面的。

### 3.草稿（draft）

`draft`这种布局在建立时会被保存到 `source/_drafts` 文件夹中，但不会显示在页面上，如果我们不想某一篇文章显示在页面上，那么就可以把它移动到`_drafts`文件夹中。

- 我们可在启动服务器时加上 `--draft` 参数来查看草稿。

```
$ hexo server --draft
```

- 还可以在站点配置文件中把 `render_drafts` 参数设为 `true` 来预览草稿。
- 我们可以通过 `publish` 命令将草稿发布文章或者页面，它将会被移动到指定的文件夹。

```
$ hexo publish [layout] <title>
```

### 4.[Front-matter](https://www.zhihu.com/search?q=Front-matter&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"article"%2C"sourceId"%3A156915260})

当我们创建一个md文件后，打开后会看到一些内容，这些称为`Front-matter`，它是文件最上方以 `---` 分隔的区域，用于指定个别文件的变量，举例来说：

```yaml
---
title: Hello World # 标题就是我们上面创建的时候指定的名字
date: 2013/7/13 20:46:25 # 文件创建的时间
---
```

> 在`Typora`中我们在md文件的首行（必须是第一行）输入`---` ，然后按回车就可以插入`Front-matter`了。

Front-matter预定义参数

```text
  layout  布局  默认为true，如果你不想你的文章被处理，可以设置为false
  title  标题  标题会显示在最上方居中位置     
  date  建立日期    如果不指定则为默认值-文件创建日期，可以自定义。
  update  更新日期  如果不指定则为默认值-文件修改后重新生成静态文件的日期。
  comments  是否开启文章的评论功能 默认值为true
  tags  标签（不适用于页面page布局）
  categoreies  分类（不适用于页面page布局）
  permalink  覆盖文章网址
  keywords  仅用于 meta 标签和 Open Graph 的关键词（不推荐使用）
```

### 为文章添加分类与标签

只有文章（post布局）支持分类和标签，需要在`Front-matter`中设置。分类有层级关系，标签没有。

举个例子：
1）下面文章它的标签是：Hexo、博客
2）分类是： 个人博客 > Hexo博客
3）“Hexo博客” 是 “个人博客” 的子分类

```yaml
categories:
- 个人博客（第一层级）
- Hexo博客（第二层级）
tags:
- Hexo
- 博客
```

### 为文章添加多个分类

1）下面文章属于三个分类：日常 > 生活，日常 > 随想，日记
2）其中生活、随想为日常的子分类，日常和日记为同级分类

```yaml
categories:
- [日常, 生活]
- [日常, 随想]
- [日记]
```

## 基本操作

### 常用命令

- **清除缓存：**`hexo clean`
- **生成静态文件：**`hexo generate`可简写为 `hexo g`
- **启动服务器：**`hexo server`或者 `hexo s` 常用参数：`-p（--port）`重设端口
- **部署：**`hexo deploy`可简写为`hexo d`，用于将网站部署到服务器上。（暂时用不到，目前都是在本地，后面我们将博客托管到`GitHub Pages`或`Gitee Pages`时才会用到此命令）
  常用参数：`-g（--generate）`，`hexo d -g`部署前预先生成静态文件，等同于 `hexo g -d`

**一般发布文章或者修改博客后需要这些操作：**清除缓存>生成静态文件>启动服务器，测试没问题后再部署。

```csharp
// 我们可以写成一条命令
$ hexo clean && hexo g && hexo s
$ hexo d
```

## normal page

我目前还不知道该如何用中文称呼这类页面。我们可以把post和draft统称为blog pages，在这之外的一种就是normal pages， 类似一个网站上的“关于”，“了解我们”之类的页面。

这类page要如何新建呢？

```
hexo new page c
```

和前两种不同，这个命令会在source文件夹内创建出c文件夹，与_posts，_drafts并列。文件夹里面有一个index.md文件。

刷新页面，你会发现c并没有出现在页面内，那它在哪儿呢？

在网址后面加上c/， 即[http://localhost:4000/c/](https://link.jianshu.com?t=http://localhost:4000/c/)，就可以看到了。

正因为c不是一个blog page，所以它也不会出现在blog列表中，而是要通过URL去access。

>[简书](https://www.jianshu.com/p/265b2c653e6f)

> [知乎](https://zhuanlan.zhihu.com/p/156915260)
>
> [Hexo博客的常用配置修改](https://www.jianshu.com/p/0fe7dd8a0e8b?winzoom=1)

