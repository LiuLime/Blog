# [Blog](https://blog.liulime.com)
[![image](https://img.shields.io/github/deployments/LiuLime/Blog/Production?label=vercel&logo=vercel&style=for-the-badge)](https://github.com/LiuLime/Blog/deployments)
![image](https://img.shields.io/github/last-commit/LiuLime/Blog?color=red&logo=github&style=for-the-badge)  
## 本地预览
```bash
$ brew install hugo # 如果没有安装hugo的话，请运行该指令
$ hugo server # 启动后请不要关闭该终端，post编辑完成后可结束本指令关闭该终端
```
## post
```bash
$ hugo new --kind post content/post/post_folder/post_name.md # 新建post
.
. # 编辑post 并且可以实时在本地浏览器查看预览页面
.
$ git add .
$ git commit -m "add post_name.md"
$ git push
```
## Notice !
Blog使用到的所有图片资源请放在static文件夹下。  
Hugo主题star数排行榜请参照[MGMCN整理的排行榜](https://github.com/MGMCN/hugoThemesRanking/blob/main/list.md)。
