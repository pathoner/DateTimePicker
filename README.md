# DateTimePicker
一个基于localStorage的时间记录点
晚上一直在弄类似微博发布时间的工具。自己的想法是做一个本地的localstirage，但是每次刷新页面时，原来数组的内容总是被重置。导致上次的时间点一直不能记录，
每次都是新的时间点。不过最后自己还是解决了这个问题。<br/>
最开始代码如下：
``` javascript
var yyear = []
// 创建时间对象 类似 2017/10/16 21:30 的数据格式的时间对象
var datefunction = function() {
        var date = new Date();
        var year =  date.getFullYear()
        var month = date.getMonth() + 1
        var day = date.getDate()
        var hours = date.getHours()
        var minutes = date.getMinutes()
        var Y_m_d = `${year}/${month}/${day} ${hours}:${minutes}`
        // 日期对象的一个储存
        yyear.push(Y_m_d)
        // 存储在localStorage.years 中 
        localStorage.years = JSON.stringify(yyear)
        // 然后解析 
        yyear = JSON.parse(localStorage.years)
        console.log(localStorage.years)
}
datefunction()
```
上边的代码一直会创建一个新的时间对象，并将其转化字符传存储在本地中。之前存储的一直不在，我找了一晚上bug.最后终于发现local的用法有点问题。原来在使用local时，我们要先进行解析。先将内容一个解析(JSON.parse(localStorage.years)) 然后在进行储存。这样每次刷新就不会重置了。
``` javascript
// 创建一个数组用来保存localStorage中的数据
var yyear = []
// 先解析
yyear = JSON.parse(localStorage.years)
var datefunction = function() {
        var date = new Date();
        var year =  date.getFullYear()
        var month = date.getMonth() + 1
        var day = date.getDate()
        var hours = date.getHours()
        var minutes = date.getMinutes()
        var Y_m_d = `${year}/${month}/${day} ${hours}:${minutes}`
        // 日期对象的一个储存
        yyear.push(Y_m_d)
        // 存储在localStorage.years 中
        localStorage.years = JSON.stringify(yyear)
        // 然后解析

        console.log(localStorage.years)
}
datefunction()
```
当然了，所谓的Local就是一个对象，我们在使用它时对它的key进行改变，同时给该key赋值。最终进行保存
