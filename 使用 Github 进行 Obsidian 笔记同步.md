https://blog.csdn.net/m0_54185999/article/details/134753360
### 前言

本文主要介绍了obsidian使用git插件进行多端同步的方法，远程仓库为[github](https://so.csdn.net/so/search?q=github&spm=1001.2101.3001.7020)，如果觉得github网络不稳定，也可以使用国内的gitee。

#### 什么是obsidian

Obsidian 是一款功能强大的笔记应用程序，它支持使用[Markdown语法](https://markdown.com.cn/cheat-sheet.html) 创建和组织笔记。它依靠双链功能可以很容易的建立笔记间的关联。优点是笔记可以本地离线保存，打开速度非常快，不用担心[服务器](https://so.csdn.net/so/search?q=%E6%9C%8D%E5%8A%A1%E5%99%A8&spm=1001.2101.3001.7020)数据丢失。缺点是多端数据同步功能需要收费，不过也可以根据网上的方法实现免费同步，本文使用obsidian的git插件实现多端同步。

#### Obsidian下载

官网下载，然后根据平台选择版本下载，**建议使用迅雷下载**，浏览器可能下载不下来。  
官网：https://obsidian.md/download  
安卓版：https://wwdx.lanzoue.com/b030yr97g

#### git软件准备

1. git安装  
    [Git 安装-廖雪峰博客](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)
2. git配置  
    git config --global user.name “用户名”  
    git config --global user.email “你的邮箱”
3. 生成密钥  
    `ssh-keygen -t rsa -C "你的邮箱"`  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/a563d250709248f4a530c5eafbe049ed.png)  
    根据上图红线路径，复制公钥 id_rsa.pub
4. 将公钥粘贴到GitHub  
    注册[github](https://github.com/)账号，登录GitHub，点击右上角用户头像图标，点击Settings，进入设置页面  
    Settings页面点击“SSH and GPG keys”，然后点击右上角“New SSH key”，添加ssh key  
    Title填入名称，key填入复制的id_rsa.pub内容，然后点击“Add SSH key”  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/d614d75fd14346bb976c3b23c6ea9ca2.png)

#### 创建github仓库

1. 登录github，创建私有仓库  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/feeaa72dad6e424781c2520cebe4890d.png)
2. 选择SSH，记住自己的仓库.git结尾的那个：  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/310c7b3d66ae4fd6a5b19b63a3c2b0cb.png)

#### obsidian安装git插件

为了实现Obsidian与GitHub的同步，还需要安装Obsidian Git插件。这个插件能够自动将本地保存的笔记文件推送（push）到GitHub仓库，并在每次打开Obsidian时自动从GitHub仓库中拉取（pull）最新的文件。

1. 打开obsidian，点击“设置”-“文件与链接”-“第三方插件”，关闭“安全模式”，点击“社区插件”的“浏览”，搜索“Obsidian Git”然后安装  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/034425cb9c604b21b1af81894c8955ec.png)  
    也可以通过链接下载，下载后放到.obsidian/plugins目录下，没有plugins创建  
    git插件：链接: https://pan.baidu.com/s/1RkiMgTb28TF6FcejTUpnpg 提取码: nvbt
2. 将你现有笔记push到远程仓库  
    在你的笔记目录，Windows右键选择open git bash here，linux直接执行命令。  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/ad449cf4c4b140f88445dcb81ee40bc9.png)  
    假设你的笔记仓库名为obdocs

```
git init 
git add obdocs
git commit -m "first commit" 
git remote add origin git@github.com:xxx/testgit.git     #这里替换成自己的仓库
git push -u origin main
```

3. 启动插件  
    配置插件实现文件自动commit和push到仓库

- 以下配置表示每隔2分钟会commit和push，每次5分钟会自动pull最新版本。  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/679529ea784e4281925f9c22db217c37.png)
- 以下配置表示，软件启动会自动pull最新版本。  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/3a54a25db72d4e4db5d27bbef8c140bf.png)

4. 配置.gitignore 文件  
    在自己的笔记目录下创建.gitignore文件，**注意**.gitignore 文件一定要包含 .obsidian/workspace.json 文件，同时最好不要有50M以上的大文件，避免引起麻烦。或者也可以将 .obsidian加入.gitignore文件。  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/11e3147998574e36842f2709d8deebce.png)  
    将 .obsidian加入.gitignore文件可以写成：  
    /.obsidian/

#### 其他终端同步

其他终端先使用git clone拉取分支，然后就可以编辑笔记了，最好不要多个终端同时操作，会造成冲突。  
`git clone git@github.com:xxx/testgit.git`