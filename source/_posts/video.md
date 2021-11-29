---
title: video标签
date: 2020-08-05 10:20:48
index_img: https://qiniu.zhaoxinchuan.cn/h5/index.webp 
banner_img: https://qiniu.zhaoxinchuan.cn/bg/category.webp
tags: [html5]
categories: html5
---
## video标签
[菜鸟教程](https://www.runoob.com/tags/av-event-canplay.html)

[W3Cschool](https://www.w3school.com.cn/tags/tag_audio.asp)

 | 属性     | 值       | 说明                                                           |
 | -------- | -------- | -------------------------------------------------------------- |
 | autoplay | autoplay | 如果出现该属性，则视频在就绪后马上播放。                       |
 | controls | controls | 如果出现该属性，则向用户显示控件，比如播放按钮。               |
 | width    | pixels   | 设置视频播放器的宽度。                                         |
 | height   | pixels   | 设置视频播放器的高度。                                         |
 | loop     | loop     | 如果出现该属性，则当媒介文件完成播放后再次开始播放。           |
 | muted    | muted    | 规定视频的音频输出应该被静音。放                               |
 | poster   | URL      | 规定视频下载时显示的图像，或者在用户点击播放按钮前显示的图像。 |
 | preload  | preload  | 如果出现该属性，则视频在页面加载时进行加载，并预备播放。       |

如果使用 "autoplay"，则忽略该属性。
src | url | 	要播放的视频的 URL。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>video</title>
</head>
<body>
    <video src="./video/sp2.mp4" id="myvideo"></video>
    <script>
        var myvideo = document.getElementById("myvideo");
        myvideo.addEventListener("loadstart", () => {
            console.log("提示音频的元数据已加载：loadstart");
        });
        myvideo.addEventListener("durationchange", () => {
            console.log("提示视频的时长已改变：durationchange");
        });
        myvideo.addEventListener("loadedmetadata", () => {
            console.log("提示音频的元数据已加载：loadedmetadata");
        });
        myvideo.addEventListener("loadeddata", () => {
            console.log("提示当前帧的数据是可用的：loadeddata");
        });
        myvideo.addEventListener("progress", () => {
            console.log("提示视频正在下载中：progress");
        });
        myvideo.addEventListener("canplay", () => {
            console.log("提示该视频已准备好开始播放：canplay");
        });
        myvideo.addEventListener("canplaythrough", () => {
            console.log("提示视频能够不停顿地一直播放：canplaythrough");
        });
    </script>
</body>

</html>
```

```
// 结果
提示音频的元数据已加载：loadstart
video.html:20 提示视频的时长已改变：durationchange
video.html:23 提示音频的元数据已加载：loadedmetadata
video.html:29 提示视频正在下载中：progress
video.html:26 提示当前帧的数据是可用的：loadeddata
video.html:32 提示该视频已准备好开始播放：canplay
video.html:35 提示视频能够不停顿地一直播放：canplaythrough
```




