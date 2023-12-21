---
title: 历史上的今天
---

<span id='year'>可爱捏</span>年，<span id='event'>可爱捏。</span>

<!--more-->

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
      document.getElementById('year').innerHTML = `${event.year}`;
      document.getElementById('event').innerHTML = `${event.title.slice(event.title.indexOf(':') + 1)}`;
    });
</script>
