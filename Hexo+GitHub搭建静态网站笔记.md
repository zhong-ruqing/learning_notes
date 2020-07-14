# Hexo+GitHub搭建静态个人网站笔记

- 笔记日期：2020.07.10
- 系统配置：Win10 (x64)

## 参考攻略

- [hexo官方文档](https://hexo.io/zh-cn/docs/)
- [Hexo小书](https://pengloo53.gitbooks.io/hexo/content/)
- [知乎笔记参考](https://zhuanlan.zhihu.com/p/26625249)

## 为什么选了Hexo + GitHub

我对自己个人网站目前的要求是不需要太炫酷的界面和响应式设计，能用于记录自己的作品和笔记就行，基于这点去查询了很多相关建站教程的信息。

从零开始纯代码搭建网站是有兴趣的，但是目前学习时间不足。不想用WordPress或者是Wix等去创建我的网站，主要原因是因为一旦适应一个架构之后想换出来可能比较麻烦，加上WordPress需要自己去购买云服务器，Wix虽然提供云服务器服务，也是需要每个月收费不少的，嫌贵嫌麻烦，不适合我这种佛系建站派。

如果用GitHub作为免费云端服务器托管自己的网站，网址能自动生成，如果想替换成个人买的域名也方便。于是去查了查，发现很多人用GitHub+Hexo的组合来搭建自己的个人网址，因为Hexo是GitHub上免费开源的项目，而且创建者是台湾人，所以对中文的支持也很好。去了[Hexo官网](https://hexo.io/zh-cn/)查看了相关介绍，有几点我很喜欢：

- 支持一键部署到GitHub Pages
- 支持Markdown，网页内容用markdown整理即可，不需要自己写html代码
- 有很多开源插件和主题能够选用

符合我的需求，也是在我能力范围之内，所以决定用这个方式搭建我的网站。

# 搭建步骤

必要

- GitHub创建个人仓库 
- 安装Git
- 安装Node.js
- 安装Hexo
- 建站
- 推送网站到GitHub
- 发布文章

可选

- 更换主题
- 获得个人网站域名并绑定
- 其他

## GitHub创建个人仓库

登录到GitHub,如果没有GitHub帐号，使用你的邮箱注册GitHub帐号：[Build software better, together](https://link.zhihu.com/?target=https%3A//github.com/) 点击GitHub中的New repository创建新仓库，仓库名应该为：**用户名**.github.io ，这个**用户名**使用你的GitHub帐号名称代替，这是固定写法，我的是zhong-ruqing.github.io。不用**用户名**作为仓库名也可以，但是后续操作稍微麻烦一点，我没有去细查，就按固定用法来了。

## 安装Git

- [Git](http://git-scm.com/) 

Git是开源的分布式版本控制系统，用于敏捷高效地处理项目。网站在本地搭建好了，需要使用Git同步到GitHub上。从Git官网下载：[Git - Downloading Package](https://link.zhihu.com/?target=https%3A//git-scm.com/download/win) ，选择适合自己机型的安装包，下载后安装。打开命令行输入`git`测试git是否安装成功。命令行中输入`git --version`可以查看安装版本。

安装成功后，绑定Git与GitHub账号，可以参考[Git官网绑定教程](https://docs.github.com/en/github/getting-started-with-github/set-up-git)，或者[git & github学习笔记](https://github.com/zhong-ruqing/learning_notes/blob/master/git_github_tutorial/git_github_tutorial.md)。

我已经安装过了，所以这一步我是跳过的。

## 安装Node.js

- [Node.js](http://nodejs.org/) (Node.js 版本需不低于 8.10，建议使用 Node.js 10.0 及以上版本)

备注： hexo是基于Node.js的，安装Node.js会包含环境变量以及npm的安装。我点进链接后找到适合自己电脑版本的软件安装包，下载后一键安装。安装后，检测Node.js是否安装成功，在命令行中输入：

```bash
$ node -v
```

检测npm是否安装成功，在命令行输入：

``` bash
$ npm -v
```

安装好Git和Node.js后，安装Hexo的环境已经搭建好了。

## 安装hexo

在必备应用程序安装完之后，打开命令行窗口，可以使用npm安装hexo：

```bash
$ npm install -g hexo-cli
```

## 建站

安装完hexo之后，在指定文件夹下打开命令行窗口（命令行上显示的当前目录应和指定文件夹一致），执行下列命令，hexo会在指定文件夹中新建所需文件：

```bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

我的`<folder>`取名是blog。

新建完成后，指定文件夹目录如下：

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

做完这些之后，就可以试试开始用hexo命令创建新的博客啦。

### 基本命令介绍（Quick Start）

- 注意：这些命令应该在上一步建站时创建的<folder>中打开命令行运行。

#### 创建新的博客 （Create a new post）

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

- 这条命令实际上为` $ hexo new post "My New Post" ` , 但`post`是默认的，所以可以省去。

#### 生成静态网页文件（Generate static files）

``` bash
$ hexo generate
```

可简写

```bash
$ hexo g
```

More info: [Generating](https://hexo.io/docs/generating.html)

- 这条命令是用于生成网页文件的。

#### 启动服务器预览（Run server）

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

可简写：

```bash
$ hexo s
```

- 这时候命令行里会出现本地测试地址，一般是 <http://localhost:4000>，打开浏览器输入该地址就可以预览生成的网站页面了。

### 测试网站雏形

- 打开命令行，输入上面三条基本命令：

```bash
$ hexo new "test_my_site"

$ hexo g

$ hexo s
```

- 在浏览器中输入 <http://localhost:4000>可以看到出现hexo的基本界面

## 推送网站到GitHub

### 推送网站命令（Deploy to remote sites）

这一步将会用到的命令是：

``` bash
$ hexo deploy
```

可简写

```bash
$ hexo d
```

More info: [Deployment](https://hexo.io/docs/one-command-deployment.html)

在使用这条命令之前我们应该先修改站点配置文件，并且安装Git部署插件，详见接下来两条内容的介绍。

### 修改站点配置文件

这是建立网站的根目录：

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes

```

根目录里的`_config.yml`是**站点配置文件**， 进入根目录里的themes文件夹也有个`_config.yml`，是**主题配置文件**。

我们在这里需要打开的是**站点配置文件**的`_config.yml`。打开文件后翻到文件末尾，修改为：

```
deploy:
	type: git
	repo: 这里填入你之前在GitHub上创建仓库的完整路径（攻略说后面要加上 .git，不过我没加好像也没问题）
	branch: master
```

我的是：

```
deploy:
  type: git
  repo: https://github.com/zhong-ruqing/zhong-ruqing.github.io
  branch: master
```

保存设置好的站点配置文件。设置站点配置其实就是给`hexo d `这个命令做相应的配置，让hexo知道你要把blog部署在哪个位置，很显然，我是要部署在我的GitHub的仓库里。

### 安装Git部署插件

在命令行中输入命令：

```bash
$ npm install hexo-deployer-git --save
```

### 测试推送网站

在命令行中输入命令：

```bash
$ hexo clean 
$ hexo g 
$ hexo d
```

完成后，打开浏览器，在地址栏输入你的放置个人网站的仓库路径，即 <http://xxxx.github.io>（可以在GitHub仓库对应的Settings中找到GitHub Pages一栏，下面有一行写着<https://xxxx.github.io/>）。

我的是<https://zhong-ruqing.github.io/>。

这时候打开浏览器输入该地址，应该就可以看到自己发布的网页了。

## 发布文章

### 创建文章

在命令行中输入：

```bash
$ hexo new "文章名称"
```

在网站文件夹根目录下（看你自己建的文件夹名字，我的是blog）的source文件夹的_post文件夹里，多出了一个叫**文章名称.md**的文件，用markdown编辑器打开就可以开始编辑要发布的文章了。

### 编辑预览

- 通过带有预览样式的Markdown编辑器实时预览书写的博文样式
- 也可以通过命令` hexo s --debug `在本地浏览器的 <http://localhost:4000> 预览博文效果

### 发布

写好博文并且样式无误后，通过`hexo g`加`hexo d` 来生成和部署网页。随后可以在浏览器中输入域名浏览。

## 更换主题

在网站根目录中themes文件夹里查看自己的主题是什么，hexo默认主题是landscape。

如果不喜欢Hexo默认的主题，可以更换不同的主题，Hexo官网有主题板块：[Themes](https://link.zhihu.com/?target=https%3A//hexo.io/themes/)。

选好主题点进去之后一般都会有教程教如何安装和配置主题，基本配置步骤一般都是用`git clone`将喜欢的主题下载到网站根目录的themes相应文件夹中，再打开**站点配置文件**`_config.yml`拉到最下面，将`theme: landscape`修改为`theme: 你喜欢的主题名`。具体详见各个主题安装配置教程即可。

## 获得个人网站域名并绑定

### 购买域名

申请域名的地方有很多，比较了一下和GoDaddy的价格，我选了阿里云：[阿里云-为了无法计算的价值](https://link.zhihu.com/?target=https%3A//www.aliyun.com/)， 域名申请入口：[域名注册](https://link.zhihu.com/?target=https%3A//wanwang.aliyun.com/domain/) 。

选择好喜欢的域名购买相应套餐即可。我购买的是zhongruqing.com。

### 在GitHub 仓库里添加一个CNAME文件

- CNAME一定要大写
- CNAME存储时一定要存为*(.) all types*文件，不能是*.txt*
- CNAME文件中内容只写自己的域名，可以带www，也可以不带，建议不带www，因为这样访问时带不带www都可以访问到，我的文件内容是：

```
zhongruqing.com
```



### 绑定域名到GitHub网页

- 第一步

登录到阿里云，进入管理控制台的域名列表，找到你的个性化域名，进入DNS解析，在解析列表里添加以下三条记录，用自己的GitHub用户名替换username，我是zhong-ruqing.github.io：

```
@          A             192.30.252.153
@          A             192.30.252.154
www      CNAME           username.github.io
```

其中，192.30.252.153是GitHub的地址。

- 第二步

登录GitHub，进入之前创建的仓库，点击settings，设置Custom domain，输入你的域名，点击save保存。

- 第三步

在GitHub 仓库里添加一个CNAME文件，这个可以通过在本地网站文件夹中添加一个CNAME文件实现，因为hexo会自动生成这个文件并且部署到GitHub中，注意：

- 创建文件的位置是`本地网站根文件夹/source目录`下，我的是`blog/source` 
- 文件名CNAME一定要大写
- 可以用记事本文件创建，但存储时一定要存为*(.) all types*文件，不能是*.txt*
- CNAME文件中内容只写自己的域名，可以带www，也可以不带，建议不带www，因为这样访问时带不带www都可以访问到，我的文件内容是：

```
zhongruqing.com
```

- 测试

完成这三步之后，打开浏览器输入自己的个性化域名，应该会直接进入自己搭建的网站了。

## 常用命令

### 简历新页面（Create a new page）

```bash
$ hexo new page "My new Page"
```

### 清除网页缓存（Clean）

```bash
$ hexo clean
```

可简写

```bash
$ hexo c
```

可以清除用于生成网页缓存，网页怎么都不正常的时候，比如换了主题之后怎么都不对，可以用这条命令。一般我会输入下面三条命令之后再查看预览：

``` bash
$ hexo clean
$ hexo g
$ hexo s
```

## 进阶功能

### Hexo 标签插件（Tag Plugins）

<https://hexo.io/zh-cn/docs/tag-plugins.html>

用于在文章中快速插入特定内容的插件。

### 插入Vimeo或者YouTube视频

在Vimeo上的视频下找到Share标签，点击之后复制Embed下面的代码放入需要的markdown文档里即可。