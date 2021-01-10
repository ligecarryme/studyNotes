### 简介

AJAX 包括以下几个步骤。

1. 创建 XMLHttpRequest 实例
2. 发出 HTTP 请求
3. 接收服务器传回的数据
4. 更新网页数据

```js
var xhr = new XMLHttpRequest();

xhr.onreadystatechange = function(){
  // 通信成功时，状态值为4
  if (xhr.readyState === 4){
    if (xhr.status === 200){
      console.log(xhr.responseText);
    } else {
      console.error(xhr.statusText);
    }
  }
};

xhr.onerror = function (e) {
  console.error(xhr.statusText);
};

xhr.open('GET', '/endpoint', true);
xhr.send(null);

//封装成Promise
var myNewAjax=function(url){
	return new Promise(function(resolve,reject){
		var xhr = new XMLHttpRequest();
        xhr.open('get',url);
        xhr.send(data);
        xhr.onreadystatechange=function(){
		if(xhr.status==200&&readyState==4){
            var json=JSON.parse(xhr.responseText);
            resolve(json)
        }else if(xhr.readyState==4&&xhr.status!=200){
                reject('error');
        	}
		}
	})
}
```

1. 使用`open()`方法指定建立 HTTP 连接的一些细节。第三个参数`true`，表示请求是异步的。
2. 指定回调函数，监听通信状态（`readyState`属性）的变化。一旦`XMLHttpRequest`实例的状态发生变化，就会调用监听函数`handleStateChange`。
3. 最后使用`send()`方法，实际发出请求。`send()`的参数为`null`，表示发送请求的时候，不带有数据体。如果发送的是 POST 请求，这里就需要指定数据体。

### 实例属性

#### XMLHttpRequest.readyState

`XMLHttpRequest.readyState` 返回一个整数，表示实例对象的当前状态。该属性只读。

- 0，表示 XMLHttpRequest 实例已经生成，但是实例的`open()`方法还没有被调用。
- 1，表示`open()`方法已经调用，但是实例的`send()`方法还没有调用，仍然可以使用实例的`setRequestHeader()`方法，设定 HTTP 请求的头信息。
- 2，表示实例的`send()`方法已经调用，并且服务器返回的头信息和状态码已经收到。
- 3，表示正在接收服务器传来的数据体（body 部分）。这时，如果实例的`responseType`属性等于`text`或者空字符串，`responseText`属性就会包含已经收到的部分信息。
- 4，表示服务器返回的数据已经完全接收，或者本次接收已经失败。

#### XMLHttpRequest.onreadystatechange

`XMLHttpRequest.onreadystatechange`属性指向一个监听函数。`readystatechange`事件发生时（实例的`readyState`属性变化），就会执行这个属性。

…

### XMLHttpRequest 的实例方法

#### XMLHttpRequest.open()

`XMLHttpRequest.open()`方法用于指定 HTTP 请求的参数，或者说初始化 XMLHttpRequest 实例对象。接受五个参数。

```c
void open(
   string method,
   string url,
   optional boolean async,
   optional string user,
   optional string password
);
```

