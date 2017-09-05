# Intro 🐯
前面的系列介绍了[HRM前端项目开发的最佳实践](https://github.com/renliwo/hrm-fe-best-practice)，以及[如何与测试撕逼](https://github.com/renliwo/hrm-doctor)，本篇文章主要介绍如何和UI／UE 撕逼。

# Motivation💗
```
UI： 有时间吗？ 我们来调下样式吧！
FE： 。。。  稍等啊。
。。。   一分钟后

UI： 有时间吗？ 我们来调下样式吧！
FE： 。。。 好吧，你来吧。

UI： 这个button 颜色不对，不是#fff, 应该是#e3e3e3
还有这里也不对，这个间距应该是10px，还有这里这个字体大小不对，
这个对齐也不对啊。
FE： 。。。 那个。。。 我现在有点事，要不我们改天吧。

```
这就是我， 一个小小的平凡的前端。 经常要和UI 撕逼。
所以有没有办法减少这种撕逼呢？
答案是有。
# How ❓
### 开发前坐下来和UI定一下规则
我么你项目使用的是ant-design mobile。 有很多人问我：使用ant-design 真的可以减少前端工作量吗？ 我怎么感觉用了ant-design，更累了？

其实累不累完全取决于项目的需求，如果你的项目需求和ant-design非常一致，那么我可以肯定地说，会减少你很多时间。 但是相反，你的设计师的设计思想，风格和ant-desgin 差异非常大，很多组件都需要你自己重写，那么你会非常累，甚至有重写一套的冲动。

因此开发前和UI做下来定下规则，是很重要的。 大到柵格系统，有的系统设计24等分，有的是12等分。 小到一个button 的底色，每一个系统都是不完全一样的。如果强行搬运，不加修改，你会感觉非常难受。
这里有一份[ant-desin-mobile 的清单](https://github.com/ant-design/ant-design-mobile/blob/master/components/style/themes/default.less)。 该清单定义了一系列的基本值，这些都是和设计师事先约定好的。

当和设计师约定好了之后，将这些基本值写入文件，作为我们和设计师的约定。 下面以ant-design-mobile为例，讲解如何具体操作
1. 定义基本值

```js

module.exports = () => ({
  "fill-body": "#f8f8f8",
  "color-text-base": "#333",
  "fill-base": "#f8f8f8",
  "fill-tap": "#e4e4e4"
});

```

2. package.json中引用上面的文件

```
"theme": "./src/theme/variable.js",
```

### 和UI 约定组件，设计稿按照约定的组件和设计规范来
通常情况下设计师有一套组件库，出图都是将组件库堆起来的。 就像前端的组件化开发一样的。这是[ant-design-mobile的sketch模板](https://github.com/ant-design/ant-design/releases/download/resource/Ant.Design.Mobile.Template.sketch)
如果项目前端使用的组件是和设计师的模板组件完全一致的（像素级还原的），那么我们做出来的东西就**很容易** 真正的像素级还原设计稿，反之很难。

### 开发的时候，如何像素级还原UI稿
那么假如前面的你都做到了，那么恭喜你，你基本上可以完美还原设计稿了，现在还有一个问题。对于我这样不是像素眼，而且还比较粗心的人，如何尽可能还原设计稿呢？下一步就是精准的尺寸，包括间距、宽高、位置等等。在没遇到马克鳗之前，我一直苦逼得用 QQ 截图来测量尺寸、大小和位置。好在 QQ 截图得功能比较强大，测量得还算准确，缺陷就是需要来回切换程序界面，一次次得测量，这样必然导致低效率。

> 此外，不只是测量尺寸，还原设计稿还需要提取对应位置得背景颜色等等。这样还需要在后台打开 Photoshop 然后偶尔切换到 PS 中，用拾色器来取色。这样改进后的测量方法就变成了：打开设计稿（PSD 或者将 PSD 中不同页面的设计稿保存出来 jpg），使用马克鳗进行标注并且观察设计结构和样式，思考如何做页面结构如何切图。之后根据上面的方法切图，再打开马克鳗测量后的图片，对照尺寸重构页面。

> 开发完成之后如何检测我们是否还原了设计稿？这里有一个工具，可以帮助你完成。 [alloydesigner](https://github.com/AlloyTeam/AlloyDesigner)是腾讯 alloyteam 团队开发的用来辅助前端页面重构的工具.正如它的介绍一样，AlloyDesigner是一款致力于提高前端生产效率的浏览器内运行工具，AlloyDesigner + Chrome F12(Especially with WorkSpace) 打造前端新的开发和测试模式。通过它，可以减少你UI开发时间，其实我是对UI开发不太感冒的人，因此这个工具对我来说吸引力还是很大的。

# Conclusion 😁
通过事前计划（约定），事中控制（工具辅助），我们有机会完美还原设计稿。以后我们和UI 撕逼也可以理直气壮了，妈妈再也不用担心我和UI撕逼了。😊
