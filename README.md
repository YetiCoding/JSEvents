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

## 事件对象

## 事件类型

## 内存和性能

## 模拟事件