# 动画

1. [transition](#transition)
2. [animation](#animation)
3. [JavaScript 动画](#JavaScript-动画)

## transition
```CSS
  /* 20*20的红色区域 鼠标移入后先宽度增加后高度增加，移出后先宽度减少再高度减少 */
  .tran{ height:20px; width:20px; background:red;} 
  .tran:hover{ height: 100px; width: 100px; } 
  .tran{-webkit-transition: width 1s, height 1s 1s;}
```
transition 属性是一个简写属性，用于设置四个过渡属性：

|值|默认值|描述|
|-|-|-|
|transition-property|all|规定设置过渡效果的 CSS 属性的名称。|
|transition-duration|0|规定完成过渡效果需要多少秒或毫秒。|
|transition-timing-function|ease|规定速度效果的速度曲线。|
|transition-delay|定义过渡效果何时开始。|0|

## animation
```CSS
  /* 100*100的红色区域 红黄蓝绿循环渐变 */
.anim{
  width:100px;
  height:100px;
  background:red;
  -webkit-animation:myanim 5s linear 2s infinite alternate;
}
@-webkit-keyframes myanim{
  0%   {background: red; left:0px; top:0px;}
  25%  {background: yellow; left:200px; top:0px;}
  50%  {background: blue; left:200px; top:200px;}
  75%  {background: green; left:0px; top:200px;}
  100% {background: red; left:0px; top:0px;}
}
```
@keyframes 规定动画。  
animation 是所有动画属性的简写属性，除了 animation-play-state 与 animation-fill-mode属性。

|属性|默认值 |描述|
|-|- |-|
|animation-name| none|规定 @keyframes 动画的名称。|
|animation-duration| 0|规定动画完成一个周期所花费的秒或毫秒|
|animation-timing-function|ease |规定动画的速度曲线。|
|animation-delay|0|规定动画何时开始。|
|animation-iteration-count| 1|规定动画被播放的次数。|
|animation-direction| normal|规定动画是否在下一周期逆向地播放。|
|animation-play-state| running|规定动画是否正在运行或暂停。|
|animation-fill-mode| |规定对象动画时间之外的状态。|

## JavaScript 动画
| |CSS |JavaScript|
|-|- |-|
|优点| 浏览器可以对动画进行优化；能够使用硬件加速|控制能力强；动画内容更为丰富，不存在兼容性问题|
|缺点| 运行过程控制较弱,无法附加事件绑定回调函数；复杂动画代码冗长；兼容性问题|可能出现线程阻塞从而造成丢帧；代码的复杂度高|
CSS动画流畅的原因
>渲染线程分为main thread(主线程)和compositor thread(合成器线程)。
>如果CSS动画只是改变transform和opacity，这时整个CSS动画得以在compositor thread完成（而JavaScript动画则会在main thread执行，然后触发compositor进行下一步操作）
>在JavaScript执行一些昂贵的任务时，main thread繁忙，CSS动画由于使用了compositor thread可以保持流畅

CSS动画比JS流畅的前提：
>JS在执行一些昂贵的任务
>同时CSS动画不触发layout或paint