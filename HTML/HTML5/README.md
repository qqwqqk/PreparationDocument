# HTML5

## 什么是HTML5
1. 简介
HTML5 技术结合了 HTML4.01 的相关标准并革新，符合现代网络发展要求，在 2008 年正式发布。HTML5 由不同的技术构成，其在互联网中得到了非常广泛的应用，提供更多增强网络应用的标准机。  
与传统的技术相比，HTML5 的语法特征更加明显，并且结合了 SVG 的内容。这些内容在网页中使用可以更加便捷地处理多媒体内容，而且 HTML5中还结合了其他元素，对原有的功能进行调整和修改，进行标准化工作。HTML5 在 2012 年已形成了稳定的版本。

2. HTML5建立的一些规则
新特性应该基于 HTML、CSS、DOM 以及 JavaScript  
减少对外部插件的需求（比如 Flash）  
更优秀的错误处理  
更多取代脚本的标记  
HTML5 应该独立于设备  
开发进程应对公众透明  

3. HTML5 中的一些有趣的新特性：
用于绘画的 canvas 元素  
用于媒介回放的 video 和 audio 元素  
对本地离线存储的更好的支持  
新的特殊内容元素，比如 article、footer、header、nav、section  
新的表单控件，比如 calendar、date、time、email、url、search  

## HTML5 视频
1. video 标签的属性

|属性||值||描述|
|-|-|-|
|autoplay|autoplay|如果出现该属性，则视频在就绪后马上播放。|
|controls|controls|如果出现该属性，则向用户显示控件，比如播放按钮。|
|height|pixels|设置视频播放器的高度。|
|loop|loop|如果出现该属性，则当媒介文件完成播放后再次开始播放。|
|preload|preload|如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。|
|src|url|要播放的视频的 URL。|
|width|pixels|设置视频播放器的宽度。|

2. HTML5 video - 方法、属性以及事件

|方法|属性|事件|
|-|-|-|
|play()|currentSrc|play|
|pause()|currentTime|pause|
|load()|videoWidth|progress|
|canPlayType|videoHeight|error|
| |duration|timeupdate|
| |ended|ended|
| |error|abort|
| |paused|empty|
| |muted|emptied|
| |seeking|waiting|
| |volume|loadedmetadata|
| |height| |
| |width| |

## HTML5 音频

|属性|值|描述|
|-|-|-|
|autoplay|autoplay|如果出现该属性，则音频在就绪后马上播放。|
|controls|controls|如果出现该属性，则向用户显示控件，比如播放按钮。|
|loop|loop|如果出现该属性，则每当音频结束时重新开始播放。|
|preload|preload|如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。|
|src|url|要播放的音频的 URL。|

## HTML5 拖放

|方法|描述|
|-|-|
|dragstart|事件主体是被拖放元素，在开始拖放被拖放元素时触。|
|darg|事件主体是被拖放元素，在正在拖放被拖放元素时触发。|
|dragenter|事件主体是目标元素，在被拖放元素进入某元素时触发。|
|dragover|事件主体是目标元素，在被拖放在某元素内移动时触发。|
|dragleave|事件主体是目标元素，在被拖放元素移出目标元素是触发。|
|drop|事件主体是目标元素，在目标元素完全接受被拖放元素时触发。|
|dragend|事件主体是被拖放元素，在整个拖放操作结束时触发。|

## HTML5 画布
1. 什么是 Canvas？
HTML5 的 canvas 元素使用 JavaScript 在网页上绘制图像。
画布是一个矩形区域，您可以控制其每一像素。
canvas 拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。

2. 绘制圆形
```JavaScript
var sketchpad = document.getElementById('canvas');
var layer = sketchpad.getContext('2d');

// x,y-圆心; start-起始角度; end-结束角度; color-颜色; type-类型('fill'和'stroke')
var draw = function(x, y, r, start, end, color, type) {
    var unit = Math.PI / 180;
    layer.beginPath();
    layer.arc(x, y, r, start * unit, end * unit);
    layer[type + 'Style'] = color;
    layer.closePath();
    layer[type]();
}

draw(100,75,50,0,360,'red','fill');
```

3. 绘制三角形
```JavaScript
var sketchpad = document.getElementById('canvas');
var layer = sketchpad.getContext('2d');

// xi,yi-顶点坐标; color-颜色; type-类型('fill'和'stroke')
var draw = function(x1, y1, x2, y2, x3, y3, color, type) {
    layer.beginPath();
    layer.moveTo(x1, y1);
    layer.lineTo(x2, y2);
    layer.lineTo(x3, y3);
    layer[type + 'Style'] = color;
    layer.closePath();
    layer[type]();
}

draw(50,50,175,50,150,'red','stroke');
```

## HTML5 SVG
1. 什么是 SVG
SVG 指可伸缩矢量图形 (Scalable Vector Graphics)
SVG 用于定义用于网络的基于矢量的图形
SVG 使用 XML 格式定义图形
SVG 图像在放大或改变尺寸的情况下其图形质量不会有损失
SVG 是万维网联盟的标准

2. SVG 的优势
SVG 图像可通过文本编辑器来创建和修改
SVG 图像可被搜索、索引、脚本化或压缩
SVG 是可伸缩的
SVG 图像可在任何的分辨率下被高质量地打印
SVG 可在图像质量不下降的情况下被放大

<svg xmlns="http://www.w3.org/2000/svg" version="1.1" height="190">
  <polygon points="100,10 40,180 190,60 10,60 160,180"
  style="fill:lime;stroke:purple;stroke-width:5;fill-rule:evenodd;" />
</svg>

```HTML
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" height="190">
  <polygon points="100,10 40,180 190,60 10,60 160,180"
  style="fill:lime;stroke:purple;stroke-width:5;fill-rule:evenodd;" />
</svg>
```

## HTML5 Canvas vs SVG
Canvas 和 SVG 都可以在浏览器中创建图形，但是它们在根本上是不同的。

1. Canvas
Canvas 通过 JavaScript 来绘制 2D 图形。
Canvas 是逐像素进行渲染的。
在 canvas 中，一旦图形被绘制完成，它就不会继续得到浏览器的关注。如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。

2. SVG
SVG 是一种使用 XML 描述 2D 图形的语言。
SVG 基于 XML，这意味着 SVG DOM 中的每个元素都是可用的。您可以为某个元素附加 JavaScript 事件处理器。
在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。

3. Canvas 与 SVG 的比较

|Canvas|SVG|
|-|-|
|依赖分辨率|不依赖分辨率|
|不支持事件处理器|支持事件处理器|
|弱的文本渲染能力|最适合带有大型渲染区域的应用程序(比如谷歌地图)|
|能够以 .png 或 .jpg 格式保存结果图像|复杂度高会减慢渲染速度(任何过度使用 DOM 的应用都不快)|
|最适合图像密集型的游戏，其中的许多对象会被频繁重绘|不适合游戏应用|

## HTML5 地理定位
1. 定位用户的位置
HTML5 Geolocation API 用于获得用户的地理位置。
鉴于该特性可能侵犯用户的隐私，除非用户同意，否则用户位置信息是不可用的。

2. getCurrentPosition
getCurrentPosition()方法用来获得用户的位置。

|错误代码|描述|
|-|-|
|Permission denied | 用户不允许地理定位|
|Position unavailable | 无法获取当前位置|
|Timeout | 操作超时|

## HTML5 Web存储
1. HTML5 提供了两种在客户端存储数据的新方法：
localStorage - 没有时间限制的数据存储
sessionStorage - 针对一个 session 的数据存储

2. 与 cookie 的对比

| |cookie|sessionStorage|localStorage|
|-|-|-|-|
|生命周期|setMaxAge() (default：当前会话)|仅在当前会话下有效(同浏览器窗口)|生命周期永久|
|存储大小|4K左右|5M或更大|5M或更大|
|存储位置|浏览器端|浏览器端|浏览器端|
|与服务器通信|携带在HTTP头中|不参与服务器通信|不参与服务器通信|
|易用性|需自己封装API|可以使用原生接口|可以使用原生接口|
|应用场景|用户登录|页面传参|临时数据存储|

3. cookie 字段

|字段|描述|
|-|-|
|name | cookie的名称|
|value | cookie的值|
|domain | 可以访问此cookie的域名|
|path | 可以访问此cookie的页面路径|
|expires/Max-Age | 此cookie超时时间|
|size | 此cookie大小|
|http | cookie的httponly属性|
|secure | 设置是否只能通过https来传递此条cookie|

>顶级域名只能设置domain为顶级域名，不能设置为二级域名或者三级域名，否则cookie无法生成。
>二级域名能读取设置了domain为顶级域名或者自身的cookie，不能读取其他二级域名domain的cookie。所以要想cookie在多个二级域名中共享，需要设置domain为顶级域名，这样就可以在所有二级域名里面或者到这个cookie的值了。
>顶级域名只能获取到domain设置为顶级域名的cookie，其他domain设置为二级域名的无法获取。

## HTML5 应用程序缓存
1. 什么是应用程序缓存(Application Cache)?
HTML5 引入了应用程序缓存，这意味着 web 应用可进行缓存，并可在没有因特网连接时进行访问。
应用程序缓存为应用带来三个优势：
离线浏览 - 用户可在应用离线时使用它们
速度 - 已缓存资源加载得更快
减少服务器负载 - 浏览器将只从服务器下载更新过或更改过的资源。

2. Cache Manifest 基础
```HTML
!DOCTYPE HTML
html manifest="demo.appcache"
...
/html
```
启用应用程序缓存，需要在文档的 html 标签中包含 manifest 属性：
每个指定了 manifest 的页面在用户对其访问时都会被缓存。
如果未指定 manifest 属性,则页面不会被缓存(除非在 manifest 文件中直接指定了该页面)。
manifest 文件的建议的文件扩展名是：".appcache"。
>PS: manifest 文件需要配置正确的 MIME-type,即 "text/cache-manifest"。必须在 web 服务器上进行配置。

3. Manifest 文件
manifest 文件是简单的文本文件，它告知浏览器被缓存的内容(以及不缓存的内容)。
manifest 文件可分为三个部分：
CACHE MANIFEST - 在此标题下列出的文件将在首次下载后进行缓存
NETWORK - 在此标题下列出的文件需要与服务器的连接，且不会被缓存
FALLBACK - 在此标题下列出的文件规定当页面无法访问时的回退页面(比如 404 页面)

## HTML5 Web Workers
1. 什么是 Web Worker？
当在 HTML 页面中执行脚本时，页面的状态是不可响应的，直到脚本已完成。
Web Worker 是运行在后台的 JavaScript，独立于其他脚本，不会影响页面的性能。您可以继续做任何愿意做的事情：点击、选取内容等等，而此时 Web Worker 在后台运行。

2. DEMO
```JavaScript
// main.js
var w;
function startWorker(){
  // 检测Worker支持情况
  if(typeof(Worker)!=="undefined"){   
    if(typeof(w)=="undefined"){ w=new Worker("/example/html5/demo_workers.js"); }
    // 监听传回的参数
    w.onmessage = function (event) { document.getElementById("result").innerHTML=event.data; };
  } else {
    document.getElementById("result").innerHTML="Sorry, your browser does not support Web Workers...";
  }
}
function stopWorker(){ w.terminate(); }

//demo_workers.js
var i=0;
function timedCount(){
  i=i+1;
  //向main.js传回参数
  postMessage(i);       
  setTimeout("timedCount()",500);
}
timedCount();
```

3. 限制
由于 web worker 位于外部文件中，它们无法访问window 对象、document 对象 与 parent 对象。