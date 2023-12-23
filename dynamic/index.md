---
layout: article
---

<div id="content">加载中...</div>

<script>
    function transform(time){
        if(time == undefined){
            return false;
        }else{
            var minute = 1000 * 60;
            var hour = minute * 60;
            var day = hour * 24;
            var halfamonth = day * 15;
            var month = day * 30;
            var year = day * 365;
            // time = time.replace(/\-/g,"/");//把 - 替换为 / ，但在这没必要，其他地方可以用用
            var sTime = time;//把时间pretime的值转为时间戳
            var now = new Date().getTime();//获取当前时间的时间戳
            var diffValue = now - sTime;//获取时间差
            if(diffValue < 0){
                return false;
            }
            var yearC = diffValue/year;
            var monthC = diffValue/month;
            var weekC = diffValue/(7*day);
            var dayC =diffValue/day;
            var hourC =diffValue/hour;
            var minC =diffValue/minute;
            if(yearC>=1){
                // console.log(parseInt(yearC) + "年前");
                return parseInt(yearC) + "年前";
            }
            if(monthC>=1){
                // console.log(parseInt(monthC) + "个月前");
                return parseInt(monthC) + "个月前";
            }
            else if(dayC>=1){
                // console.log(parseInt(dayC) +"天前")
                return parseInt(dayC) + "天前";
            }
            else if(hourC>=1){
                // console.log(parseInt(hourC) +"小时前")
                return parseInt(hourC) + "小时前";
            }
            else if(minC>=1){
                // console.log(parseInt(minC) +"分钟前")
                return parseInt(minC) + "分钟前";
            }else{
                // console.log("刚刚")
                return "刚刚";
            }   
        }   
    }
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
            txt += `<span><strong>PandaGhost </strong></span><i class="fa-solid fa-clock" style="color:gray"></i><span style="color:gray"> ${transform(data[i].time)}</span><p>${content}</p><hr></hr>`
        }
        document.getElementById("content").innerHTML=txt;
    }
    fetch("./data.json")
        .then((res) => res.json())
        .then((data) => print(data))
</script>