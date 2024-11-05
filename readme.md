# 如何使用该文档
我们可以看到该文档有lesson1-15的文件夹，这几个文件夹可以作为独立的学习文档下载或使用；当然我们建议使用在线的mkdocs来更方便阅读。

最新更新的版本放在了 docs 文件夹内，也作为mkdocs的部署源文件；

如果你是自己下载该项目的话，需要安装mkdocs库并进行本地或在线部署
## mkdocs 安装
要安装 MkDocs，你可以使用以下命令通过 pip 进行安装：
```
pip install mkdocs
```
一些附加的主题（例如 mkdocs-material），可以使用以下命令：
```
pip install mkdocs-material
```
安装完成后，可以通过以下命令确认安装是否成功：
```
mkdocs --version
```

## mkdocs 本地部署
在终端加载到当**前项目文件夹**，运行本地部署命令：
```
mkdocs serve
```
会跳转得到本地html链接，打开即可进行阅读
## mkdocs 在线部署
以github为例，部署方式在终端加载到当前项目文件夹输入：（需要连接到github对应的repo）
```
mkdocs gh-deploy
```

当然我们也十分建议使用markdown阅读器进行阅读、编辑或学习
