layout: hexo+github
title: Hexo+GitHub Pages如何搭建并异地管理Blog
date: 2016-05-31 14:35:09
tags: 技术杂谈
---
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="http://music.163.com/outchain/player?type=2&id=441532&auto=1&height=66"></iframe>
<body>
	最近看到知乎上出了一篇<a href="http://www.jianshu.com/p/4eaddcbe4d12">《5分钟 搭建免费个人博客》</a>的文章，鉴于最近公司比较闲，于是乎便跟着作者所给的教程走了一遍，结果发现作者在写的时候好像写错了一个地方，在安装Nodejs的时候，作者告诉用HomeBrew安装，但是我在安装的时候发现采用HomeBrew安装存在一些问题，于是乎从GitHub上找到了nvm的原作者<a href="https://github.com/creationix/nvm">Tim Caswell</a>发现其实nvm并不支持Homebrew的安装，只能采用<code>curl</code>或者<code>wget</code>的方式安装，所以说如果有通过上述文章搭建博客的同学注意了，采用如下方式：
	<ul>
	<li><code>curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash</code></li>
	或者
	<li><code>wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash</code></li>
	</ul>
就可以了。但是文中并没有说明如何异地来管理博客，众所周知如果代码不能异地管理那么我们仅凭每天拷贝代码来管理代码这得多么痛苦，所以结合<a href="http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo搭建博客/">GitHub Pages + Hexo搭建博客</a>这篇文章我决定重新写一篇如何搭建并如何异地管理博客的文章。<br>
在这里我给大家提供两种方式来供大家使用，一种是开源仓库一种是私密仓库，都是基于Git的一种托管。
<p><font size="4px" color="red">好了废话不多说，在开始之前请大家查看一下系统有没有安装Git，Nodejs以及Hexo。不管你是第一次建立博客还是说异地管理都需要上述三个方面的支持。</font></p>
<ul>
<li><h4>git 安装</h4>
<code>brew install git</code>确保已安装Homebrew，如果没安装那就先百度下安装Homebrew。</li>
<li><h4>安装Nodejs</h4></li>
使用<ul>
	<li><code>curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash</code></li>
	或者
	<li><code>wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash</code></li>
	</ul>
	先安装nvm然后重启终端运行<br><code>nvm install 4</code>
	<li><h4>安装Hexo</h4></li>
	完成上述安装后运行以下命令<br><code>sudo npm install hexo-cli -g</code>
</ul>
<ul>
<li><h3>采用GitHub Pages仓库对应的分支进行管理</h3></li>
首先就像<a href="http://www.jianshu.com/p/4eaddcbe4d12">《5分钟 搭建免费个人博客》</a>这个文章中说的一样，打开自己的GitHub如果没有自己就注册一个，然后如下图<br>
<img src="http://o7daudvnt.bkt.clouddn.com/blog0.png"></img><br>
点击New，进入到如下图所示内容<br>
<img src="http://o7daudvnt.bkt.clouddn.com/blog11.png"></img><br>
创建一个本地仓库。仓库名称的前缀要与你的名字一样。然后进入下图所示，创建一个名字为hexo的分支用来管理你博客的hexo代码。<br>
<img src="http://o7daudvnt.bkt.clouddn.com/blog12.png"></img><br>点击Setting中的Branches选项，将hexo设置为默认分支，如下图，<br>
<img src="http://o7daudvnt.bkt.clouddn.com/blog13.png"></img><br>点击update即可。返回到分支上使用<br><code>git clone https://github.com/ClayGuitar/ClayGuitar.github.io.git</code><br>
这个命令将你的仓库克隆到你想克隆的地方。然后cd到你刚才clone的仓库下面，<br>
<code>git branch -a</code><br>
查看一下你所在的分支，在确保是在hexo分支的情况下运行命令<br>
<code>hexo init</code>如图：<br>
<img src="http://o7daudvnt.bkt.clouddn.com/blog14.png"></img><br>
等运行完后使用以下命令<br>
<code>hexo s</code><br>,
如下图<br>
<img src="http://o7daudvnt.bkt.clouddn.com/blog15.png"><br>
进入上述网址查看以下hexo创建的博客是否成功，在这里推荐一下<a href="https://github.com/lenbo-ma/hexo-theme-vno">hexo-theme-vno</a>一个博客主题。<br>
测试没问题后在仓库目录下安装<a href="https://github.com/hexojs/hexo-deployer-git">hexo-deployer-git</a><br>
<code>npm install hexo-deployer-git --save</code><br>
这个时候你会认为已经完成了，但是不好意思，并没有，你会发现在使用了<code>hexo init</code>命令后原有的远程仓库不见了，所以这个时候需要你重新加载一下远程仓库，使用如下命令<br>
<ol>
<li><code>git init</code></li>//初始化本地仓库
<li><code>git remote add origin https://github.com/ClayGuitar/ClayGuitar.github.io.git</code></li>//添加远程仓库
<li><code>git fetch && git checkout hexo</code></li>//拉取并且切换到hexo分支
</ol>
然后大功告成,打开你仓库的目录下的_config.yml文件，将其deploy参数改一下，如下图
<img src="http://o7daudvnt.bkt.clouddn.com/blog16.png"></img><br>
接下来就是发布到你的GitHubPages上去了，命令如下<br>
<code>hexo clean && hexo g && hexo d</code>
</body><br>
输入在浏览器上输入<a href="http://clayguitar.github.io/">http://clayguitar.github.io/</a>看下有没有问题，如果没有那就运行以下命令将所有的文件提交到hexo分支上。
<ol>
<li><code>git add .</code></li>
<li><code>git commit -m'提交hexo文件'</code></li>
<li><code>git push origin hexo</code></li>
</ol>
下次异地管理的时候只需电脑确保有Git、Nodejs以及Hexo环境下，直接<code>git clone</code>将项目从GitHub上clone到本地，然后cd到仓库目录下，运行以下命令:<br>
<code>rm -rf .deploy_git</code><br>
将.deploy_git隐藏文件夹删除，不然hexo g -d部署博客的时候会将整个项目部署到其master分支上。然后再执行上述发布到GitHub Pages以及提交分支命令即可。
<li><h3>采用私有仓库管理</h3></li>
我是利用Bitbucket来管理私人仓库的，你也可以用别的私人仓库，其实都大同小异。这里我还是以Bitbucket为例，
<ul>
<li><h5>1.创建私有仓库</h5>
<img src="http://o7daudvnt.bkt.clouddn.com/blog17.png"></img><br></li>
<li><h5>2.打开我有一个已经存在的项目</h5><img src="http://o7daudvnt.bkt.clouddn.com/blog18.png"></img><br>根据提示的命令行进行操作,在这里如果文件夹没有git本地仓库记得先<br>
<code>git init</code><br>
一下。然后再<br>
<code>git remote add origin https://bielian@bitbucket.org/bielian/hexo.git</code></li>
</ul>
剩下的步骤就参考上述GitHub分支如何异地管理步骤。
</ul>

