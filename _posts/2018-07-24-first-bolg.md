---
layout: post
title:  <!--"提升用户体验的前端动画"-->
categories: JavaScript
tags: 
author: DuPont
---
* content
{:toc}




##前言

算是第一篇博客吧，搞了两天 终于搞定了，前段时间学习的git ，在搭建博客额时候也算联系了一遍，解决了一些可能遇到常遇到的问题，下面列举一下问题，供自己以后参考吧。





##问题1
在本地的整个博客文件不能上传，原因：上传文件过大导致不能上传
####解决方法 ： 
1，修改 本地文件夹 .git里面 config 文件   里面有  
2，远端上传地址     在添加一个    
[http]  
    postBuffer = 524288000     
    改变上传大小
    




##问题2

githubdesktop不能跟remote 同步，因为通过本地push解决了，还没有找到原因，在改完.git里面的config文件后，desktop 弹出远端URL同步提醒  
原因:怀疑是git里面的config里面的 URL不正确。

##问题3
'''


error: failed to push some refs to 'https://github.com/dubang9/dubang9.github.io.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

'''




原因：  本地跟remote未同步
####解决办法
git pull --rebase git@github.com:dubang9/dubang9.github.io.git

##问题4
因为在github上initial一个repository的时候自动生成一个READ.ME文件，而我clone的repository里面也有一个READ.ME文件  导致不能push
####解决办法
因为只有自己一个人在弄这个blog，也不能考虑branch协同 ，所以就直接  git push -f 啦，偷懒强推了。

#总结
遇到问题时，先在纸上把可能的解决问题的方法步骤1，2，3，4 写下来。在操作的时候 ——对照纸上的草稿，完成一项标记一项。
#######谋定而后动
吐槽；github网速是真慢啊，一大半的时候都浪费在等待服务器响应上面了。
发现越到晚上 网速越慢，难道访问外网每天还限流的吗？