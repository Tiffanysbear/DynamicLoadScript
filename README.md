# DynamicLoadScript

> 动态加载js代码，兼容IE8等不支持标签中async等情况，支持callback回调<br>
> 确保js执行之后，调用回调函数
> 代码如下：

```javascript
var loadScript = function (url, callback, opt) {
    var script = document.createElement('script');
    var opt = opt || {};
    script.type = 'text/javascript';
    if (opt.charset) {
        script.charset = opt.charset;
    }
    if (opt.id) {
        script.id = opt.id;
    }
    if (script.readyState) {
        script.onreadystatechange = function () {
            if (script.readyState === 'loaded' || script.readyState === 'complete') {
                script.onreadystatechange = null;
                callback();
            }
        };
    } else {
        script.onload = function () {
            callback();
        };
    }
    script.src = url;
    document.body.appendChild(script);
};
```
