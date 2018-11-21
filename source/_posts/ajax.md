---
title: ajax
date: 2018-11-19 17:25:20
tags:
---

```javascript
var xhr = new XMLHttpRequest()
xhr.open('GET','/hello2.json',true)
xhr.send()
xhr.addEventListener('load',function(){
    console.log(xhr.status)
    if(xhr.status >= 200 && xhr.status < 300 || xhr.status === 304){
       var data = xhr.responseText
       console.log(data)
    }else{
        console.log('error')
    }
})
```

