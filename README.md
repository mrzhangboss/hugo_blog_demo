# Based on Hugo Bilingual Blog Example ([中文](README.CN.md))

- Theme used: [blowfish](https://github.com/nunocoracao/blowfish.git)
- Comments via: [utteranc](https://utteranc.es/) 
- Auto-publish using GitHub Actions

# 1. Configuration Steps

### Create a GitHub Page Repository
- Create the `{username}.github.io` project: `username` is your GitHub username, and this project should be public.
- Generate an SSH key

Linux/Mac

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"


```


If you have already generated one, make sure not to overwrite it. Enter a file name, such as `deploy_key`. This will generate `deploy_key` and `deploy_key.pub` files in the current directory. (Even if it hasn't been generated, it's recommended to enter a file name.)

Copy the contents of `deploy_key.pub` and add it to the `settings` -> `Deploy Key` -> `Add deploy Key` of the current repository, making sure to check the write permissions button.

### Create a Private Blog Repository

Create any private repository. In the project's `settings` -> `Secrets And Variables` -> `Action`, add `secrets`, with the key `ACTIONS_DEPLOY_KEY` and the value being the `deploy_key` generated above.

### Configure the Blog

Clone the current repository locally. If you downloaded a zip file, you need to execute the following commands:

```bash

git init
git submodule add -b main https://github.com/nunocoracao/blowfish.git themes/blowfish

```


Replace https://github.com/nunocoracao/blowfish with your project URL.

Modify the configuration:

- config/_default/hugo.toml



```

baseURL = "https://{username}.github.io/"

```

Modify the configuration names:

- config/_default/languages.zh-cn.toml
- config/_default/languages.en.toml

Modify personal button information:

- config/_default/menus.en.toml
- config/_default/menus.zh-cn.toml

Modify website configurations such as enabling comments:

- config/_default/params.toml


## Optional: Enable Comments
Create a public GitHub project such as blog_comments (assuming your username is user). In [comments.html](layouts/partials/comments.html), 

replace test/test_blog_comments with user/blog_comments.

In the [params.toml](config/_default/params.toml) file, 
set showComments = true. Add showComments: true at the top of each article.


