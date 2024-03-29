---
title: Github+hexo网站搭建
date: 2021-11-10 18:30:00.0
updated: 2023-04-18 15:53:42
url: /archives/Github&hexo网站搭建
categories: 
- 博客
tags: 
- git
- github
- hexo
---

<p>&emsp;&ensp;  这个是我在网络上学习博客搭建而编写的教程，在这里我非常的感谢b站的 <a href="https://space.bilibili.com/350090479?spm_id_from=333.788.b_765f7570696e666f.1">CoolPlayer-函博</a>，<a href="https://space.bilibili.com/441519471?spm_id_from=333.788.b_765f7570696e666f.2">视频搬运崽啊</a> 和CSDN社区的大佬们。</p>
<!--more-->
<h2>前言</h2>
<p>使用github pages服务搭建博客的好处有：</p>
<blockquote>
<ul>
<li>全是静态文件，访问速度快；</li>
<li>免费方便，免费搭建个人博客，不需要服务器不需要后台；</li>
<li>可以随意绑定自己的域名；</li>
<li>数据绝对安全，基于github的版本管理，可以恢复历史版本；</li>
<li>博客内容可以轻松打包、转移、发布或分享到其它平台；</li>
<li>.......</li>
</ul>
</blockquote>
<h3>准备工作</h3>
<p>注册 <a href="https://github.com/">github账号</a>
安装node.js、npm、git</p>
<pre><code class="language-bash">node -v
npm -v
git --version</code></pre>
<p>输入以上指令检查软件是否安装，如果有错误请自行<a href="https://www.baidu.com">百度</a>查找原因</p>
<p>本文所使用的环境：</p>
<blockquote>
<p>Windiws 10
node 16.13.0
npm 8.1.0
git 2.34.0</p>
</blockquote>
<h2>搭建github博客</h2>
<h3>创建仓库</h3>
<p>新建一个名为 <font color=red>你的用户名.github.io</font> 的仓库(必须是你的用户名，其他名称无效)，建立之后你的网站访问地址就是http://你的用户名.github.io。
每一个github账户最多只能创建一个这样可以直接使用域名访问的仓库。</p>
<h3>绑定域名</h3>
<p>如果想要你的域名更个性一点，拥有自己的域名那就看看这一步吧:</p>
<p>首先注册一个域名，域名选择一定要选个大公司，在这里我推荐去<a href="https://sg.godaddy.com/zh/offers/domain?isc=gennbacn01&amp;countryview=1&amp;currencyType=CNY&amp;utm_source=baidu&amp;utm_medium=cpc&amp;utm_term=Title&amp;utm_campaign=zh%2Dcn%5Fcorp%2Dcore%5Fsem%5Fbh%5Fb%5Fz%5F001&amp;utm_content=Brandzone%20PC">godaddy</a> ,或者国内的<a href="https://wanwang.aliyun.com/">阿里云</a> 。</p>
<p>域名分为两种：带WWW的和不带WWW的。</p>
<p>域名配置最常见的方式：
1.记录类型分别填CNAME和A。
2.CNAME填写域名。
3.A记录值填写你的<font color=red>你的用户名.github.io</font>的网址IP。</p>
<blockquote>
<p>由于不带www方式只能采用A记录，所以必须先ping一下 <font color=red>你的用户名.github.io</font> 的IP，将ping出来的ip填入A记录值，这样才能保证无论是否添加www都可以访问。</p>
</blockquote>
<p>4.在你的github项目根目录新建一个名为CNAME的文件（无后缀），里面填写你的域名，加不加www看你自己喜好。</p>
<blockquote>
<ul>
<li>如果你填写的是没有www的，比如 mygit.me，那么无论是访问 <a href="http://www.mygit.me">http://www.mygit.me</a> 还是 <a href="http://mygit.me">http://mygit.me</a> ，都会自动跳转到 <a href="http://mygit.me">http://mygit.me</a></li>
<li>如果你填写的是带www的，比如 www.mygit.me ，那么无论是访问 <a href="http://www.mygit.me">http://www.mygit.me</a> 还是 <a href="http://mygit.me">http://mygit.me</a> ，都会自动跳转到 <a href="http://www.mygit.me">http://www.mygit.me</a></li>
<li>如果你填写的是其它子域名，比如 abc.mygit.me，那么访问 <a href="http://abc.mygit.me">http://abc.mygit.me</a> 没问题，但是访问 <a href="http://mygit.me">http://mygit.me</a> ，不会自动跳转到 <a href="http://abc.mygit.me">http://abc.mygit.me</a></li>
</ul>
</blockquote>
<p>5.绑定新域名之后，原来的<font color=red>你的用户名.github.io</font>并没有失效，而是会自动跳转到你的新域名。</p>
<h2>配置SSH key</h2>
<p>提交代码需要你的github权限，直接使用用户名和密码不安全，在这里我们我们使用ssh key来解决本地和服务器的连接问题。</p>
<p>用git bash执行如下命令:</p>
<pre><code class="language-bash">$ git config --global #user.name &quot;git用户名&quot;或邮箱地址 
$ cd ~/.ssh #检查本机已存在的ssh密钥
$ ls
$ ssh-keygen -t rsa -C #&quot;邮箱地址&quot; 连续回车三次</code></pre>
<pre><code class="language-bash">$ vim id_rsa.pub
：wq
$ ssh -T git@github.com    #查看安装成功</code></pre>
<p>查看公钥：cat id_rsa.pub 或者vim id_rsa.pub</p>
<p>复制 id_rsa.pub文件内容到githubkey里add就可以了</p>
<blockquote>
<p>打开github主页，进入个人设置 -&gt; SSH and GPG keys -&gt; New SSH key
将刚复制的内容粘贴到key那里，title随便填，保存。</p>
</blockquote>
<h3>测试是否成功</h3>
<pre><code class="language-bash">$ ssh -T git@github.com # 注意邮箱地址不用改</code></pre>
<p>如果提示 Are you sure you want to continue connecting (yes/no)?，输入yes，然后会看到：</p>
<blockquote>
<p>Hi liuxianan! You’ve successfully authenticated, but GitHub does not provide shell access.</p>
</blockquote>
<p>看到这个信息说明SSH已配置成功。</p>
<p>此时你还需要配置：</p>
<pre><code class="language-bash">$ git config --global user.name &quot;liuxianan&quot;// 你的github用户名，非昵称
$ git config --global user.email  &quot;xxx@qq.com&quot;// 填写你的github注册邮箱</code></pre>
<p>作用是执行hexo d操作后上传源代码</p>
<h2>使用hexo写博客</h2>
<h3>hexo介绍</h3>
<p><a href="http://hexo.io">Hexo</a>是一个简单、快速、强大的基于 <a href="https://github.com/hexojs/hexo">Github</a> Pages 的博客发布工具，支持Markdown格式，有众多优秀插件和主题。</p>
<h3>原理</h3>
<p>github pages存放的是静态文件，blog存放不只是文章内容，还有文章列表、分类、标签、翻页等动态内容，所以hexo所做的就是将这些md文件都放在本地，每次写完文章后调用写好的命令来批量完成相关页面的生成，然后再将有改动的页面提交到github。</p>
<h3>安装</h3>
<pre><code class="language-bash">$ npm install -g hexo</code></pre>
<h3>初始化</h3>
<p>在电脑建立名为name的文件夹，比如我的是 <font color=red>D:\Workspaces\blog</font> 。</p>
<pre><code class="language-bash">$ cd /D/Workspaces/blog/
$ hexo init</code></pre>
<p>hexo会自动下载一些文件到这个目录，包括node_modules</p>
<pre><code class="language-bash">$ hexo g # 生成
$ hexo s # 启动服务</code></pre>
<p>执行以上命令之后，hexo就会在public文件夹生成相关html文件，这些文件将来都是要提交到github去的。</p>
<pre><code class="language-bash">hexo s #开启本地预览服务</code></pre>
<p>浏览器打开http://localhost:4000 即可看到篇名为 Hello World 的文章，如果浏览器一直加载不出来可能是因为端口占用的缘故。</p>
<blockquote>
<p>解决端口冲突问题请参考这篇文章：
<a href="http://blog.liuxianan.com/windows-port-bind.html">http://blog.liuxianan.com/windows-port-bind.html</a></p>
</blockquote>
<h3>修改主题</h3>
<p>默认主题很丑，我们首先替换一个好看点的主题。这是<a href="https://hexo.io/themes/">官方主题</a> 。</p>
<p>我们以<a href="https://github.com/litten/hexo-theme-yilia">hexo-theme-yilia</a>主题为例:</p>
<p>首先下载这个主题：</p>
<pre><code class="language-bash">$ cd /f/Workspaces/hexo/
$ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia</code></pre>
<p>下载主题在 <font color=red>D:\Workspaces\blog\themes</font> 文件夹里。</p>
<p>修改<font color=red>_config.yml</font>中的<font color=red>theme: landscape</font>改为<font color=red>theme: yilia</font>。</p>
<pre><code class="language-bash">$ hexo clean #清理public文件夹
$ hexo g #重新生成</code></pre>
<h3>备份</h3>
<p>虽然github有版本管理，但备份一下总是好的（以防万一）</p>
<h3>上传到github</h3>
<p>配置 <font color=red>_config.yml</font> 中有关deploy的部分:</p>
<p>正确写法：</p>
<pre><code class="language-bash">deploy:
  type: git
  repository: git@github.com:liuxianan/liuxianan.github.io.git
  branch: master</code></pre>
<p>错误写法：
deploy:
type: github
repository: <a href="https://github.com/liuxianan/liuxianan.github.io.git">https://github.com/liuxianan/liuxianan.github.io.git</a>
branch: master</p>
<p>安装插件：</p>
<pre><code class="language-bash">npm install hexo-deployer-git --save</code></pre>
<p>没有安装此插件会报以下错误：</p>
<pre><code class="language-bash">Deployer not found: github 或 Deployer not found: git</code></pre>
<pre><code class="language-bash">git bash #部署</code></pre>
<p>部署这个命令一定要用git bash，否则会提示 <font color=red>Permission denied (publickey). </font></p>
<pre><code class="language-bash">$ hexo d #上传</code></pre>
<p>将本次有改动的代码全部提交，没有改动的不会</p>
<h3>保留CNAME、README.md等文件</h3>
<p>提交之后网页上一看，发现以前其它代码都没了，此时不要慌，一些非md文件可以把他们放到source文件夹下，这里的所有文件都会原样复制（除了md文件）到public目录。</p>
<p>hexo默认会把所有md文件都转换成html，包括README.md，所有需要每次生成之后、上传之前，手动将README.md复制到public目录，并删除README.html。</p>
<h2>常用hexo命令</h2>
<p>常见命令：</p>
<pre><code class="language-bash">hexo new &quot;postName&quot; #新建文章
hexo new page &quot;pageName&quot; #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，&#039;ctrl + c&#039;关闭server）
hexo deploy #部署到GitHub
hexo help  # 查看帮助
hexo version  #查看Hexo的版本</code></pre>
<p>缩写：</p>
<pre><code class="language-bash">hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy</code></pre>
<p>组合命令；</p>
<pre><code class="language-bash">hexo s -g #生成并本地预览
hexo d -g #生成并上传</code></pre>
<h3>_config.yml</h3>
<p>可以在 _config.yml 中修改</p>
<pre><code class="language-bash"># Hexo Configuration
## Docs: http://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/
# Site 站点配置
title: Hexo-demo #网站标题
subtitle: hexo is simple and easy to study #网站副标题
description: this is hexo-demo #网栈描述
author: pomy #你的名字
language: zh-CN #网站使用的语言
timezone: Asia/Shanghai #网站时区
# URL #可以不用配置
## If your site is put in a subdirectory, set url as &#039;http://yoursite.com/child&#039; and root as &#039;/child/&#039;
url: http://yoursite.com #网址，搜索时会在搜索引擎中显示
root: / #网站根目录
permalink: :year/:month/:day/:title/ #永久链接格式
permalink_defaults: #永久链接中各部分的默认值
# Directory 目录配置
source_dir: source #资源文件夹，这个文件夹用来存放内容
public_dir: public #公共文件夹，这个文件夹用于存放生成的站点文件
tag_dir: tags #标签文件夹
archive_dir: archives #归档文件夹
category_dir: categories #分类文件夹
code_dir: downloads/code #Include code 文件夹
i18n_dir: :lang #国际化文件夹
skip_render: #跳过指定文件的渲染，您可使用 glob 来配置路径
# Writing 写作配置
new_post_name: :title.md # 新文章的文件名称
default_layout: post #默认布局
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0 #把文件名称转换为 (1) 小写或 (2) 大写
render_drafts: false #显示草稿
post_asset_folder: false #是否启动资源文件夹
relative_link: false #把链接改为与根目录的相对位址
future: true
highlight: #代码块的设置
enable: true
line_number: true
auto_detect: true
tab_replace:
# Category &amp; Tag 分类 &amp; 标签
default_category: uncategorized #默认分类
category_map: #分类别名
tag_map: #标签别名
# Date / Time format 时间和日期
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss
# Pagination 分页
## Set per_page to 0 to disable pagination
per_page: 10 #每页显示的文章量 (0 = 关闭分页功能)
pagination_dir: page #分页目录
# Extensions 扩展
## Plugins: http://hexo.io/plugins/ 插件
## Themes: http://hexo.io/themes/ 主题
theme: landscape #当前主题名称
# Deployment #部署到github
## Docs: http://hexo.io/docs/deployment.html
deploy:
type:</code></pre>
<p>一般主题下有一个 languages 文件夹，用于对应 language 配置项。比如在 ejs 中有：</p>
<p>&lt;%= __('tags') %&gt;</p>
<p>language 的配置项是 zh-CN ，则会在 languages 文件夹下找到 zh-CN.yml 文件中对应的项来解释。</p>
<p>修改全局配置时，注意缩进，同时注意冒号后面要有一个空格。</p>
<h3>新建博客文章</h3>
<pre><code class="language-bash">hexo new &#039;my-first-blog&#039;</code></pre>
<p>hexo会帮我们在<font color=red>_posts</font>下生成相关md文件</p>
<p>我们只需要打开这个文件就可以开始写博客了，默认生成如下内容：</p>
<pre><code class="language-bash">---
title: my-first-blog
date: 2021-11-19 10:40:00
tags:
---</code></pre>
<p>也可以直接自己新建md文件，用这个命令的好处是帮我们自动生成了时间。</p>
<p>一般完整格式如下：</p>
<pre><code class="language-bash">---
title: postName #文章页面上的显示名称，一般是中文
date: 2013-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
categories: 默认分类 #分类
tags: [tag1,tag2,tag3] #文章标签，可空，多标签请用格式，注意:后面有个空格
description: 附加一段文章摘要，字数最好在140字以内，会出现在meta的description里面
---

以下是正文</code></pre>
<pre><code class="language-bash">hexo new page &quot;my-second-blog&quot;</code></pre>
<p><font color=red>hexo new page 'postName'</font>命令和<font color=red>hexo new 'postName'</font>区别:</p>
<p>最终部署时生成：blog\public\my-second-blog\index.html，但是它不会作为文章出现在博文目录。</p>
<h3>如何让博文列表不显示全部内容</h3>
<p>默认情况下，生成的博文目录会显示全部的文章内容，如何设置文章摘要的长度呢？</p>
<p>答案：是在合适的位置加上<!--more-->即可，例如：</p>
<pre><code class="language-bash">这个是我在网络上学习的Github+hexo搭建的网站，在这里我非常的感谢b站的 [CoolPlayer-函博](https://space.bilibili.com/350090479?spm_id_from=333.788.b_765f7570696e666f.1)，[视频搬运崽啊](https://space.bilibili.com/441519471?spm_id_from=333.788.b_765f7570696e666f.2) 和CSDN社区的大佬们。

&lt;!--more--&gt;

## 前言
使用github pages服务搭建博客的好处有：

>* 全是静态文件，访问速度快；
>* 免费方便，免费搭建个人博客，不需要服务器不需要后台；
>* 可以随意绑定自己的域名；
>* 数据绝对安全，基于github的版本管理，可以恢复历史版本；
>* 博客内容可以轻松打包、转移、发布或分享到其它平台；
>* .......</code></pre>
<h3>Custom 404页面</h3>
<p>在blog/source目录下创建404.html</p>
<p>404.html的内容可以设置为下面的内容 _config.yml中的permalink_defaults属性不需要修改）.</p>
<pre><code class="language-bash">---
layout: default
---
&lt;html&gt;
    &lt;head&gt;
         &lt;meta charset=&quot;UTF-8&quot; /&gt;
         &lt;title&gt;404&lt;/title&gt;                                                                                                                                        
    &lt;/head&gt;
    &lt;body&gt;
         &lt;script type=&quot;text/javascript&quot; src=&quot;http://www.qq.com/404/search_children.js&quot; charset=&quot;utf-8&quot;&gt;&lt;/script&gt;
    &lt;/body&gt;
&lt;/html&gt;</code></pre>
<p>简化:</p>
<pre><code class="language-bash">&lt;script type=&quot;text/javascript&quot; src=&quot;http://www.qq.com/404/search_children.js&quot; charset=&quot;utf-8&quot;&gt;&lt;/script&gt;</code></pre>
<h2>其他</h2>
<h3>中文乱码</h3>
<p>在md 文件中写中文内容，发布出来后为乱码，原因是md的编码不对，将md文件另存为“UTF-8”编码的文件即可解决问题。</p>