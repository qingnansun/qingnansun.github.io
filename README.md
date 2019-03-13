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

## busuanzi统计
https://lfwen.site/2016/11/13/next-busuanzi-vistor-count/ 

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


## 支持mermaid图
https://tyloafer.github.io/2018/04/21/hexo-mermaid/

## 设置置顶
http://wangwlj.com/2018/01/09/blog_pin_post/

## 报错
不能为空
hexo 报错 Cannot read property 'replace' of null

## Valine评论 - 已经包含在NEXT主题
https://mochazz.github.io/2018/10/20/%E4%B8%BAhexo%E7%9A%84even%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E8%AF%84%E8%AE%BA%E5%8A%9F%E8%83%BD/ 
http://smartsi.club/add-a-comment-function-to-the-next-theme-of-hexo.html
https://www.jianshu.com/p/728a9594bb6c
https://www.zhyong.cn/posts/95cb/
https://www.jianshu.com/p/7f5bf1221259  比较及来必力
https://ryanluoxu.github.io/2017/11/27/Hexo-Next-%E6%B7%BB%E5%8A%A0-Gitment-%E8%AF%84%E8%AE%BA%E7%B3%BB%E7%BB%9F/ gitment
https://sjq597.github.io/2018/05/18/Hexo-%E4%BD%BF%E7%94%A8Gitment%E8%AF%84%E8%AE%BA%E5%8A%9F%E8%83%BD/

## 侧边栏
http://www.voidcn.com/article/p-fdbltzkv-bpd.html

## NEXT 主题
https://hexo-guide.readthedocs.io/zh_CN/latest/theme/%E4%B8%BB%E9%A2%98%E7%89%88%E6%9C%AC%E7%AE%A1%E7%90%86.html
http://blog.shenyuanluo.com/HexoConfig1.html
http://mashirosorata.vicp.io/HEXO-NEXT%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE.html
https://fish-404.github.io/Blog-adjust-sidebar-nextmist-left/
https://juejin.im/post/5a31bf7451882512a8615077
美化-顶部进度条 https://www.jianshu.com/p/5017abb0d0a2

## 广告
https://www.93bok.com/Hexo%E7%AB%99%E7%82%B9Next%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0google%20adsense%E5%B9%BF%E5%91%8A/

## TODO
文章普通图片格式
手机版的开头目录
多语言版本
多lnk
描述
关键字
http://whatbeg.com/2017/03/23/addemailsubscribe.html

目录样式调整
https://www.jianshu.com/p/903ec28c5640

近期文章
http://bigdatadecode.club/hexo-next%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E8%BF%91%E6%9C%9F%E6%96%87%E7%AB%A0%E7%89%88%E5%9D%97.html

热文 related 插件
https://www.npmjs.com/package/hexo-related-popular-posts/v/2.0.1

解决百度爬虫无法抓取github pages
http://skyyangman.info/blog/2016/02/baidu-spider-forbidden.html
