---
layout: post
title: 如何在微信公众号优雅的展示代码
category: other
tags: [other]
---

我在2017-04-25日开通了微信公众号，尝试着去分享一些技术文章，不可避免的文章里面有很多的代码，尝试了很多的方法，现在算是找到了一个还不错的解决方案，因此想把这个分享出来。

刚开始前自然是在网上找了一番有什么好的工具可以支持，看了很多解决方案大概分为下面几种：

-  手动复制粘贴进去调一调格式
-  代码制作成图片
-  购买专业版工具导出为微信公众号格式
-  很多在线的编辑软件
-  markdown here
-  其它

为什么会这样呢，最根本的原因就是微信的公众号不支持markdown的格式，好吧知乎也是。反正不管怎么的大家都还的继续用不是，就出来了很多的解决方案。而且微信的编辑器对代码这块支持也不够，幸好支持网页格式直接复制大家就都利用这个机制去做工具。

## 排除的方案

先说说手动复制粘贴吧，本来的代码是这个格式的：

``` java
@SpringBootApplication
@EnableDiscoveryClient
public class ProducerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ProducerApplication.class, args);
	}
}
```

在微信中就会变成下面这样，需要手动去敲回车，代码量大了苦不堪言。

``` java
@SpringBootApplication@EnableDiscoveryClientpublic class ProducerApplication {
public static void main(String[] args) {
		SpringApplication.run(ProducerApplication.class, args);
	}
}
```

或者是代码没有挤在一起，但是因为代码比较宽，只显示了半截，半截还在屏幕外面呢。

代码转化成图片，最原始的就是用截屏工具一段一段的去截屏，想想就痛苦，业内也有人写了工具来支持，具体可以参考这篇文章：[html2canvas 将代码转为图片](https://www.h5jun.com/post/convert-code-to-image-via-html2canvas.html)，但是图片多了很多会影响页面的打开速度，而且编辑的时候需要一段一段的上传图片也很复杂。

购买专业版工具导出为微信公众号格式这个方式我不喜欢，第一要花钱，第二每次需要在这个软件中去处理，再导出也挺麻烦的；很多在线的编辑软件，也是一样进去都是花花碌碌的页面，广告贼多，有些还必须先注册，体验很差。

所以以上的几种方式在一开始的时候就被我放弃了。

## 选择方案

刚开始的时候就看到了markdown here这个款工具，感觉算是体验也不错，也用了有一阵子了。我使用的是chrome浏览器，其它浏览器也有对应的插件，使用步骤如下：

- 1、在Google Chrome中安装Markdown－here插件
- 2、在sublime中用Markdwon格式书写
- 3、拷贝粘贴到微信公共帐号的编辑器中
- 4、上传文章中使用的图片
- 5、点击浏览器上的插件按钮，使用Markdown－here渲染

也可以自定义CSS，自定义代码高亮的格式等等，但是它也有两个致命的缺点：

- 以markdown格式粘贴进去之后，使用快捷键```CTRL+Alt+M```生成html后代码格式也没有问题，但是点击保存之后很多代码就会黏在一起，什么原因呢？Markdown解释器在转换代码片段时，没有在换行的时候添加```<br>```标签，而是直接输出一个换行符``` \n```，微信编辑页在保存或者预览时，将部分换行符给过滤了。
- 就算代码格式正常，使用苹果微信查看代码的时候会被自动折行，效果很差。

第一个问题也有解决方案，网上有开源精神的朋友写了插件来支持，具体可以参考这篇文章：[微信公众号代码区域换行问题（解决）
](http://www.jianshu.com/p/ea588ec043ab),但是第二个问题还是不能解决，然后我只能每次贴心的给推送的文章下面加这么一句话：

> 苹果手机代码会折行，建议苹果用户点击阅读原文查看，效果会更好一些。

每次在公众号下面去粘贴这一句，感觉也挺傻X的。

我在网上查找解决方案的时候，偶然看到小胡子哥作者写了一个开源软件:online-markdown,界面如下；

 
![](http://favorites.ren/assets/images/2017/online-markdown.png)

使用方式很简单，将写好的markdown格式的代码直接复制粘贴到这个页面里面，点击预览就可以看到渲染后的效果了，根据自己的需要也可以在上面选择不同的样式和代码高亮的格式，选完之后点击复制，直接粘贴到微信公号的编辑器中既可，我试着用了一下效果不错。

大家可以使用这个地址来测试[http://md.intelyes.xyz/](http://md.intelyes.xyz/)

但是还是有一些小瑕疵，作者也会去完善，感兴趣的可以去github上面star一下。小瑕疵有三个：

- 1、可以选择的样式不是很多，只有三种，但如果你感兴趣的话可以自己去加
- 2、“- ”的格式转换不是很好，会换行。我看有人已经提出来了，作者应该也会很快修复这个问题。
- 3、建议使用chrome浏览器，其它浏览器兼容性较差。

目前这个就是我选择使用的方案了，也希望这个工具可以帮助到大家。

> 如果你有更好的解决方案，也请一定告诉我。


