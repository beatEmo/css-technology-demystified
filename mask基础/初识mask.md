## 初识 mask？

> **mask 译为遮罩**
>
> mask 属性允许使用者通过 ***遮罩或者裁切*** 特定区域的图片的方式来 ***隐藏*** 一个元素的部分或者全部 ***可见区域***
>
> - mask的语法和background基本一致


#### 一个简单的背景图（mask版）

> **mask 允许使用者通过遮罩或者裁切特定区域的图片的方式来隐藏一个元素的部分或者全部可见区域**
>
> ***元素的内容**与 mask 生成的渐变的透明重叠部分，将会变得**透明***

```
.mask {  
      background: url("./img/1.jpg") no-repeat center / 100%;
+     mask: linear-gradient(90deg, transparent, #000);
+     -webkit-mask: linear-gradient(90deg, transparent, #000);
    }
```

![1699282807477](image/初识mask/1699282807477.png)

![1699282891832](image/初识mask/1699282891832.png)

#### 技巧一：使用 mask 进行内容裁切

```
.mask {
      width: 610px;
      height: 280px;
      background: url("./img/1.jpg") no-repeat center / 100%;
      -webkit-mask: linear-gradient(135deg, transparent 15px, deeppink 0) top
          left,
        linear-gradient(-135deg, transparent 15px, deeppink 0) top right,
        linear-gradient(-45deg, transparent 15px, deeppink 0) bottom right,
        linear-gradient(45deg, transparent 15px, deeppink 0) bottom left;
      -webkit-mask-size: 50.5% 50.5%;
      -webkit-mask-repeat: no-repeat;
    }
```

![1699283848214](image/初识mask/1699283848214.png)

#### 实现内切圆角渐变色按钮

```
.mask-inset-circle {
      background: linear-gradient(45deg, #2179f5, #e91e63);
      -webkit-mask: radial-gradient(
          circle at 100% 100%,
          transparent 12px,
          #2179f5 13px
        ),
        radial-gradient(circle at 0 0, transparent 12px, #2179f5 13px),
        radial-gradient(circle at 100% 0, transparent 12px, #2179f5 13px),
        radial-gradient(circle at 0 100%, transparent 12px, #2179f5 13px);
      -webkit-mask-repeat: no-repeat;
      -webkit-mask-position: right bottom, left top, right top, left bottom;
      -webkit-mask-size: 70% 70%;
    }
```

![1699285735476](image/初识mask/1699285735476.png)

![1699285752110](image/初识mask/1699285752110.png)

#### 技巧二：巧用 mask 实现渐变消失布局

```
ul {
      width: 300px;
      display: flex;
      flex-wrap: nowrap;
      overflow-x: scroll;
      -webkit-mask: linear-gradient(90deg, red 60%, transparent);
    }
```

![1699286076022](image/初识mask/1699286076022.png)

#### 技巧三：巧用 mask 实现融合效果

> 预留了从 `40%` 到 `60%`的从不透明到透明的过渡

```
    div {
      background: url("./img/1.jpg");
      position: relative;
    }
    div::after {
      content: "";
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      background: url("./img/2.jpg");
      -webkit-mask: linear-gradient(45deg, #000 40%, transparent 60%);
    }
```

![1699287383636](image/初识mask/1699287383636.png)

#### 技巧四：使用 mask 实现内容切换效果

> 切记： **尝试去理解这个属性被设计出来的目的，以及想要解决的问题** 。
>
> Mask 的核心就是遮罩，遮挡住元素的内容（可以是部分挡住，可以是逐渐消失，甚至是可以分块挡住），显示出其元素背后的内容。
