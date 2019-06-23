---
title: 5分钟利用Github+Hexo搭建个人博客!
date: 2018-06-22 14:22:05
updated: 2018-06-22 14:22:05
tags:
- 摸鱼日志

urlname: github+hexo
categories: [hexo]
copyright: true

---

### 前言
本文记录了使用github+hexo搭建个人博客的过程以及搭建过程中遇到的一些问题。


关于使用hexo搭建博客，[hexo官网](https://hexo.io/zh-cn/)已经有了很详细的介绍，但官方文档的介绍往往是力求全面详尽而显得过于冗长(尽管hexo已经够简洁了)，下面介绍如何以最快的速度实现一个“最小hexo系统”。

搭建环境为Ubuntu16.04.(Windows/Mac/Linux等其他环境请参考[hexo官网](https://hexo.io/zh-cn/))

<!-- more -->
- - -

### 安装hexo
1. 安装Git：
```
$ sudo apt-get install git-core
```

2. hexo是基于Node.js的静态博客，需要使用node.js里的npm工具，所以接下来下载Node.js。以下两种方式二选一即可。
```
$ curl https://raw.github.com/creationix/nvm/master/install.sh | sh
$ wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
```

3. 下载完成后，重启终端并执行下列命令
```
$ nvm install stable
```
至此，我们完成了安装hexo的准备工作。而安装hexo呢，只需一个命令：
4. 安装hexo
```
$ npm install hexo-cli -g
```

hexo安装完毕！
- - -

### 发布你的第一篇文章
1. 初始化hexo
```
$ hexo i blog //init的缩写 blog是项目名
$ cd blog //切换到站点根目录
$ npm install
$ hexo g //generetor的缩写
$ hexo s //server的缩写
```

2. 创建第一篇文章
```
hexo new mypaper.md
//文章会生成在/blog/sorce/_post/下
```

3. 本地服务器访问网页
打开浏览器输入`localhost:4000`查看网页效果，当然，此时只是默认主题，如果不喜欢可以使用[next](https://github.com/iissnan/hexo-theme-next)，这是一个界面简洁且功能丰富的主题。

4. 设置github仓库
在github上新建一个repository并且务必命名为`username.github.io`。
修改本地blog根目录下的配置文件_config.xml:
```
deploy:
	type: git
	repo: git@github.com:username/username.github.io.git
	branch: master
```

5. 安装插件
```
$ npm install hexo-deployer-git --save
```

6. 将博客部署到github上
```
hexo clean
hexo g //generate
hexo d //deploy
```


### 花里胡哨的东西
##### 首页只显示「摘要」

在首页显示一篇文章的部分内容，并提供一个链接跳转到全文页面是一个常见的需求。 NexT 提供[三种方式](http://theme-next.iissnan.com/faqs.html#%E9%A6%96%E9%A1%B5%E6%98%BE%E7%A4%BA%E6%96%87%E7%AB%A0%E6%91%98%E5%BD%95)来控制文章在首页的显示方式。 也就是说，在首页显示文章的摘录并显示 阅读全文 按钮，可以通过以下方法：

1.在文章中使用 `<!-- more -->` 手动进行截断，Hexo 提供的方式 「推荐」
2.在文章的 front-matter 中添加 description，并提供文章摘录

3.自动形成摘要，在 主题配置文件 中添加：
```
    auto_excerpt:
      enable: true
      length: 150
```
默认截取的长度为 150 字符，可以根据需要自行设定

建议使用 `<!-- more -->`（即第一种方式），除了可以精确控制需要显示的摘录内容以外， 这种方式也可以让 Hexo 中的插件更好的识别。

**尝试了第一二种方式，但是第二种方式在超过一行的情况下不work，还没有找到解决方法。**


————20190618更新————


##### 页面点击小红心

将 love.js 文件添加到 \themes\next\source\js\src 文件目录下。
love.js:
```
!function(e,t,a){function r(){for(var e=0;e<n.length;e++)n[e].alpha<=0?(t.body.removeChild(n[e].el),n.splice(e,1)):(n[e].y--,n[e].scale+=.004,n[e].alpha-=.013,n[e].el.style.cssText="left:"+n[e].x+"px;top:"+n[e].y+"px;opacity:"+n[e].alpha+";transform:scale("+n[e].scale+","+n[e].scale+") rotate(45deg);background:"+n[e].color+";z-index:99999");requestAnimationFrame(r)}var n=[];e.requestAnimationFrame=e.requestAnimationFrame||e.webkitRequestAnimationFrame||e.mozRequestAnimationFrame||e.oRequestAnimationFrame||e.msRequestAnimationFrame||function(e){setTimeout(e,1e3/60)},function(e){var a=t.createElement("style");a.type="text/css";try{a.appendChild(t.createTextNode(e))}catch(t){a.styleSheet.cssText=e}t.getElementsByTagName("head")[0].appendChild(a)}(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"),function(){var a="function"==typeof e.onclick&&e.onclick;e.onclick=function(e){a&&a(),function(e){var a=t.createElement("div");a.className="heart",n.push({el:a,x:e.clientX-5,y:e.clientY-5,scale:1,alpha:1,color:"rgb("+~~(255*Math.random())+","+~~(255*Math.random())+","+~~(255*Math.random())+")"}),t.body.appendChild(a)}(e)}}(),r()}(window,document);

```
找到 \themes\next\layout\_layout.swing 文件， 在文件的后面，</body> 标签之前 添加以下代码：
```
<!-- 页面点击小红心 -->
<script type="text/javascript" src="/js/src/love.js"></script>
```


##### 背景的设置
将 particle.js 文件添加到 \themes\next\source\js\src 文件目录下。
```
!function(){function n(n,e,t){return n.getAttribute(e)||t}function e(n){return document.getElementsByTagName(n)}function t(){i=a.width=window.innerWidth||document.documentElement.clientWidth||document.body.clientWidth,c=a.height=window.innerHeight||document.documentElement.clientHeight||document.body.clientHeight}function o(){d.clearRect(0,0,i,c);var n,e,t,a,m,r,y=[x].concat(w);w.forEach(function(o){for(o.x+=o.xa,o.y+=o.ya,o.xa*=o.x>i||o.x<0?-1:1,o.ya*=o.y>c||o.y<0?-1:1,d.fillRect(o.x-.5,o.y-.5,1,1),e=0;e<y.length;e++)n=y[e],o!==n&&null!==n.x&&null!==n.y&&(a=o.x-n.x,m=o.y-n.y,r=a*a+m*m,r<n.max&&(n===x&&r>=n.max/2&&(o.x-=.03*a,o.y-=.03*m),t=(n.max-r)/n.max,d.beginPath(),d.lineWidth=t/2,d.strokeStyle="rgba("+u.c+","+(t+.2)+")",d.moveTo(o.x,o.y),d.lineTo(n.x,n.y),d.stroke()));y.splice(y.indexOf(o),1)}),l(o)}var i,c,a=document.createElement("canvas"),u=function(){var t=e("script"),o=t.length,i=t[o-1];return{l:o,z:n(i,"zIndex",-1),o:n(i,"opacity",.5),c:n(i,"color","0,0,0"),n:n(i,"count",99)}}(),m="c_n"+u.l,d=a.getContext("2d"),l=window.requestAnimationFrame||window.webkitRequestAnimationFrame||window.mozRequestAnimationFrame||window.oRequestAnimationFrame||window.msRequestAnimationFrame||function(n){window.setTimeout(n,1e3/45)},r=Math.random,x={x:null,y:null,max:2e4};a.id=m,a.style.cssText="position:fixed;top:0;left:0;z-index:"+u.z+";opacity:"+u.o,e("body")[0].appendChild(a),t(),window.onresize=t,window.onmousemove=function(n){n=n||window.event,x.x=n.clientX,x.y=n.clientY},window.onmouseout=function(){x.x=null,x.y=null};for(var w=[],y=0;u.n>y;y++){var s=r()*i,f=r()*c,h=2*r()-1,g=2*r()-1;w.push({x:s,y:f,xa:h,ya:g,max:6e3})}setTimeout(function(){o()},100)}();

```
找到 \themes\next\layout\_layout.swing 文件， 在文件的后面，</body>标签之前 添加以下代码：
```
<!-- 背景动画 -->
<script type="text/javascript" src="/js/src/particle.js"></script>
```
##### 给 Github 添加 README
默认情况下，Github中每一个项目，我们希望有一份 README.md 的文件来作为项目的说明，但是我们在项目根目录下的 blog\source 目录下创建一份 README.md 文件，写好说明介绍，部署的时候，这个 README.md 会被 hexo 解析掉，而不会被解析到 Github 中去的。
正确的解决方法其实很简单：
方法1：
把 README.md 文件的后缀名改成 “MDOWN” 然后扔到blog/source文件夹下即可，这样 hexo 不会解析，Github 也会将其作为 MD 文件解析。
方法2：
解决方法很简单，在站点配置文件中，搜索 skip_render:，在其冒号后加一个空格然后加上 README.md 即可。


<div style='display: none'>
##### 实现guestbook留言板功能
进入到博客的根目录，运行命令：
```
hexo new page guestbook
```
</div>
##### 添加Local search功能
安装搜索插件：
```
hexo-generator-searchdb
```

在博客根目录下执行以下命令：
```
$ npm install hexo-generator-searchdb --save
```
配置博客
安装完成，编辑博客配置文件：_config.yml
```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```
配置主题
Next 主题自带搜索设置，编辑主题配置文件：_config.yml

找到文件中 Local search 的相关配置，设为 true
```
# Local search
local_search:
  enable: true
```
hexo 重新部署

##### hexo本地图片插入
关于图片插入，耗费了我一些时间。最初我是在/source/文件夹下建立了一个upload_image/用来存放图片，在markdown中调用时是`![image](../../upload_image/image.png)`这种形式，可以看出，需要向上跳两级目录，才能找到对应的图像。
后来又尝试把图像直接放在与.md文件同一目录下，要不然是在编辑markdown时不显示，要不然是生成的静态网页不显示。
找了好久终于在[Hexo 图片插入](http://www.xinxiaoyang.com/programming/2016-11-25-hexo-image-bug/)找到了解决方法，需要安装
```
npm install https://github.com/CodeFalling/hexo-asset-image --save
```
这样一个插件。方可以使用相对路径的图片，既可以在markdown中显示，也可以在网页中显示。



### 参考资料
[1] [大道至简——Hexo简洁主题推荐](https://www.haomwei.com/technology/maupassant-hexo.html)
[2][Hexo-NexT搭建个人博客（二）](https://neveryu.github.io/2016/09/30/hexo-next-two/#5-%E9%BC%A0%E6%A0%87%E7%82%B9%E5%87%BB%E5%B0%8F%E7%BA%A2%E5%BF%83%E7%9A%84%E8%AE%BE%E7%BD%AE)
[3][Hexo 搭建博客的个性化设置二](https://dingxuewen.com/2017/03/03/Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2%E7%9A%84%E4%B8%AA%E6%80%A7%E5%8C%96%E8%AE%BE%E7%BD%AE%E4%BA%8C/)
[4][Hexo NexT 主题添加留言本页面](https://blog.paddings.cn/2016/05/11/blog/hexo-guestbook/)
[5][hexo - Next 主题添加搜索功能](https://yashuning.github.io/2018/06/29/hexo-Next-%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%90%9C%E7%B4%A2%E5%8A%9F%E8%83%BD/)