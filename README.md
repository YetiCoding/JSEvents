# JSEvents
---------------
## 事件流
----------
### 事件冒泡

事件由子节点向父节点逐层传递

div触发click事件传递过程:
```flow

div--->body---->html---->Document

```

### 事件捕获

与事件冒泡正相反 由父节点向子节点传递

div触发click事件传递过程:
```flow

Document--->html---->body---->div

```

## 事件处理程序

事件监听器
以‘on’开头，click事件 ---> onclick ，load事件 ---> onload

指定方式:

**方式一:**

_HTML绑定事件处理_

 ``` html

    <input type = "button" value = "click" onclick="alert('clicked')" />

 ```
此方式会创建一个封装着元素属性值得函数。这个函数有一个局部变量 ***event***

``` html

    <input type = "button" value = "click" onclick="alert(event.type)" />

```

this等于事件的目标元素

``` html

    <input type = "button" value = "click" onclick="alert(this.value)" />

    <!-- value ==> click -->
```

作用域扩展，可访问document及该元素本身

函数内部实现方式:
``` javascript

    function(){
        with(document){
            with(this){
                //元素属性
            }
        }
    }

```

案例:
``` html
<form method="get">
    <input type="text" name="username" value="">
    <input type="button" value="Click" onclick="alert(username.value)">
</form>
```

缺点:
  ***时差问题，各浏览器处理事件上存在差异***

**方式二:**

_DOM0_

```javascript
    //添加
    var btn = document.getElementById("btn");
    btn.onclick = function(){
        alert(this.id); //btn
    }
    //删除
    btn.onclick = null;

```

**方式三**

_DOM2_

```javascript

    var btn = getElementById("btn");

    //添加 参数1:事件 参数2 回调函数  参数3 boolean true:事件捕获时触发  false:事件冒泡时触发
    btn.addEventListener("click",function(){
        //do something
    },false);


    //删除
    btn.removeEventListener("click",function(){},false);

```

**删除监听器时需要删除和添加时相同的回调函数才有效**

``` javascript

    //无效的删除
    btn.addEventListener("click",function(){
        alert(1);
    },false);

    btn.removeEventListener("click",function(){
        alert(1);
    },false);

    //有效的删除
    var handler = function(){
        //do something
    }

    btn.addEventListener("click",handler,false);
    btn.removeEventListener("click",handler,false);

```

**IE**

``` javascript

    attachEvent();

    detachEvent();

```
***事件处理程序会在全局作用域中运行***

``` javascript

    var btn = document.getElementById("btn");
    btn.attachEvent("onclick",function(){  //区别 onclick
        alert(this === window);   //true
    },false)

```

## 事件对象
------------
###DOM Event

**每次触发都会向回调函数传人event对象**
``` javascript

    btn.addEventListener("click",function(event){

        alert(event.type);

    },false)

```
***currentTarget***
当前对象

***target***
源对象

阻止默认特定事件默认行为: *event.preventDefault()*  **(只有cancelable为true时)**

## 事件类型

###UI事件

    **load事件**

    触发条件：
        当页面完全加载完成后(所有图片\Javascript文件\CSS文件等外部资源)

###焦点事件

###鼠标事件

###滚轮事件

###文本事件

###键盘事件

###合成事件

###变动事件

## 内存和性能

## 模拟事件