---
title: 如何在Github Pages上搭建User Page的hexo博客
date: 2019-09-21 14:20:31
tags: hexo,userPage,Github,TarvisCI
---

由官方教程给出的[推荐方式](https://hexo.io/zh-cn/docs/github-pages)，Travis CI会将public文件夹发布在gh-pages分支下，然而Github对于User Page的限制为仅允许使用master分支作为主分支。

所以需要以下操作：

首先，新建一个新的分支，以src为例。将hexo目录（包括_config.yml和package.json的目录）push到src分支，并在github端设置src分支为默认分支。

之后，修改.travis.yml文件：

```yaml
sudo: false
language: node_js
node_js:
  - 10 # use nodejs v10 LTS
cache: npm
branches:
  only:
    - src # 改为监视src分支
script:
  - hexo generate # generate static files
deploy:
  provider: pages
  skip-cleanup: true
  github-token: $GH_TOKEN
  target_branch: master # 发布目标为master分支
  keep-history: true
  on:
    branch: src # 发布来源为src分支
  verbose: true
  local-dir: public
```

这里要注意的是**deploy**和**branches**两段的修改。由监视master->从master编译->发布到gh-pages(默认)改为监视src->由src编译->发布到gh-pages。

之后本地修改文章时，请注意在src分支而并非master分支下修改。