git init 
git add obdocs
git commit -m "first commit" 
git remote add origin git@github.com:xxx/testgit.git     #这里替换成自己的仓库
git push -u origin main

4. 配置.gitignore 文件  
    在自己的笔记目录下创建.gitignore文件，**注意**.gitignore 文件一定要包含 .obsidian/workspace.json 文件，同时最好不要有50M以上的大文件，避免引起麻烦。或者也可以将 .obsidian加入.gitignore文件。  
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/11e3147998574e36842f2709d8deebce.png)  
    将 .obsidian加入.gitignore文件可以写成：  
    /.obsidian/

[微信读书-正版书籍小说免费阅读 (qq.com)](https://weread.qq.com/)