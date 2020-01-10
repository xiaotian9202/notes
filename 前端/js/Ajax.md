# Ajax

## 运行原理

Ajax相当于浏览器发送请求与接受响应的代理人，以实现在不影响用户浏览页面的情况下，局部更新页面数据，从而提高用户体验。

## Ajax的实现步骤

### 1. 创建Ajax对象

```js
var xhr = new XMLHttpRequest();
```

### 2. 告诉请求地址以及请求方式

```js
xhr.open('GET', 'http://www.example.com');
```

### 3. 发送请求

```js
xhr.send();
```

### 4. 服务端给客户端的响应数据格式

服务器在大多数情况下会以JSON对象作为响应数据的格式。当客户端拿到数据后，需要将JSON数据和HTML字符串进行拼接，然后将拼接后的结果展示在页面中。

在http请求与响应的过程中，无论是请求参数还是响应内容，如果是对象类型，最终都会被转换为对象字符串进行传输。

```js
JSON.parse()  // 将json字符串转换为json对象
```

### 5.  请求参数传递

- GET请求方式

```js
xhr.opne('get', 'http://www.example.com?name=zhangsan&age=20');
```

- POST请求方式

```js
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
xhr.send('name=zhangsan&age=20');
```





