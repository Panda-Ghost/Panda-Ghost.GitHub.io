---
layout: article
---

<div id="content">可爱捏</div>

<script>
    function post(str){
        let date=new Date();
        let res={time: date.getTime(), content: str};
        console.log(JSON.stringify(res))
    }
    function compare(a, b){
        return b.time - a.time;
    }
    function print(data){
        let i;
        let txt="<hr></hr>";
        data.sort(compare);
        for(i in data){
            console.log(data[i]);
            let time=new Date(data[i].time);
            let date=` ${time.getFullYear()}年 ${time.getMonth()+1}月${time.getDate()}日 ${time.getHours()}:${time.getMinutes()}`;
            let content=data[i].content;
            txt += `<div style="font-color:gray"><i class="fa-solid fa-clock"></i><span><strong>${date}</strong></span></div><p>${content}</p><hr></hr>`
        }
        document.getElementById("content").innerHTML=txt;
    }
    fetch("./data.json")
        .then((res) => res.json())
        .then((data) => print(data))
</script>