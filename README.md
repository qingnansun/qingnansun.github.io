# NexT主题
## 更改为NexT主题
https://theme-next.iissnan.com/getting-started.html#install-next-theme





## Setup with HEXO
[Official document](https://hexo.io/docs/setup)

## Busuanzi counter for visits-counting
### Script in footer
```
      <script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
      <span id="busuanzi_container_site_pv"> 
        本站访问量<span id="busuanzi_value_site_pv"></span>次
      </span>
      <span id="busuanzi_container_site_uv"> 
        本站访客数<span id="busuanzi_value_site_uv"></span>人
      </span>
```

### Counter code for pages and articles
```
      <span id="busuanzi_container_page_pv">
        本文总阅读量<span id="busuanzi_value_page_pv"></span>次
      </span>
```

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

# To Try    
      {% set display_toc = is_post and theme.toc.enable %}
        {% if display_toc %}
              {% if toc.length <= 1 %}
                <p class="post-toc-empty">{{ __('post.toc_empty') }}</p>
              {% else %}
                <div class="post-toc-content-2">{{ toc }}</div>
              {% endif %}
        {% endif %}




        <input type="button" onclick="open_closeTOC()" id="showcloseButton">
        <script>
            function open_closeTOC() {
                var id = document.querySelector(".post-body > ul");
                if (id.style.display == "block") {
                    id.style.display = "none"; document.getElementById("showcloseButton").value = "展开目录";
                }
                else if (id.style.display == "none") {
                    id.style.display = "block"; document.getElementById("showcloseButton").value = "折叠目录";
                }
            }
            (function () {
                document.querySelector(".post-body > ul").style.display = "none"; document.getElementById("showcloseButton").value = "展开目录";
            })();
        </script>


## NEXT 配置
https://www.jianshu.com/p/3a05351a37dc

## 国际版
语言名称看语言包
https://hexo.io/zh-cn/docs/internationalization.html

## busuanzi失效
https://blog.csdn.net/ddydavie/article/details/83020549

## 字数统计
需要设置 并 安装插件
https://www.itfanr.cc/2017/12/06/hexo-blog-optimization/
https://www.jianshu.com/p/baea8c95e39b

## 置顶
http://wangwlj.com/2018/01/09/blog_pin_post/
https://lewky.cn/posts/6ed0d627.html  top可以编号

## 多级目录展开
https://github.com/iissnan/hexo-theme-next/issues/710


## RSS
站点配置和主题配置
https://www.jianshu.com/p/a79422ab2013
https://steemit.com/cn/@greedyboy/hexo-next-rss

## TODO
文章普通图片格式
手机版的开头目录
多语言版本
多lnk
描述
关键字