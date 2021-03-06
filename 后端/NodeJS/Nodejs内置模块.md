# fs 文件系统模块

fs模块是Node.js 官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。

导入 `fs` 模块

```javascript
const fs = require('fs');
```

## 读取文件

`fs.readFile()`方法，读取指定文件中的内容，语法格式：

```javascript
fs.readFile(path,[options],callback);
```

参数说明：

- 必选，字符串，表示文件的路径
- 可选，表示以什么编码格式来读取文件
- 必选，文件读取完成之后，通过回调函数来拿到读取的结果

使用：

```javascript
const fs = require('fs');

fs.readFile("./data.json", 'utf-8', (err, data) => {
  if (err) {
    return console.log(err);
  }
  console.log(data);
})
```



## 写入文件

`fs.writeFile()`方法，向指定文件中写入内容，语法：

```javascript
fs.writeFile(file,data,[options],callback)
```

参数说明：

- 必选，表示文件的存放路径
- 必选，表示要写入的内容
- 可选，表示以什么格式写入文件，默认 utf-8
- 必选，文件写入完成后的回调函数

使用：

```javascript
const fs = require('fs');

fs.writeFile("./data.txt", "123", (err) => {
  if (err) {
    return console.log(err);
  }
  console.log("写入成功");
})
```



## 练习

将cj.txt文件内的

```
aaa=99 bbb=55 ccc=84 ddd=69 eee=95 fff=84
```

转成

```
1 aaa:99
2 bbb:55
3 ccc:84
4 ddd:69
5 eee:95
6 fff:84
```

这种格式并保存在新文件cj-ok.txt中.



```javascript
const fs = require("fs");

fs.readFile("./cj.txt", "utf-8", (err, data) => {
  if (err) {
    return console.log(err);
  }

  let dealedData = "";
  let dealData = [];
  let count = 1;

  dealData = data.split(" ");
  dealData.map((e) => {
    e = e.replace(/=/, ":");
    dealedData += count + " " + e + "\n";
    count += 1;
  });

  fs.writeFile("./cj-ok.txt", dealedData, (err) => {
    if (err) {
      return console.log(err);
    }
    console.log("完成");
  });
});
```



## 路径动态拼接

在使用fs 模块操作文件时，如果提供的操作路径是以`./`或`../`开头的相对路径时，很容易出现路径动态拼接错误的问题。

原因:代码在运行的时候，**会以执行node命令时所处的目录**，动态拼接出被操作文件的完整路径。

解决方案:在使用fs模块操作文件时，直接提供完整的路径，不要提供`./`或`../`开头的相对路径，从而防止路径动态拼接的问题.

```javascript
const fs = require("fs");
// __dirname 表示当前文件所处的路径
fs.readFile(__dirname + "/data.txt", "utf-8", (err, data) => {
  if (err) {
    console.log(err);
  }
  console.log(data);
});
```



# path 路径模块

path模块是Node.js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。

导入 path 模块

```javascript
const path = require('path');
```



## 路径拼接

`path.join()`，将多个路径片段拼接成一个完整的路径字符串

```javascript
path.join([...paths]);
```

- ...paths 路径片段的序列

使用

```javascript
const path = require("path");

const pathStr = path.join("/a", "/b/b", "../", "./d", "e");
const pathStr2 = path.join(__dirname + "./1.txt");

console.log(pathStr);
console.log(pathStr2);

```

 

## 获取路径中的文件名

`path.basename()`，从路径字符串中将文件名解析出来

```javascript
path.basename(path,[ext]);
```

- path 必选 ， 表示一个路径的字符串
- ext 可选，表示文件扩展名

使用：

```javascript
const path = require("path");
const { PassThrough } = require("stream");

const fsPath = "a/b/c/d/index.html";

console.log(path.basename(fsPath));  // index.html
console.log(path.basename(fsPath, ".html"));	// index

```

# Http 模块

http模块是Node.js官方提供的、用来创建web服务器的模块。通过http模块提供的`http.createServer()`方法，就能方便的把一台普通的电脑， 变成一台Web服务器，从而对外提供Web资源服务。

## 创建 web 服务器

1. 导入 http 模块
2. 创建 web 服务器实例
3. 为服务器绑定 request 事件，监听客户端的请求

```javascript
const http = require("http");

const server = http.createServer();

const http = require("http");

const server = http.createServer();

server.on("request", function (req, res) {
  console.log("对于" + req.url + "的" + req.method + "请求");
  res.end(
    JSON.stringify({
      code: 200,
      data: "success!",
    })
  );
});

server.listen(8080, function () {
  console.log("127.0.0.1:8080");
});


server.listen(8080, function () {
  console.log("127.0.0.1:8080");
});

```



### req

只要服务器接收到了客户端的请求，就会调用通过`server.on()`为服务器绑定的 request事件处理函数。

如果想在事件处理函数中，访问与客户端相关的数据或属性，可以使用如下的方式:

```javascript
server.on("request", function (req, res) {
  console.log("对于" + req.url + "的" + req.method + "请求");
});
```



### res

在服务器的request事件处理函数中，如果想访问与服务器相关的数据或属性，可以使用如下的方式:

```javascript
server.on("request", function (req, res) {
  res.end(
    JSON.stringify({
      code: 200,
      data: "success!",
    })
  );
});
```

针对中文乱码问题，设置响应头编码格式;

```javascript
res.setHeader("Content-Type", "text/html;charset=utf-8");
```







