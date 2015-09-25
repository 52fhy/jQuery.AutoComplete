[jQuery.AutoComplete](http://work.jiani.info/jQuery.AutoComplete/)
=================
jQuery.AutoComplete是一个基于jQuery的自动补全插件。借助于jQuery优秀的跨浏览器特性，可以兼容Chrome/IE/Firefox/Opera/Safari等多种浏览器。

![ScreenShot](http://images.cnitblog.com/blog2015/663847/201504/251607339218146.jpg)

##特性一览：

* 支持补全列表的宽度设定。
* 支持补全列表的最大高度设定。
* 支持补全列表的行数限制。
* 支持补全列表的显示位置及方向的设定。
* 支持自定义匹配规则。
* 支持匹配文本的渲染。
* 支持自定义匹配文本的渲染样式。
* 支持补全列表的样式设定。
* 支持自定义补全列表项的创建。
* 支持多种数据源。
* 支持'json'和'xml'两种数据格式。
* 支持异步处理。
* 支持错误调试。
* 支持jQuery1.7.1+。

 
##一、如何使用：

   引入`jquery.autocomplete.js` 和 `jquery.autocomplete.css 文件到你的页面中。
   
##二、参数说明：

autocomplete的参数比较丰富。这里我不全部进行介绍。大家自行去看api文档。
```javascript
$("#tt").AutoComplete({
    'data': ['One', 'Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine', 'Ten',     'Eleven', 'Twelve']
});
```
data可以是数组，也可以是url，但url返回的数据必须是数组。

 
##三、示例：

###1、本地数据：
html代码：
```html
<input type="text" id="tt" value="" class="text" />
```
 
javascript代码：
```javascript
$(function(){
    $("#tt").AutoComplete({
        'data':['Cambodia', 'Cameroon', 'Canada', 'Cape-Verde', 'Cayman-Islands', 'Central-African-Republic', 'Chad', 'Chile', 'China', 'Colombia', 'Commonwealth', 'Comoros', 'Costa-Rica', "Cote-d'Ivoire", 'Croatia', 'Cuba', 'Cyprus', 'Czech-Republic'],
    });

})
```
注意data是有引号的。

 

###2、ajax请求：

html代码：
```html
<input type="text" id="company" value="" class="text" />
```
javascript代码：
```javascript
$(function(){
    $("#tt").AutoComplete({
        'data':'http://localhost/test/suggestCom',
    });
})
```

服务端返回数据格式：
```javascript
["\u5317\u4eac\u73b0\u4ee3","\u5317\u4eac\u57ce\u5efa\u96c6\u56e2\u6709\u9650\u8d23\u4efb\u516c\u53f8","\u5317\u4eac\u5efa\u5de5\u96c6\u56e2\u6709\u9650\u8d23\u4efb\u516c\u53f8","\u5317\u4eac\u9996\u90fd\u65c5\u6e38\u96c6\u56e2\u6709\u9650\u8d23\u4efb\u516c\u53f8","\u5317\u4eac\u533b\u836f\u96c6\u56e2\u6709\u9650\u8d23\u4efb\u516c\u53f8","\u5317\u4eac\u4e00\u8f7b\u63a7\u80a1\u6709\u9650\u8d23\u4efb\u516c\u53f8","\u5317\u4eac\u91d1\u9685\u96c6\u56e2\u6709\u9650\u8d23\u4efb\u516c\u53f8","\u5317\u4eac\u71d5\u4eac\u5564\u9152\u96c6\u56e2\u516c\u53f8","\u5317\u4eac\u5e02\u71c3\u6c14\u96c6\u56e2\u6709\u9650\u8d23\u4efb\u516c\u53f8","\u5317\u4eac\u4f4f\u603b\u96c6\u56e2\u6709\u9650\u8d23\u4efb\u516c\u53f8"]
```

服务端的代码：（以ThinkPHP示例）
```php
public function suggestCom(){
        $wd = $_GET['keyword'];
        $keywords = $wd;
    
        $company_model = M('Company');
    
        $res = $company_model->where("name like '%".$keywords."%' or abbr like '%".$keywords."%' ")->limit(10)->select();
        foreach($res as $v){
            $suggestions[]= $v['name'];
        }
    
        echo json_encode($suggestions);
    }
```
注意默认是GET过来的数据，名称是keyword，返回数据是和本地data一致的。


演示地址：http://autocomplete.jiani.info/demo/    
文档地址：http://autocomplete.jiani.info/doc/  

