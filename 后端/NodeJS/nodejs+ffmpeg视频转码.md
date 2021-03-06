使用 ffmpeg 进行视频转码

<!-- more -->

首先电脑中要先安装 ffmpeg
[下载](http://ffmpeg.org/download.html#build-windows)安装
配置环境
![](nodejs+ffmpeg视频转码.assets/w4h3P1.jpg)
检查安装
![](nodejs+ffmpeg视频转码.assets/w4hoR0.jpg)
至此,ffmpeg 就安装完成了.
接下来要在 node 中使用,需要下载[fluent-ffmpeg](https://www.npmjs.com/package/fluent-ffmpeg)

```language
npm install fluent-ffmpeg
```

转码例子:
[Node 爬取字母站视频](https://k8963.github.io/2020/09/13/Node%E7%88%AC%E5%8F%96%E5%AD%97%E6%AF%8D%E7%AB%99%E8%A7%86%E9%A2%91/)使用这个例子所下载的视频进行转码,将 flv 格式的视频转为 mp3

```javascript
function transcode(info) {
  // 文件路径 + flv 原格式
  var command = ffmpeg("media/" + info.name + ".flv")
    .on("start", function (commandLine) {
      console.log("开始" + commandLine);
    })
    .on("progress", function (progress) {
      console.log("进度" + progress.percent + "%");
    })
    .on("end", function () {
      console.log("完成");
    })
    //文件路径 + mp3要转码的格式
    .save("media/" + info.name + ".mp4");
}
let videoInfo = {
  url: "https://www.bilibili.com/video/BV1rs411p7c8?from=search&seid=16766879598476832298",
  name: "feeling you",
};
// 调用函数
transcode(videoInfo);
```

执行结果
![](nodejs+ffmpeg视频转码.assets/w451c6.jpg)

在文件中试听转码后的文件,无问题
![](nodejs+ffmpeg视频转码.assets/w4IrGR.jpg)

当要转成 mp4 ,修改此处代码

```javascript
.save('media/' + info.name + '.mp4');
```

执行 js 文件,顺利转码.