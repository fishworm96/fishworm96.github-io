---
title: hexo
date: 2021-03-09 22:33:21
categories: hexo笔记
tags: hexo
---

# HEXO

## 基本操作

```
hexo s	开启本地博客地址：http://localhost:4000
hexo n "文章名"
vim "文章名称.md"	进入文章进行修改	wq	保存并退出
hexo clean	清理
hexo g	生成(在本地生成新建的文章)
hexo d	推送
```

<!--more-->

## Hexo 添加分类及标签

> 生成的新文件夹都在source下也就是和放文章的文件夹一块 以下所有命令都是在博客文件目录下执行

#### 1. 创建“分类”选项

生成“分类”页并添加tpye属性,进入博客目录。执行下方命令

```
$ hexo new page categories
```

categories文件夹下会有index.md这个文件，打开后默认内容是这样的：

```
---
title: categories
date: 2019-04-22 14:47:40
---
```

添加type: "categories"到内容中，添加后是这样的：

```
---
title: 分类
date: 2019-04-24 15:30:30
type: categories
---
```

保存并关闭文件。

给文章添加“categories”属性

打开需要添加分类的文章，为其添加categories属性。下方的categories:Hexo表示这篇文章添加到到“Hexo”这个分类。注意：一篇文章只会添加到一个分类中，如果是多个默认放到第一个分类中。

```
---
title: Hexo 添加分类及标签
date: 2017-05-26 12:12:57
categories: Hexo
---
```

至此，成功给文章添加分类，点击首页的“分类”可以看到该分类下的所有文章。当然，只有添加了categories: xxx的文章才会被收录到首页的“分类”中。

#### 2. 创建“标签”选项

生成“标签”页并添加tpye属性

```
$ hexo new page tags
```

在tags文件夹下，找到index.md这个文件，打开后默认内容是这样的：

```
---
title: 标签
date: 2019-04-22 14:22:08
---
```

添加type: "tags"到内容中，添加后是这样的：

```
---
title: 标签
date: 2019-04-24 15:40:24
type: tags
---
```

保存并关闭文件。

给文章添加“tags”属性,打开需要添加标签的文章，为其添加tags属性。

```
---
title: Hexo 添加分类及标签
date: 2019-04-24 15:40:24
categories:  Hexo
tags:  博客
---
```

# 添加评论功能

## 一、添加留言本 page

进入到博客的根目录，运行命令：

```cpp
hexo new page guestbook
```

## 二、留言本页面中添加多说访客代码

上一步中使用 hexo 命令新建了一个 page，进入到博客的source目录，里面会多了一个gusetbook文件夹，里面有一个index.md文件，打开该文件编辑：



```jsx
<div class="ds-recent-visitors" data-num-items="28" data-avatar-size="42" id="ds-recent-visitors"></div>
```

这段代码加到index.md底部就行。

## 三、菜单设置中添加留言本

找到Next主题设置的_config.yml文件里面的menu项



```bash
menu:
  home: /
  #about: /about
  archives: /archives
  tags: /tags
  categories: /categories
  guestbook: /guestbook
```

## 四、添加多语言文件的值

因为这里使用的是中文，找到languages文件夹里面的zh-CH.yml文件，menu子项中添加留言：

```undefined
menu:
  home: 首页
  archives: 归档
  categories: 分类
  tags: 标签
  about: 关于
  search: 搜索
  commonweal: 公益404
  guestbook: 留言
```

## 五、设置一个评论系统

我用的是Next 主题，本身就已经集成了valine，直接配置即可
 下面网上搜来的其余系统,请自行搜索教程

- ~~多说~~
- ~~网易云跟帖~~
- 畅言
- 来必力（LiveRe）
- Disqus
- Hypercomments
- valine

## 开启Valine

# 注册Leancloud

我们的评论系统其实是放在Leancloud上的，因此首先需要去注册一个账号 [点我注册](https://links.jianshu.com/go?to=https%3A%2F%2Fleancloud.cn%2F)

1、 注册完以后需要创建一个应用，名字可以随便起，然后 进入应用->设置->应用key ,获取你的 `appid` 和 `appkey`
 2、 打开主题配置文件 搜索 valine，填入appid 和 appkey

![img](https:////upload-images.jianshu.io/upload_images/8921320-9201b23ae78846cf.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

配置appid 和 appkey.png

 2、在Leancloud -> 设置 -> 安全中心 -> Web 安全域名 把你的域名加进去



## 新增Hexo博客文章置顶功能

**修改Hexo文件夹下的node_modules/hexo-generator-index/lib/generator.js**

需要添加的代码：

```
posts.data = posts.data.sort(function(a, b) {
      if(a.top && b.top) {
          if(a.top == b.top) return b.date - a.date;
          else return b.top - a.top;
      }
      else if(a.top && !b.top) {
          return -1;
      }
      else if(!a.top && b.top) {
          return 1;
      }
      else return b.date - a.date;
  });
```

如何使用：在需要置顶的文章添加top属性即可，排序从小到大