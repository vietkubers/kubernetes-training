# How to public your posts to github-page?

1. **Fork** the repo https://github.com/vietkubers/vietkubers.github.io to your Github account
2. **Clone** the above forked repo to your local directory
```
$ git clone https://github.com/$USER/vietkubers.github.io.git
```
3. **Create** a markdown file in folder [_post](https://github.com/vietkubers/vietkubers.github.io/tree/master/_posts) and name it as `yyyy-mm-dd-ten-bai-viet.md`
```
$ cd vietkubers.github.io.git/_post
$ touch yyyy-mm-dd-ten-bai-viet.md
```
4. **Modify** the created post with declaration section as:
```
---
layout: post
title: Deploying multiple nodes with Kubeadm
date: 2018-11-16
categories: [linux, tutorials, kubernetes]
tags: [Linux, Tutorials, Kubernetes]
---
```
Please refer to [this example post](https://raw.githubusercontent.com/vietkubers/vietkubers.github.io/master/_posts/2018-11-21-deploying-multiplenodes-with-kubeadm.md) for more details.

5.  Commit, push and create your Pull Request

