---
title: Hexo + Github 搭建 Blog (MacOS)
date: 2021-05-24 12:31:17
categories: Blog
tags: blog-building
---

---

[toc]

---

# 20210524 

## Why

最近在学产品经理的课，有了呈现作品集的需求，遂在网上寻找教程搭建 Blog，最终选定了[这篇]((https://zhuanlan.zhihu.com/p/35668237))详细的教程，在此记录搭建过程。

## What

### Node.js 安装

去到官网下载[Node.js 安装包](https://nodejs.org/zh-cn/download/)，按提示安装就好啦。

之后打开命令行输入以下指令，若出现版本号则证明安装成功：

```
node -v
```

### Git 安装

[Git 下载页面](https://git-scm.com/downloads)

> 因为很久之前已经安装过 Git，所以详细步骤先按下不表

### Github 注册及仓库新建

#### Github 注册

移步 [Github 官网](https://github.com/) 完成注册。

> 详细过程这里也按下不表，理由同上

#### 仓库搭建

注册完账号后回到自己的页面，然后选择新建仓库：

![](https://raw.githubusercontent.com/Medill-East/IMGStorage/master/img/PicGo-Github-PicBed/20210524114739.png)

这里对项目名字进行更改，其中名字需要有 `github.io` 后缀，`这里的名字一定要和自己的 github name 相同！`，然后记得选中 `Add a README file`：

![](https://raw.githubusercontent.com/Medill-East/IMGStorage/master/img/PicGo-Github-PicBed/20210524114910.png)

然后找到该 repository 之后，点击 `settings`：

![](https://raw.githubusercontent.com/Medill-East/IMGStorage/master/img/PicGo-Github-PicBed/20210524115240.png)

直接往下滑之后会看到 `Github Pages`：

![](https://raw.githubusercontent.com/Medill-East/IMGStorage/master/img/PicGo-Github-PicBed/20210524115314.png)

点进去之后 `Choose a theme` 可以先随机挑选一个主题，之后回到 `GitHub Pages`，可以看到下面的界面：

![](https://raw.githubusercontent.com/Medill-East/IMGStorage/master/img/PicGo-Github-PicBed/20210524115755.png)

点进去之后就能看到自己的网页啦。

![](https://raw.githubusercontent.com/Medill-East/IMGStorage/master/img/PicGo-Github-PicBed/20210524121147.png)

### 安装 Hexo

[教程](https://zhuanlan.zhihu.com/p/35668237)中这里是在本地找了一个位置新建了一个文件夹来存放博客文件，暂时没搞懂和直接放 `github` 上的区别... 

这里我先用 [Github Desktop](https://desktop.github.com/) 把之前新建的仓库下载到本地：

![](https://raw.githubusercontent.com/Medill-East/IMGStorage/master/img/PicGo-Github-PicBed/20210524121018.png)

所以我就先也在 之前新建的仓库文件夹下创建新的 `blog` 文件夹。

用命令行进入到该路径下，输入如下指令安装 Hexo，此处若有报错可无视：

```
sudo npm i hexo-cli -g
```

安装后输入如下指令验证安装结果：

```
hexo -v
```

之后输入如下指令初始化网站：

```
hexo init
```

输入如下指令安装必备组件：

```
npm install
```

以上完成了本地的网站配置，然后是如下几个有用的指令：

- 生成静态网页
```
hexo g
```

- 打开本地服务器

```
hexo s
```

之后在浏览器键入[http://localhost:4000/](http://localhost:4000/)就可以打开查看啦。

![](https://raw.githubusercontent.com/Medill-East/IMGStorage/master/img/PicGo-Github-PicBed/20210524121816.png)

然后按 `ctrl + c` 关闭本地服务器。

### 连接 Github 与本地

打开命令行后输入如下指令，记得将相应用户名和邮箱改成自己的：

```
git config --global user.name "YourGitName"

git config --global user.email "YourEmail"
```

之后生成密钥：

```
ssh-keygen -t rsa -C "haodong.liao@gmail.com"
```

这里会提示你键入保存密钥的地址，只需要不断回车即可：

![](https://raw.githubusercontent.com/Medill-East/IMGStorage/master/img/PicGo-Github-PicBed/20210524122153.png)

打开自己的 [github](https://github.com/)，点击头像之后点击 `settings`，然后选择 `SSH and GPG keys`，新建一个 SSH，名字我起名为 `blog`，然后在命令行中输入以下指令：

```
cat ~/.ssh/id_rsa.pub
```

将输出的内容保存到密钥的内容框中，点击保存。

之后在命令行中键入如下内容，若出现用户名则成功：

```
ssh -T git@github.com
```

![](https://raw.githubusercontent.com/Medill-East/IMGStorage/master/img/PicGo-Github-PicBed/20210524122557.png)

打开博客根目录下的 `_config.yml` 文件，即博客的配置文件，修改以下配置为你自己的配置：

```
deploy:
  type: git
  repository: git@github.com:Medill-East/haodong.github.io.git
  branch: master
```

注意 `repository` 的地址可以从仓库的这里获取：

![](https://raw.githubusercontent.com/Medill-East/IMGStorage/master/img/PicGo-Github-PicBed/20210524122756.png)

### 写文章 发布文章

在博客根目录下输入以下指令安装扩展：

```
npm i hexo-deployer-git
```

输入以下指令以新建文章：

```
hexo new post "my first post"
```

然后在路径 `.\blog\source\_posts` 目录下就可以看到多出了 `my-first-post.md` 文件，这就是文章文件啦。

对 md 文件进行相应编辑后，在根目录下键入以下指令以生成静态网页和进行本地预览：

- 生成静态网页
```
hexo g
```

- 打开本地服务器

```
hexo s
```

- 上传到 github

```
hexo d
```


> 注意需要确保 `Github Pages` `settings` 下的 `Source` 下的 `Branch` 为 `master`

> 然后如果本地做过一些改动的话需要同步到 github 上

---

# 20210526 解决 CSS 样式不加载的问题

按照如上步骤配置之后出现了一个问题：在本地预览能够看到的效果部署到网页之后没了 CSS 的效果，所以这里先对这个问题进行一下解决。

尝试了多篇帖子的办法，最终以如下途径成功加载上了 CSS：

1. 把仓库名改为了 
`your github name.github.io` 
比如我的 github name 为 `Medill-East`
那么仓库名就需要为 `medill-east.github.io`

2. 更改根目录下的 _config.yml 配置文件的开头部分 `URL` 和 `root` 配置：

```
# URL
url: https://medill-east.github.io/ # 这里记得改成自己的 url 哦
root: /
```

感谢这篇帖子：[生成路径的问题，导致css，js无法加载 #1121](https://github.com/hexojs/hexo/issues/1121)

---

# 20210527 更换主题

这里和 [超详细Hexo+Github博客搭建小白教程](https://zhuanlan.zhihu.com/p/35668237) 中一样，采用的是 [Hexo博客主题之hexo-theme-matery的介绍](http://blinkfox.com/2018/09/28/qian-duan/hexo-bo-ke-zhu-ti-zhi-hexo-theme-matery-de-jie-shao/) 该主题。

以下为过程记录。

## 下载

进入根目录的 `themes` 文件夹下，用命令行下载：

```
git clone https://github.com/blinkfox/hexo-theme-matery.git
```


## 配置

### 切换主题

修改根目录下 `_config.yml` 的 `theme` 的值：

```
theme: hexo-theme-matery
```

- 建议修改
 -  两个 `per_page` 的分页条数设为 `6` 的倍数，以优化显示
 -  若是中文用户可以修改 `language` 的值为 `zh-CN`

### 新建分类 categories 页

`categories` 用于展示所有分类， 若是 `source` 目录下还没有 `categories/index.md` 文件，就需要新建一个，回到博客根目录(`blog`文件夹)之后运行以下代码：

```
hexo new page "categories"
```

编辑刚新建的页面文件 `/source/categories/index.md`，至少需要以下内容：

```
---
title: categories
date: 2021-05-27 11:44:43
type: "categories"
layout: "categories"
---
```

### 新建标签 tags 页

`tags`页用于展示所有标签，若是 `source` 目录下还没有 `tags/index.md` 文件，就需要新建一个，回到博客根目录(`blog`文件夹)之后运行以下代码：

```
hexo new page "tags"
```

编辑刚新建的页面文件 `/source/tags/index.md`，至少需要以下内容：

```
---
title: tags
date: 2021-05-27 11:44:43
type: "tags"
layout: "tags"
---
```

### 新建关于我 about 页

`about` 页用于展示关于我和我的博客的信息，若是 `source` 目录下还没有 `about/index.md` 文件，就需要新建一个，回到博客根目录(`blog`文件夹)之后运行以下代码：

```
hexo new page "about"
```

编辑刚新建的页面文件 `/source/about/index.md`，至少需要以下内容：

```
---
title: about
date: 2021-05-27 11:49:31
type: "about"
layout: "about"
---
```

### 新建友链 friends 页（可选）

`friends` 页用于展示友情链接，若是 `source` 目录下还没有 `friends/index.md` 文件，就需要新建一个，回到博客根目录(`blog`文件夹)之后运行以下代码：

```
hexo new page "friends"
```

编辑刚新建的页面文件 `/source/about/index.md`，至少需要以下内容：

```
---
title: friends
date: 2021-05-27 11:51:08
type: "friends"
layout: "friends"
---
```

同时在博客 `source` 目录下新建 `_data` 目录，在 `_data` 目录中新建 `friends.json` 文件，内容如下：

```json
[{
    "avatar": "http://image.luokangyuan.com/1_qq_27922023.jpg",
    "name": "码酱",
    "introduction": "我不是大佬，只是在追寻大佬的脚步",
    "url": "http://luokangyuan.com/",
    "title": "前去学习"
}, {
    "avatar": "http://image.luokangyuan.com/4027734.jpeg",
    "name": "闪烁之狐",
    "introduction": "编程界大佬，技术牛，人还特别好，不懂的都可以请教大佬",
    "url": "https://blinkfox.github.io/",
    "title": "前去学习"
}, {
    "avatar": "http://image.luokangyuan.com/avatar.jpg",
    "name": "ja_rome",
    "introduction": "平凡的脚步也可以走出伟大的行程",
    "url": "ttps://me.csdn.net/jlh912008548",
    "title": "前去学习"
}]
```

### 代码高亮

使用了 [hexo-prism-plugin](https://github.com/ele828/hexo-prism-plugin) 的 Hexo 插件做代码高亮。返回根目录 `blog` 之后运行如下代码：

```
npm i -S hexo-prism-plugin
```

然后修改根目录下 `_config.yml` 文件中的 `higlight.enable` 值为 `false`，并新增 `prism` 插件相关配置：

```
highlight:
  enable: false

prism_plugin:
  mode: 'preprocess'    # realtime/preprocess
  theme: 'tomorrow'
  line_number: false    # default false
  custom_css:
```

---

# 20210530 
### 搜索

主题中使用了 [hexo-generator-search](https://github.com/wzpan/hexo-generator-search) 的 Hexo 插件来做内容搜索，先回到根目录后，命令如下：

```
npm install hexo-generator-search --save
```

在根目录下的 `_config.yml` 文件中新增以下配置：

```
search:
  path: search.xml
  field: post
```

### 中文链接转拼音（可选）

Hexo 默认会使得名称为中文的文章的永久链接中也有中文，这样会降低兼容性，而且 `gitment` 评论对中文链接也不支持，这里和教程中一样，使用 [hexo-permalink-pinyin ](https://github.com/viko16/hexo-permalink-pinyin) Hexo 插件在生成文章时生成中文拼音的永久链接：

```
npm i hexo-permalink-pinyin --save
```

在根目录下的 `_config.yml` 文件中新增以下配置：

```
permalink_pinyin:
  enable: true
  separator: '-' # default: '-'
```

### 文章字数统计（可选）

这里和教程中一样，使用 [hexo-wordcount ](https://github.com/willin/hexo-wordcount) Hexo 插件统计文章字数、阅读时长信息：

```
npm i --save hexo-wordcount
```

在根目录下的 `_config.yml` 文件中新增以下配置：

```
wordCount:
  enable: true
  postWordCount: true
  min2read: true
  totalCount: true
```

### 添加 RSS 订阅支持（可选）

这里和教程中一样，使用 [hexo-generator-feed ](https://github.com/hexojs/hexo-generator-feed) Hexo 插件提供 RSS 订阅功能：

```
npm install hexo-generator-feed --save
```

在根目录下的 `_config.yml` 文件中新增以下配置：

```
feed:
  type: atom
  path: atom.xml
  limit: 20
  hub:
  content:
  content_limit: 140
  content_limit_delim: ' '
  order_by: -date
```

执行 
```hexo clean && hexo g```

重新生成博客文件，然后在 `public` 文件夹中即可看到 `atom.xml` 文件，说明你已经安装成功了。

### 修改页脚

页脚修改的配置文件在主题文件(即`themes/hexo-theme-matery`文件夹)的 
`/layout/_partial/footer.ejs`，包括站点、使用的主题、访问量等。

这里我对作者信息进行了一下修改，需要到 `_config.yml` 文件中找到 `author:` 然后改成自己的信息。之后别忘了

```
hexo clean && hexo g
```
还有同步 `github` 哦

### 修改社交链接

在主题 `_config.yml` 文件中，默认支持 `QQ`/`Github`和邮箱的配置，可以在主题文件的 `/layout/_partial/social-link.ejs` 文件中，新增、修改你需要的社交链接地址，增加链接可参考如下代码：

```
<a href="https://github.com/blinkfox" class="tooltipped" target="_blank" data-tooltip="访问我的GitHub" data-position="top" data-delay="50">
    <i class="fa fa-github"></i>
</a>
```

其中，社交图标（如：fa-github）你可以在 [Font Awesome](https://fontawesome.com/v5.15/icons) 中搜索找到。以下是常用社交图标的标识，供参考：

- Facebook: fa-facebook
- Twitter: fa-twitter
- Google-plus: fa-google-plus
- Linkedin: fa-linkedin
- Tumblr: fa-tumblr
- Medium: fa-medium
- Slack: fa-slack
- 新浪微博: fa-weibo
- 微信: fa-wechat
- QQ: fa-qq

### 修改打赏的二维码图片

在主题文件的 `source/medias/reward` 文件中，你可以替换成你的的微信和支付宝的打赏二维码图片。

### 配置音乐播放器（可选）

要支持音乐播放，就必须开启音乐的播放配置和音乐数据的文件。

首先，在你的博客 `source` 目录下的 `_data` 目录（没有的话就新建一个）中新建 `musics.json` 文件，文件内容如下所示：

```
[{
    "name": "五月雨变奏电音",
    "artist": "AnimeVibe",
    "url": "http://xxx.com/music1.mp3",
    "cover": "http://xxx.com/music-cover1.png"
}, {
    "name": "Take me hand",
    "artist": "DAISHI DANCE,Cecile Corbel",
    "url": "/medias/music/music2.mp3",
    "cover": "/medias/music/cover2.png"
}, {
    "name": "Shape of You",
    "artist": "J.Fla",
    "url": "http://xxx.com/music3.mp3",
    "cover": "http://xxx.com/music-cover3.png"
}]
```

> 注：以上 JSON 中的属性：name、artist、url、cover 分别表示音乐的名称、作者、音乐文件地址、音乐封面。

然后，在主题的 `_config.yml` 配置文件中激活配置即可：

```
# 是否在首页显示音乐.
music:
  enable: true
  showTitle: false
  title: 听听音乐
  fixed: false # 是否开启吸底模式
  autoplay: false # 是否自动播放
  theme: '#42b983'
  loop: 'all' # 音频循环播放, 可选值: 'all', 'one', 'none'
  order: 'list' # 音频循环顺序, 可选值: 'list', 'random'
  preload: 'auto' # 预加载，可选值: 'none', 'metadata', 'auto'
  volume: 0.7 # 默认音量，请注意播放器会记忆用户设置，用户手动设置音量后默认音量即失效
  listFolded: false # 列表默认折叠
  listMaxHeight: # 列表最大高度
```

## 文章 Front-matter 介绍

### Front-matter 选项详解

`Front-matter` 选项中的所有内容均为非必填的。但教程的作者仍然建议至少填写 `title` 和 `date` 的值。

| 配置选项 |                         默认值 |                           描述                           |
| -------- | -----------------------------: | :------------------------------------------------------: |
| title    |            Markdown 的文件标题 |             文章标题，**强烈建议填写此选项**             |
| date     |           文件创建时的日期时间 | 发布时间，**强烈建议填写此选**项，且最好保证**全局唯一** |
| author   | 根 `_config.yml` 中的 `author` |                         文章作者                         |
| img |	featureImages 中的某个值 |	文章特征图，推荐使用图床(腾讯云、七牛云、又拍云等，我自己使用的是 picgo + github )来做图片的路径. 如: http://xxx.com/xxx.jpg
| top	 | true | 	推荐文章（文章是否置顶），如果 top 值为 true，则会作为首页推荐文章
| cover	| false | 	v1.0.2版本新增，表示该文章是否需要加入到首页轮播封面中
| coverImg |	无 |	v1.0.2版本新增，表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
| password	| 无 |	文章阅读密码，如果要对文章设置阅读验证密码的话，就可以设置 password 的值，该值必须是用 SHA256 加密后的密码，防止被他人识破。前提是在主题的 config.yml 中激活了 verifyPassword 选项
| toc	| true |	是否开启 TOC，可以针对某篇文章单独关闭 TOC 的功能。前提是在主题的 config.yml 中激活了 toc 选项
| mathjax| 	false|	是否开启数学公式支持 ，本文章是否开启 mathjax，且需要在主题的 _config.yml 文件中也需要开启才行
| summary	| 无|	文章摘要，自定义的文章摘要内容，如果这个属性有值，文章卡片摘要就显示这段文字，否则程序会自动截取文章的部分内容作为摘要
| categories| 	无|	文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类
| tags	|无 |文章标签，一篇文章可以多个标签

> 注意:

> 如果 `img` 属性不填写的话，文章特色图会根据文章标题的 `hashcode` 的值取余，然后选取主题中对应的特色图片，从而达到让所有文章都的特色图各有特色。
> `date` 的值尽量保证每篇文章是唯一的，因为本主题中 `Gitalk` 和 `Gitment` 识别 id 是通过 date 的值来作为唯一标识的。
> 如果要对文章设置阅读验证密码的功能，不仅要在 `Front-matter` 中设置采用了 SHA256 加密的 `password` 的值，还需要在主题的 `_config.yml` 中激活了配置。有些在线的 SHA256 加密的地址，可供使用：[开源中国在线工具](https://tool.oschina.net/encrypt?type=2)、[chahuo](http://encode.chahuo.com/)、[站长工具](http://tool.chinaz.com/tools/hash.aspx)。

以下为教程作者给出的示例：

### 最简示例

```
---
title: typora-vue-theme主题介绍
date: 2018-09-07 09:25:00
---
```


### 最全示例

```
---
title: typora-vue-theme主题介绍
date: 2018-09-07 09:25:00
author: 赵奇
img: /source/images/xxx.jpg
top: true
cover: true
coverImg: /images/1.jpg
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: false
mathjax: false
summary: 这是你自定义的文章摘要内容，如果这个属性有值，文章卡片摘要就显示这段文字，否则程序会自动截取文章的部分内容作为摘要
categories: Markdown
tags:
  - Typora
  - Markdown
---
```

---

## 自定制修改

在本主题的 `_config.yml` 中可以修改部分自定义信息，有以下几个部分：

- 菜单
- 我的梦想
- 首页的音乐播放器和视频播放器配置
- 是否显示推荐文章名称和按钮配置
- favicon 和 Logo
- 个人信息
- TOC 目录
- 文章打赏信息
- 复制文章内容时追加版权信息
- MathJax
- 文章字数统计、阅读时长
- 点击页面的’爱心’效果
- 我的项目
- 我的技能
- 我的相册
- Gitalk、Gitment、Valine 和 disqus 评论配置
- 不蒜子统计和谷歌分析（Google Analytics）
- 默认特色图的集合。当文章没有设置特色图时，本主题会根据文章标题的 hashcode 值取余，来选择展示对应的特色图

### 更多修改可能性

#### 修改主题颜色

在主题文件的 `/source/css/matery.css` 文件中，搜索 `.bg-color` 来修改背景颜色：

```
/* 整体背景颜色，包括导航、移动端的导航、页尾、标签页等的背景颜色. */
.bg-color {
    background-image: linear-gradient(to right, #4cbf30 0%, #0f9d58 100%);
}

@-webkit-keyframes rainbow {
   /* 动态切换背景颜色. */
}

@keyframes rainbow {
    /* 动态切换背景颜色. */
}
```

#### 修改 banner 图和文章特色图

可以直接在 `/source/medias/banner` 文件夹中更换喜欢的 `banner` 图片，主题代码中是每天动态切换一张，只需 7 张即可。如果你会 `JavaScript` 代码，可以修改成你自己喜欢切换逻辑，如：随机切换等，`banner` 切换的代码位置在 `/layout/_partial/bg-cover-content.ejs` 文件的 `<script></script>` 代码中：

```
$('.bg-cover').css('background-image', 'url(/medias/banner/' + new Date().getDay() + '.jpg)');
```

在 `/source/medias/featureimages` 文件夹中默认有 24 张特色图片，你可以再增加或者减少，并需要在 `_config.yml` 做同步修改。



---

# Todo：域名问题

暂时先凑合用，后面再琢磨域名问题(￣▽￣)"

---

# References

- [超详细Hexo+Github博客搭建小白教程](https://zhuanlan.zhihu.com/p/35668237)
- [Hexo博客主题之hexo-theme-matery的介绍](http://blinkfox.com/2018/09/28/qian-duan/hexo-bo-ke-zhu-ti-zhi-hexo-theme-matery-de-jie-shao/)
- [生成路径的问题，导致css，js无法加载 #1121](https://github.com/hexojs/hexo/issues/1121)