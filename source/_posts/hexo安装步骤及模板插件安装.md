title: hexo安装步骤及模板插件安装
date: 2016-01-27 19:03:48
tags: hexo安装步骤,hexo模板安装,hexo插件安装,hexo
---
作为一个技术小白我竟然可以用 **Markdown** 写博客了！当然Hexo的安装就废掉我不少力气，还有怎么发布到GitHub上也很难为我，虽然花了有近一周时间才搞定这点东西，但还是值得的！（还能怎么说？）博客的安装发布耗费了不少力气，第一篇博客赶紧把过程记录下来，免得以后老眼昏花又搞不来了，，，主要是那些代码我背不住。奶奶个胸，写这点东西的时候脑子里尽然想到一个可恶的人。。。 

### [给自己的友情链接-- Cmd Markdown](https://www.zybuluo.com/mdeditor)

** 跟着我来 **

> * 环境准备
> * 安装Hexo
> * 发布Hexo到GitHub
> * hexo博客更换主题
> * hexo博客绑定个人域名



## 环境准备 

Hexo本身安装很简单，网上教程一大堆，但是我刚开始连环境都安装不成功， 比如要安装GIT、Homebrew、npm、nvm、node.js等，我反反复复的安装了无数次，才算是有了一丢丢经验，先都记在这里!

思路是：
先安装Homebrew
使用Homebrew安裝nvm
使用nvm安裝Node.js
使用nvm无痛切换Node.js版本
Node.js自带npm
用npm安装hexo
hexo安装主题theme，写文章什么的
用hexo s -debug预览
预览没问题用hexo g生成静态页
最后用hexo d发布到git的默认分支master

在做以上动作之前要先建立本地电脑与自己github的连接，要知道git是个版本管理工具，github是远程仓库。

以下都是终端（terminal）里输的啊，复制进去回车就行。

### 升级Xcode,这是解决一大堆BUG的终极大招，安装后会发现再安装别的就不会老失败了，你要反反复复的失败的话先找苹果算账。

> xcode-select --install

### 安装Homebrew

> ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)”  #安装homebrew
> brew tap phinze/homebrew-cask && brew install brew-cask  #安装 brew-cask
> brew update

这一步比较容易成功，基本上都不会出错

#### 使用Homebrew安裝nvm 

> brew install nvm

安裝完后，为了让你可以直接在shell使用nvm指令，必须在你的 .bash_profile 加入以下这行：
> source $(brew --prefix nvm)/nvm.sh

或者直接输入以下这行来加入：
> echo "source $(brew --prefix nvm)/nvm.sh" >> .bash_profile

记得重新source你的 .bash_profile来让设定生效：
>  . ~/.bash_profile

这样就完成了nvm的安裝

#### 使用nvm安裝Node.js

> nvm ls-remote  #先看有哪些版本可以安装
> nvm use --delete-prefix v0.12.9 --silent  #经常失败可以用这个选个最新版
> node -v  可以验证有没安装成功


## 用npm安装hexo

> npm install hexo-cli -g
> 运行 ' hexo s --debug '，并访问 ' http://localhost:4000 '，查看站点是否正确运行

npm安装不成功可以
> sudo rm -rf /usr/local/{lib/node{,/.npm,_modules},bin,share/man}/{npm*,node*,man1/node*}
> npm install -g npm-autoinit
> npm config set onload-script npm-autoinit/autoinit
> npm install

## 发布Hexo到GitHub
- 在github创建仓库（Create a new repository），Repository name填：benbenlang.github.io点最下面的绿色按钮
- 在benbenlang.github.io创建两个分支：master 与 hexo；
- 设置hexo为默认分支（因为我们只需要手动管理这个分支上的Hexo网站文件）；
- 使用git clone git@github.com:benbenlang/benbenlang.github.io.git拷贝仓库到自己电脑；
- cd到本地benbenlang.github.io文件夹下在终端里依次执行
  npm install hexo #在本地仓库安装hexo
  hexo init  #初始化仓库
  
  此时benbenlang.github.io仓库里的_config.yml文件最下面分支branch值应该是hexo）;
  比如这样： 
  > deploy:
  type: git
  repo: https://github.com/benbenlang/benbenlang.github.io.git
  branch: hexo

  npm install  #安装些东西
  npm install hexo-deployer-git --save（此时本地仓库里的_config.yml文件分支branch应该是hexo）;
- 然后修改_config.yml中的deploy，分支branch值改为master；
- 依次执行
git add .
git commit -m “…”
git push origin hexo 向hexo分支提交网站相关的文件；
- 执行hexo g -d生成网站并部署到GitHub上。
这样一来，在GitHub上的benbenlang.github.io仓库就有两个分支，一个hexo分支用来存放网站的原始文件，一个master分支用来存放生成的静态网页。

以上这些都是学习 [CrazyMilk](http://crazymilk.github.io/) 大神的,我对大神的崇拜之情如滔滔江水，绵绵不绝！

## hexo博客更换主题

cd到自己本地仓库的benbenlang.github.io文件夹
> git clone https://github.com/wuchong/jacman.git themes/jacman  #把主题下载到本地的themes文件夹

修改benbenlang.github.io文件夹里_config.yml的theme属性，将其设置为jacman
> git push origin master  #把主题提交到远端仓库
> hexo s #预览主题
> hexo g -d #发布

## hexo博客绑定个人域名

这个我还没搞，好像不算太难。

**MAC下加环境变量 .bash_profile的方法**
> cd ~ #进入文件夹
> touch .bash_profile #回车
> open -e .bash_profile
> export PATH=${PATH}:/usr/local/mysql/bin

### 安装 Node.js

> curl https://raw.github.com/creationix/nvm/master/install.sh | sh
安装完成后，重启终端并执行下列命令即可安装 Node.js
> nvm install 4



每次改完东西都要输
> npm install hexo-deployer-git --save
> git pull origin master
> hexo g #生成静态页
> hexo s #本地预览测试
> hexo g -d #发布

> { [Error: Cannot find module './build/Release/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
{ [Error: Cannot find module './build/default/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }
{ [Error: Cannot find module './build/Debug/DTraceProviderBindings'] code: 'MODULE_NOT_FOUND' }

解决方案：

使用命令npm install hexo --no-optional

