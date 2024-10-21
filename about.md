---
layout: articlenoc
title: 关于
show_author_profile: true
---

## 历史上的今天

<p id='todinhis'>出错了捏</p>

<script>
  let today = new Date();
  let path = ''
  
  if (today.getMonth() < 9) {
    path += '0'
  }
  path += `${(today.getMonth() + 1)}`

  if (today.getDate() < 10) {
    path += '0'
  }
  path += `${today.getDate()}`
  
  fetch(`https://panda-ghost.github.io/todayinhistory/${path}.json`)
    .then((response) => response.json())
    .then((data) => {
      let event = data[Math.floor(today.getFullYear()%data.length)];
      let inner = `${event.year}年的今天，${event.title.slice(event.title.indexOf(':') + 1)}`;
      document.getElementById('todinhis').innerHTML=inner
    });
</script>

## 有用的东西

- [Graph Editor (csacademy.com)](https://csacademy.com/app/graph_editor/)
- [算法学习笔记（目录） - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/105467597)
- [hzwer.com - Home](http://hzwer.com/)
- [洛谷 - 计算机科学教育新生态 (luogu.com.cn)](https://www.luogu.com.cn/)
- [AcWing](https://www.acwing.com/)
- [OI Wiki (oi-wiki.org)](https://oi-wiki.org/)
- [Font Awesome](https://fontawesome.com/)
- [奇趣网站收藏家](https://fuun.fun/)
- [colorate](https://colorate.azurewebsites.net/)

## 友链

- [tianrui-huang.github.io](https://tianrui-huang.github.io/)
- [ShwBlog](https://shwst.one/)
- [Mekdull's Blog](https://mekdull.netlify.app/)
- [TzBlog - Tz的个人博客](https://tzblog.tech/)
- [AlexEinstein's Blog](https://alexeinstein.github.io/)
- [Qiuuu's Blog](https://qiuuu1504.github.io)
- [shijihong's Blog](https://shijihong2008.github.io)


## 本站的 GitHub 仓库

- [Click Here](https://github.com/Panda-Ghost/Panda-Ghost.GitHub.io/)
