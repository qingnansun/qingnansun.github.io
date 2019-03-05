
## Setup with HEXO
[Official document](https://hexo.io/docs/setup)

## Busuanzi counter for visits-counting
Script in footer
Counter code for pages and articles

## Map counter 
Creat the following the mapcounter file

Themes\landscape\layout\_widget\mapcounter.ejs

```
<div class="widget-wrap">
    <h3 class="widget-title"><%= __('Counter') %></h3>
    <div class="widget">
        <script type="text/javascript" src="//ra.revolvermaps.com/0/0/8.js?i=0n4gowqtyrd&amp;m=0&amp;c=ff0000&amp;cr1=ffffff&amp;f=arial&amp;l=33" async="async"></script>
    </div>
</div>
```
Then add the mapcounter widget in the themes Configure file
```
widgets:
- category
- tag
- tagcloud
- archive
- recent_posts
- mapcounter
```

## SEO
http://www.admintony.com/Hexo%E5%81%9ASEO%E4%BC%98%E5%8C%96%E9%81%87%E5%88%B0%E7%9A%84%E5%9D%91.html

https://chenhuichao.com/2018/04/27/seo/seo-hexo-optimization/

## Relative path of the pictures

使用标签插件模式
```
{% asset_img 1_北漂.jpg %}
{% asset_img 1_北漂.jpg title %}
```
http://www.xinxiaoyang.com/programming/2016-11-25-hexo-image-bug/

https://yanyinhong.github.io/2017/05/02/How-to-insert-image-in-hexo-post/

## 设置使新建post的文件名带日期
在站点设置文件中如下修改
```
# Writing
new_post_name: :year:month:day-:title.md # File name of new posts
```

参考： https://hexo.io/zh-cn/docs/writing

## 根据目录生成类别
Use the plugin [hexo-directory-category](https://www.npmjs.com/package/hexo-directory-category)


## 生成文章目录
### 设置显示目录 

- 将TOC代码加在以下文件的header部分，否则会双重编号。
- 如果使用目录样式设置部分的css，则可以放在content前

\themes\landscape\layout\_partial\article.ejs

```
<!-- Table of Contents -->
<% if (!index){ %>
<div id="toc" class="toc-article">
<strong class="toc-title">文章目录</strong>
<%- toc(post.content) %>
</div>
<% } %>
```
### 修改目录样式
\themes\landscape\source\css\_partial

```
/*toc*/
.toc-article
  background #eee
  border 1px solid #bbb
  border-radius 10px
  margin 1.5em 0 0.3em 1.5em
  padding 1.2em 1em 0 1em
  max-width 35%
.toc-title
  font-size 120%
  font-weight:bold
#toc
  line-height 1em
  font-size 0.9em
  float right
  .toc
    padding 0
    margin 1em
    line-height 1.8em
    li
      list-style-type none
  .toc-child 
    margin-left 1em
```
参考:
http://charmlegal.com/2017/12/05/article6/


## 疑难问题
### 本地和发布的样式不同

全局设置中的网址改成自己的  
`url: http://qingnansun.github.io`

如果已经设置了ssl，则为  
`url: https://qingnansun.github.io`

