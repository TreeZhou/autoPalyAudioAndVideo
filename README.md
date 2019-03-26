网页视频和音乐自动播放		


```
	<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>音乐视频自动播放</title>
  </head>
  <body>
    <audio id="audio" src="./resources/1.mp3" autoplay loop="loop"></audio>
    <video
      id="video"
      style="object-fit: fill;"
      x-webkit-airplay="true"
      playsinline="true"
      x5-video-player-type="h5"
      x5-video-player-fullscreen="true"
      width="100%"
      preload="auto"
      autoplay
      src="./resources/1.mp4"
    ></video>
  </body>
  <script>
   // 各个方案的执行脚本

  </script>
</html>
```

方案一：使用```WeixinJSBridge```
- ios可以自动播放音乐和视频
- 安卓中只能自动播放音乐
- 只支持微信浏览器
```
 function autoPlay(id) {
      var audio = document.getElementById(id);
      if (window.WeixinJSBridge) {
        WeixinJSBridge.invoke(
          "getNetworkType",
          {},
          function(e) {
            audio.play();
          },
          false
        );
      } else {
        document.addEventListener(
          "WeixinJSBridgeReady",
          function() {
            WeixinJSBridge.invoke("getNetworkType", {}, function(e) {
              audio.play();
            });
          },
          false
        );
      }
      audio.play();

      return false;
    }
    autoPlay("video");
```


方案二：微信的```wx.ready```接口
- ios可以自动播放音乐和视频
- 安卓中只能自动播放音乐
- 只支持微信浏览器,并且需要微信授权wx.config()
```
 wx.ready(function() {
       document.getElementById("video").play()
    });
```

方案三 document监听第一次点击事件
- ios和安卓都可以播放，但需要一次触发条件
- 支持所有浏览器
```
function oneEvnet() {
document.removeEventListener("click", oneEvnet, false);
var audio = document.getElementById("video");
audio.play();
}
document.addEventListener("click", oneEvnet, false);
```

总结：微信浏览器中安卓无法自动播放视频，除此以外，媒体文件可以在各大机型中实现自动播放

[GitHub案例](https://github.com/TreeZhou/autoPalyAudioAndVideo "GitHub")