---
title: Github Pages with Jekyll Tutorial
layout: default
category: lessons
tags: [intro, jekyll, github, tutorial, beginner]
---

本篇介绍如何使用github pages作为个人blog, 用markdown语言编写博客并在本地通过jekyll预览

## 配置和使用Github
安装git或者github客户端以使用github, 注册github用户，新建一个username.github.io的repo, 用自己的用户名替换username

在username.github.io中新建index.html，稍后就可以通过http://username.github.io访问了

###使用Jekyll
可以通过fork别人使用jekyll的pages项目快速开始，这里不做介绍。

jekyll将markdown转为html显示为web页面，使用标记语言写文档更加直观和简单。

将username.github.io项目clone到本地，创建如下结构

    .
    |-- _config.yml
    |-- _layouts
    |   |-- default.html
    |-- _posts
    |   |-- 2015-05-02-hello-world.markdown
    |-- _site
    |-- index.html
    |-- images
        |-- *
    |-- css
        |-- *.css
    |-- javascripts
        |-- *.js

_config.yml保存配置信息

    baseurl: /
    auto: true

编辑javascripts, css, images及_layouts下的文件创建页面样式

_posts目录中新建post，使用YYYY-MM-DD-T-i-t-l-e.mardown命名

index.html中添加如下内容

    ---
    layout: default
    title: Weiluluwei.GitHub.io Blog
    ---
    
    <h2>{{ page.title }}</h2>
    <p>All blogs</p>
    <ul>
        {% for post in site.posts %}
        <li>{{ post.date | date_to_string }}    <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
        {% endfor %}
    </ul>

在_posts中添加文件就可以了

###本地预览
在发布之前可以在本地检查显示效果

首先要安装jekyll，确保ruby已经安装

    $gem install bundler
    $cat Gemfile
    source 'https://rubygems.org'
    gem 'github-pages'
    $bundle install

在repo目录运行jekyll

    $jekyll server

打开浏览器<http://127.0.0.1:4000>

###提交更改到github
_site是本地预览时转换html自动生成的文件夹，可以在.gitignore中忽略