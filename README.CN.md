#  基于Hugo 双语博客示例



- 主题采用：[blowfish](https://github.com/nunocoracao/blowfish.git)
- 评论采用：[utteranc](https://utteranc.es/) 
- 采用 github action 自动发布




# 1. 配置 步骤

### 创建Github Page仓库
- 创建 `{username}.github.io` 项目 ： username 为你github 账号名，该项目为公共项目
- 生成ssh key

Linux/Mac
``` 

ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

```

假如已经生成记得不要覆盖，输入一个文件名：如 deploy_key，可在当前目录下生成 `deploy_key` 和 `deploy_key.pub` 文件(即使没生成也推荐输入文件名)

复制 `deploy_key.pub` 内容，在 当前仓库的 `settings` -> `Deploy Key` -> `Add deploy Key` 添加 `deploy_key.pub`值，记得勾选 write权限按钮


### 创建私有博客仓库

随便创建一个私有库，在该项目`settings` -> `Secrets And Variables` -> `Action` 添加 `secrets`, 其中 key 为 `ACTIONS_DEPLOY_KEY` 值为上面生成的`deploy_key`


### 配置博客

克隆当前仓库到本地,假如你下载了zip 文件，需要执行下面命令

删除 .gitmodules themes/blowfish
```bash

git init
git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish
```


将 https://github.com/nunocoracao/blowfish 替换成你的项目


修改配置项目：
[deploy.yml](.github%2Fworkflows%2Fdeploy.yml)

external_repository: username/username.github.io
cname: username.github.io

修改为你自己的用户名

config/_default/hugo.toml

```

baseURL = "https://{username}.github.io/"
```

修改配置名称：

- config/_default/languages.zh-cn.toml
- config/_default/languages.en.toml


修改个人按钮信息

- config/_default/menus.en.toml
- config/_default/menus.zh-cn.toml

修改网站配置如支持评论等
- config/_default/params.toml


## 可选： 开启评论

1. 创建github一个公开的项目如：blog_comments(假设你的账号名为 user)
[comments.html](layouts/partials/comments.html) 中
将 test/test_blog_comments 替换成 user/blog_comments

2. 将 [params.toml](config/_default/params.toml) 文件中 showComments = true
每篇文字头上添加 showComments: true

## 可选：支持私有域名
假如你有自己的私有域名：
修改[deploy.yml](.github%2Fworkflows%2Fdeploy.yml)  将cname 改成你的域名

cname: github.com

# 2.写博客

现在可以在 content 目录下面写博客了，可以参考[template.md](content/template.md) 写

可在文件夹上面放入一张 featured.png 图片

# 推荐配置

- categories： 为博客文章的大分类（如前端、后端），支持二级分类即（前端又可以分为 页面布局、动画、组件等）
- tags： 为当前知识细分种类，如 MySQL、Flutter、Redis 这种细分，支持多标签
- series： 为系列，即当一个知识点足够大，可以细分为一个系列，如ES使用介绍，可以分成系列，如：ES基础、ES进阶、ES实战，使用series_order 来当作序号



目前该示例采用了下面的分类：

- 规划 roadmap
- 设计 design
- - 构图 composition
- - 插画 illustration
- 前端 frontend
- - 布局 layout
- - 动画 animation
- 后端 backend
- - 网络 network
- - 数据库 database
- - 中间件 middleware
- - AI ai
- 随笔 essays
- - 编程 programming
- - 人生 life


