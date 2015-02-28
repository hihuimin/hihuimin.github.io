---
layout: post
title: "使用Compass生成高清屏雪碧图"
---

如不清楚Compass生成雪碧图的同学可以先看看这个官方教程[Spriting with Compass](http://compass-style.org/help/tutorials/spriting/)，看完你或许会发现一个问题，它貌似不支持高清屏下雪碧图的使用。

由于现在主流手机均为高清屏，所以准备一套双倍图就够了，合成雪碧图使用时，background size/position 需要除以2，为此写了一个mixin来自定义生成雪碧图：

{% highlight sass %}
@import "compass/utilities/sprites";

@mixin sprite-background($map, $sprite) {
    height: ceil(image-height(sprite-file($map, $sprite)) / 2);
    width: ceil(image-width(sprite-file($map, $sprite)) / 2);

    $x: floor(nth(sprite-position($map, $sprite), 1) / 2);
    $y: floor(nth(sprite-position($map, $sprite), 2) / 2);

    background: sprite-url($map) no-repeat $x $y;
    background-size: ceil(image-width(sprite-path($map)) / 2) ceil(image-height(sprite-path($map)) / 2);
}
{% endhighlight %}

使用时，若要对icons目录下的图片生成雪碧图，且将music.png运用于.icon_music类名，按以下方式调用即可：

{% highlight sass %}
$icons: sprite-map("icons/*.png", $spacing: 4px);

.icon_music {
    @include sprite-background($icons, 'music');
}
{% endhighlight %}

注意在合成雪碧图时指定了$spacing:4px，这是为了使图片间留有空白，加之计算height/width时用的是向上取整ceil，这样一来，即使源图片尺寸的像素值为奇数，也不会出现被截断的问题了。

