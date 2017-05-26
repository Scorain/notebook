# 每日小结

> &copy; suny



### 2017-04-10


HTML 动态/静态 `NodeList` 和 `HTMLCollection`



**参考文献**

- [querySelectorAll 方法相比 getElementsBy 系列方法有什么区别？](https://www.zhihu.com/question/24702250)


---

### 2017-04-11


DOM事件的 `passive` 属性



**参考文献**

- [addEventListener](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener)

---

### 2017-04-13


web接口之 `FileReader` 对象

    有些需求需要将本地的文件导入到页面表单中，因此需要读取本地磁盘中文件的内容， FileReader 接口提供了此权限。

    getFileContent 方法是用 input[type=file] 元素读取文件内容的封装，
    fileInput 参数为 input[type=file] 元素， 
    callback 参数为读取完成后的回调，此回调有一个参数：读取结果字符串。
    
    ```
    function getFileContent(fileInput, callback) {
        if (fileInput.files && fileInput.files.length > 0 && fileInput.files[0].size > 0) {
            var file = fileInput.files[0];
            if (window.FileReader) {
                var reader = new FileReader();
                reader.onloadend = function (evt) {
                    if (evt.target.readyState == FileReader.DONE) {
                        callback(evt.target.result);
                    }
                };
                reader.readAsText(file);
            }
        }
    }
    ```



**参考文献**

- [FileReader](https://developer.mozilla.org/zh-CN/docs/Web/API/FileReader)


---

### 2017-04-14


CSS3 属性 `box-shadow`

```
selector {
    box-shadow: inset <offset-x> <offset-y> <blur-radius> <spread-radius> <color>, ...
}
```



**参考文献**

- [box-shadow](https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-shadow)

---


### 2017-04-17


前端实现0.5px细线

> 背景图片

> css3 缩放

> css3 线性渐变

> css3 阴影

> meta 页面缩放



**参考文献**

- [css3使用技巧：细线边框的3种不同的写法](http://www.daqianduan.com/5935.html)

- [纯CSS实现border的0.5px设置](http://www.zhangyunling.com/543.html)

---



### 2017-04-20


前端上报

> js报错   window.onerror

> 性能   window.prefermance

> 日志

> UI监控




**参考文献**

- [前端相关数据监控](http://www.alloyteam.com/2014/03/front-end-data-monitoring/)

- [如何做前端异常监控？](https://www.zhihu.com/question/29953354)

---




### 2017-04-28


给git仓库配置用户名和邮箱

> 用户名 `git config [--global] [--unset] user.name 'yourname'`

> 邮箱 `git config [--global] [--unset] user.email 'youremail'`




**参考文献**

- [同一客户端下使用多个git账号](http://www.jianshu.com/p/89cb26e5c3e8)

---




### 2017-05-23


through2:转换数据流的封装

```

const through2 = require('require2');
const toUpperCase = through2((dataIn, enc, cb) => {
    let dataOut = new Buffer(data.toString().toUpperCase());
    let error = null;
    cb(error, dataOut);
});
process.stdin.pipe(toUpperCase).pipe(process.stdout);

```

　　through2是nodejs中转换数据流的封装库。上例中 dataIn 是读入数据， dataOut是写出数据，error 是错误信息。


**参考文献**

- [Node.js之对象流（Stream）权威指南](https://futu.im/posts/2017-05-21-object-streams-in-nodejs/)

---



### 2017-05-25


IOS body绑定click事件的bug

> window，document，body 绑定click事件时，点击body不会触发




**参考文献**

- [IOS上给body绑定click事件的bug](http://yanhaijing.com/mobile/2015/08/27/click-bug-on-body-on-ios/)
- [微信内置浏览器不支持 onclick 如何解决？](https://www.zhihu.com/question/37536990)

---




### 2017-05-26


水平、垂直居中的实现

> table时代 `align` `valign`

> css时代 `标准文档流` `浮动布局` `定位布局`

> flex时代 `父容器` `子容器` `主轴` `交叉轴`




**参考文献**

- [一劳永逸的搞定 flex 布局](https://juejin.im/post/58e3a5a0a0bb9f0069fc16bb)
- [CSS Flexible Box Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout)

---