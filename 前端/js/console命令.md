console

`console`对象是 JavaScript 的原生对象，可以输出各种信息到控制台。

## 1. console 对象的静态方法

### 1. 1 console.log()，console.info()，console.debug()

#### 1.1.1 console.log() - 用于在控制台输出信息

> - 可以接受一个或多个参数，将它们连接起来输出
>
> > ```js
> > console.log('Hello World')
> > // Hello World
> > console.log('a', 'b', 'c')
> > // a b c
> > ```
>
> - `console.log`方法会自动在每次输出的结尾，添加换行符
>
> - 格式化字符串
>
> | 占位符 | 参数类型                                        |      |
> | ------ | ----------------------------------------------- | ---- |
> | %s     | 字符串                                          |      |
> | %d     | 整数                                            |      |
> | %i     | 整数                                            |      |
> | %f     | 浮点数                                          |      |
> | %o     | 对象的链接                                      |      |
> | %c     | 对输出的字符串使用css样式，样式由第二个参数指定 |      |

#### 1.1.2 console.info()

`console.info`是`console.log`方法的别名，用法完全一样。

#### 1.1.3 `console.debug`

`console.debug`方法与`console.log`方法类似，会在控制台输出调试信息。但是，默认情况下，`console.debug`输出的信息不会显示，只有在打开显示级别在`verbose`的情况下，才会显示。

### 1.2 console.warn()，console.error()

`warn`方法和`error`方法也是在控制台输出信息，它们与`log`方法的不同之处在于，`warn`方法输出信息时，在最前面加一个黄色三角，表示警告, 背景色也是黄色；`error`方法输出信息时，在最前面加一个红色的叉，表示出错, 背景色红色。

### 1.3 console.table()

- console.table()可以用来查看对象的内容。该方法会将对象的属性以表格的形式打印出来。

- `table()`的第二个参数是可选的，你可传入一个字符串数组，来指定想显示的属性。

### 1.4 console.count()

- 用于计数，输出它被调用了多少次;

- 可以接受一个字符串作为参数，作为标签，对执行次数进行分类。

### console.dir()，console.dirxml()

- `dir`方法用来对一个对象进行检查（inspect），并以易于阅读和打印的格式显示。

- 该方法对于输出 DOM 对象非常有用，因为会显示 DOM 对象的所有属性。

- `dirxml`方法主要用于以目录树的形式，显示 DOM 节点。

### 1.5 `console.assert()`

`console.assert()`接受两个参数，如果第一个参数的结果为`false`，则该方法会将第二个参数输出到控制台。

下面的代码会判断list元素的子节点数目是否超过500，如果超过则打印一条错误消息：

```
console.assert(list.childNodes.length < 500, "Node count is > 500");
```

### 1.6 console.time()，console.timeEnd()

- 用于计时，可以算出一个操作所花费的准确时间。

```js
console.time('Array initialize');

var array= new Array(1000000);
for (var i = array.length - 1; i >= 0; i--) {
  array[i] = new Object();
};

console.timeEnd('Array initialize');
// Array initialize: 1914.481ms
```

### 1.7 console.group()，console.groupEnd()，console.groupCollapsed()

group命令对相关的输出进行分组。`group`方法只接受一个字符串参数，表示分组的名称。控制台会把接下来所有的输出组合输出，调用`groupEnd()`可以结束当前分组.

```js
var user = "jsmith", authenticated = false;
console.group("Authentication phase");
console.log("Authenticating user '%s'", user);
// authentication code here...
if (!authenticated) {
    console.log("User '%s' not authenticated.", user)
}
console.groupEnd();
```

日志分组是可以相互嵌套的，当分组信息较多的时候比较有用。

```js
var user = "jsmith", authenticated = true, authorized = true;
// Top-level group
console.group("Authenticating user '%s'", user);
if (authenticated) {
    console.log("User '%s' was authenticated", user);
    // Start nested group
    console.group("Authorizing user '%s'", user);
    if (authorized) {
        console.log("User '%s' was authorized.", user);
    }
    // End nested group
    console.groupEnd();
}
// End top-level group
console.groupEnd();
console.log("A group-less log trace.");
```

`console.groupCollapsed`方法与`console.group`方法很类似，唯一的区别是该组的内容，在第一次显示时是收起的（collapsed），而不是展开的。

```js
console.groupCollapsed('Fetching Data');

console.log('Request Sent');
console.error('Error: Server not responding (500)');

console.groupEnd();
```

### console.trace()，console.clear() 

`console.trace`方法显示当前执行的代码在堆栈中的调用路径。

```js
console.trace()
// console.trace()
//   (anonymous function)
//   InjectedScript._evaluateOn
//   InjectedScript._evaluateAndWrap
//   InjectedScript.evaluate
```

`console.clear`方法用于清除当前控制台的所有输出，将光标回置到第一行。如果用户选中了控制台的“Preserve log”选项，`console.clear`方法将不起作用。

## 2. 控制台命令行API

### 2.1 debugger 语句

作用是设置断点。如果有正在运行的除错工具，程序运行到`debugger`语句时会自动停下。如果没有除错工具，`debugger`语句不会产生任何结果，JavaScript 引擎自动跳过这一句。

Chrome 浏览器中，当代码运行到`debugger`语句时，就会暂停运行，自动打开脚本源码界面。

**参考链接**

[ChromeDevTools](https://leeon.gitbooks.io/devtools/content/learn_basic/using_console.html)

[console 对象与控制台 - 阮一峰](https://www.bookstack.cn/read/javascript-tutorial/docs-features-console.md)



