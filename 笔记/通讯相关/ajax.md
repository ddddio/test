# AJAX（不兼容IE6）

```javascript
    let xhr = new XMLHttpRequest(); //xhr.readyState==0
    xhr.open("post","1.php",true);  //xhr.readyState==1
    //第一个参数为提交方式 post,get
    //第二个参数为提交的地址
    //第三个参数为是否为异步 true为异步，false为同步（已被官方淘汰了，用户体验不行） 默认为true
    xhr.send("name='张三'")        //xhr.readyState==2
    //发送合适的请求头信息
    xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");  //post专属
    xhr.onload = function () { 
    // 请求结束后,在此处写处理代码  
    };
    //传递的参数为请求主体 如果是get请求头 那么需要将xhr.send()传递null
    //...... 接收头 xhr.readyState==3
    //...... 接受体 xhr.readyState==4  无论是否成功xhr.readyState都会为4，具体的判断就交给xhr.status了
    xhr.onreadystatechange=function(){
        if(xhr.readyState==4)alert("end");
        alert("斯帕拉西~death");
    }
    //当加载到onreadystatechange方法时，xhr.readyState每一次修改时都会调用该方法，可以用来判断加载是否完成
```
status
- 1xx 信息（杂鱼信息）
- 2xx 成功
- 3xx 重定向（304除外，304也为成功）
  - 301 永久从定向
  - 302 暂时从定向（比如直接访问baidu.com会跳转到www.baidu.com）
  - 304 重定向到本地缓存的，在请求时会看该网站缓存在本地的最后修改时间文件和服务器里的最后修改时间（如果不相同还是请求，如果相同就本地的 一般静态网页这么做）
- 4xx 客户端出错（浏览器）
- 5xx 服务器出错
  - 500 服务器内部问题
  - 503 服务器超载（内存爆了）
- 6xx 拓展（自定义，往后的也是自定义）
