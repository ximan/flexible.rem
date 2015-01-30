# 移动端弹性布局（rem）解决方案

## 问题

* 设计稿宽度为640（iPhone 4为基准）、750（iPhone 6为基准），怎样合理布局？
* 不同设备、不同宽度（甚至是横屏），如何处理容器比例？宽度可以用百分比，高度呢？
* 同上，如何处理字号？所有设备都是相同字号？
* 设计师的1px边框，如何实现？

## 解决

    rem：相对长度单位。相对于根元素(即html元素)font-size计算值的倍数

* js获取网页宽度，计算`html`合适的字号，实现弹性模块、边距、字号等
* js动态计算viewport的initial-scale初始缩放值，实现1px边框

## 示例

![扫一扫](demo.png)
[DEMO链接](http://ximan.github.io/flexible.rem/)

## 用法

1. 把`<head>`里`<meta name="viewport">`删掉，在此位置加本js，建议对本js做`内敛处理`
2. js里默认设计稿宽度为`dd = 640`，请根据需求自行替换（代码有压缩，请搜索`640`）
3. `rem`=`px`/100。例如设计稿里`div`宽度`640px`、上下边距`20px`、边框`1px`、字号`24px`，应该写成：

        div{
            width:6.4rem;
            margin:.2rem 0;
            border:.01rem solid #000;
            font-size:.24rem;
        }

## bug

* PC端Chrome、Android端Chrome、UC：文字过多时（去掉demo中html注释），文字大小会默认加大24px（0.24rem变成36px；0.28rem变成38px）。解决方案：某一个外容器加高度（.text{height:200px}）
* PC端Chrome：设置设计稿宽度为750（iPhone 6，宽度375），默认rem为100，在iPhone 4、5、5S（宽度都是320，小于375）时，0.01rem（1px）的边框显示不出来。因为PC浏览器会自动忽略小数点后面所有数字。解决方案：直接写1px
* Android端自带浏览器：initial-scale小于1时，px单位并没有缩小（例如initial-scale=1或者0.5，font-size:12px永远一样大）。解决方案：改用rem做单位

## 注意

没有万能的办法，此方法也不是万能的。例如要求横竖屏时广告图片宽高都成比例放大缩小，这种设置`rem`的方法显然是不行的。所以需要横竖屏宽高都自适应，建议用宽度100%或者[响应式（宽高等比缩放）布局](http://ons.me/493.html)比较好。（不在乎横屏的除外）