1. 安装 hugo
```bash
brew install hugo
```

2. 使用 hugo 建一个网站，在 Downloads 文件夹下
```bash
cd ~/Downloads
hugo new site mysite
```
以上命令会在 Downloads 目录下生成一个 mysite 文件夹，目录树如下：
```
.
├── archetypes
│   └── default. md
├── assets
├── config. toml   // 需要配置的文件
├── content        // 博客存放位置
├── data
├── layouts
├── public
├── static         // 图片存放位置
└── themes         // 主题存放位置
```

3. 查找并使用主题
https://themes.gohugo.io
以 m10c 为例
```bash
cd ~/Downloads/mysite
git clone https://github.com/vaga/hugo-theme-m10c.git themes/m10c
```

4. 指定主题在本地启动服务器 (在 mysite 目录下执行)
```bash
hugo server -t m10c --buildDrafts
```
默认在 http://localhost:1313 运行

5. 上传个人博客
```bash
hugo new post/blog.md
```
![[Showcase.png]]

6. 其他配置需要参考 m10c 主题的手册

7. 使用 github 搭建个人远程博客
``` bash
hugo --baseUrl="https://shurgogo.github.io/" --buildDrafts
cd public
git init
git add .
git commit -m "hugo publish"
git branch -M main
git remote add origin git@github.com:shurgogo/shurgogo.github.io.git
git push -u origin main
```
等待 5 分钟左右，可以在 https://shurgogo.github.io 看到个人博客