## 内存泄漏

[ref.](http://www.cnblogs.com/sprying/archive/2013/05/31/3109517.html)

内存泄漏是指一块被分配的内存既没有使用，又没有被回收的，直到浏览器进程结束。

## 内存泄漏的情况

1, 当页面中元素被移除或替换时，若元素绑定的事件仍没被移除，在IE中不会作出恰当处理，此时要先手工移除事件，不然会存在内存泄露。

```js
<div id="myDiv">
  <input type="button" value="Click me" id="myBtn">
</div>
<script type="text/javascript">
  var btn = document.getElementById("myBtn");
  btn.onclick = function(){
    document.getElementById("myDiv").innerHTML = "Processing...";
  }
</script> 
```
改成 
```js
<div id="myDiv">
    <input type="button" value="Click me" id="myBtn">
</div>
<script type="text/javascript">
    var btn = document.getElementById("myBtn");
    btn.onclick = function(){
        btn.onclick = null;
        document.getElementById("myDiv").innerHTML = "Processing...";
    }
</script>
```
或改成事件委托
```
<div id="myDiv">
    <input type="button" value="Click me" id="myBtn">
</div>
<script type="text/javascript">
    document.onclick = function(event){
        event = event || window.event;
        if(event.target.id == "myBtn"){
            document.getElementById("myDiv").innerHTML = "Processing...";
        }
    }
</script>
```

2, 闭包问题引起的内容泄漏













