# Blog
## 本地预览
```bash
$ brew install hugo # 如果没有安装hugo的话，请运行该指令
$ hugo server # 启动后请不要关闭该终端
```
## post
```bash
$ hugo new --kind post content/post/post_folder/post_name.md # 新建post
.
. # 编辑post 并且可以实时在本地网页查看预览
.
$ git add .
$ git commit -m "add post_name.md"
$ git push
```
