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


