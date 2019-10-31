---
title: github使用
date: 2018-03-27 14:22:05
updated: 2018-03-30 14:00:00
comments: true
tags:
- 摸鱼日志

categories:
copyright: true
urlname: github-ssh
---
# github 使用
```
ssh-keygen -C 'xxxx@qq.com' -t rsa
```

```
$ cd ~/.ssh
```
打开"id_rsa.pub"复制key
```
ssh -T git@github.com
```
$$F_{\mu}$$
$F_a + F_b = F_c$
$E=mc^2$
$$$A=B^2$$$
![](/upload_image/spongebob_72px_1066516_easyicon.net.png)

把_config.xml文件中的`repo:`修改成ssh提交的格式，修改后的代码如下：
```
deploy:
  type: git
  repo: git@github.com:heres-y/heres-y.github.io.git
  branch: master
```

参考网址：[git push 免密码](https://bryceyang.github.io/blog/2017/05/25/Tips/#heading-git-push-%E5%85%8D%E5%AF%86%E7%A0%81)