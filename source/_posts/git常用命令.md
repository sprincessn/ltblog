---
title: git常用命令
date: 2019-07-26 11:08:30
tags: [git]
categories: git
---

1. 清除缓存

不小心输错用户名密码时，这时候提交会反复用缓存的身份数据导致一直失败，所以需要清除缓存，

git提交代码时清除用户和密码缓存：`git config --system --unset credential.helper`