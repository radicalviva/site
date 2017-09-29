<!--
title: 快速上手
resource:
  jsFiles:
    - ${url.g2}
-->

# 快速上手

## G2

G2 (The Grammar Of Graphics) 是一个由纯 JavaScript 编写、强大的语义化图表生成工具，它提供了一整套图形语法，可以让用户通过简单的语法搭建出无数种图表，并且集成了大量的统计工具，支持多种坐标系绘制，可以让用户自由地定制图表，是为大数据时代而准备的强大的可视化工具。

## 特性

- 简单、易用
- 完备的可视化编码
- 强大的扩展能力


## 安装

### 浏览器引入

既可以通过将脚本下载到本地也可以直接引入在线资源；


```html
<!-- 引入在线资源 -->
<script src="https://a.alipayobjects.com/g/datavis/g2/2.3.10/index.js"></script>
```

```html
<!-- 引入本地脚本 -->
<script src="./g2.js"></script>
```

### 通过 npm 安装
<a href="https://www.npmjs.com/package/g2" target="_blank"><img src="https://img.shields.io/npm/v/g2.svg?style=flat"></a>

我们提供了 G2 npm 包，通过下面的命令即可完成安装

```bash
npm install g2 --save
```
成功安装完成之后，即可使用 `import` 或 `require` 进行引用。

```js
var G2 = require('g2');
var chart = new G2.Chart({
  id: 'c1',
  width: 600,
  height: 300
});
```

## 快速开始
在 G2 引入页面后，我们就已经做好了创建第一个图表的准备了。

下面是以一个基础的柱状图为例开始我们的第一个图表创建。

### 浏览器引入方式

#### 1. 创建 `div` 图表容器

在页面的 `body` 部分创建一个 div，并制定必须的属性 `id`：

```html
<div id="c1"></div>
```

#### 2. 编写图表绘制代码

创建 `div` 容器后，我们就可以进行简单的图表绘制:

1. 创建 Chart 图表对象，指定图表所在的容器 ID、指定图表的宽高、边距等信息；
2. 载入图表数据源；
3. 使用图形语法进行图表的绘制；
4. 渲染图表。

这部分代码用 `<script></script>`，可以放在页面代码的任意位置（最好的做法是放在 `</body>` 之前）。

```js
var data = [
  {genre: 'Sports', sold: 275},
  {genre: 'Strategy', sold: 115},
  {genre: 'Action', sold: 120},
  {genre: 'Shooter', sold: 350},
  {genre: 'Other', sold: 150},
]; // G2 对数据源格式的要求，仅仅是 JSON 数组，数组的每个元素是一个标准 JSON 对象。
// Step 1: 创建 Chart 对象
var chart = new G2.Chart({
  id: 'c1', // 指定图表容器 ID
  width : 600, // 指定图表宽度
  height : 300 // 指定图表高度
});
// Step 2: 载入数据源,定义列信息
chart.source(data, {
  genre: {
    alias: '游戏种类' // 列定义，定义该属性显示的别名
  },
  sold: {
    alias: '销售量'
  }
});
// Step 3：创建图形语法，绘制柱状图，由 genre 和 sold 两个属性决定图形位置，genre 映射至 x 轴，sold 映射至 y 轴
chart.interval().position('genre*sold').color('genre')
// Step 4: 渲染图表
chart.render();
```

完成上述两步之后，保存文件并用浏览器打开，一张柱状图就绘制成功了：

<div id="c1"></div>

```js-
  var data = [
    {genre: 'Sports', sold: 275},
    {genre: 'Strategy', sold: 115},
    {genre: 'Action', sold: 120},
    {genre: 'Shooter', sold: 350},
    {genre: 'Other', sold: 150},
  ];
  var chart = new G2.Chart({
    id: 'c1',
    forceFit: true,
    height : 400
  });
  chart.source(data, {
    genre: {
      alias: '游戏种类'
    },
    sold: {
      alias: '销售量'
    }
  });
  chart.interval().position('genre*sold').color('genre')
  chart.render();
```

完整的代码如下：

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>柱状图</title>
    <!-- 引入 G2 文件 -->
    <script src="https://a.alipayobjects.com/g/datavis/g2/2.3.6/g2.js"></script>
  </head>
  <body>
    <!-- 创建图表容器 -->
    <div id="c1"></div>
    <script>
      var data = [
        {genre: 'Sports', sold: 275},
        {genre: 'Strategy', sold: 115},
        {genre: 'Action', sold: 120},
        {genre: 'Shooter', sold: 350},
        {genre: 'Other', sold: 150},
      ]; // G2 对数据源格式的要求，仅仅是 JSON 数组，数组的每个元素是一个标准 JSON 对象。
      // Step 1: 创建 Chart 对象
      var chart = new G2.Chart({
        id: 'c1', // 指定图表容器 ID
        width : 600, // 指定图表宽度
        height : 300 // 指定图表高度
      });
      // Step 2: 载入数据源,定义列信息
      chart.source(data, {
        genre: {
          alias: '游戏种类' // 列定义，定义该属性显示的别名
        },
        sold: {
          alias: '销售量'
        }
      });
      // Step 3：创建图形语法，绘制柱状图，由 genre 和 sold 两个属性决定图形位置，genre 映射至 x 轴，sold 映射至 y 轴
      chart.interval().position('genre*sold').color('genre')
      // Step 4: 渲染图表
      chart.render();
    </script>
  </body>
</html>
```

### 在React中使用G2

[BizCharts]()
<!-- TODO -->

## 体验改进计划说明

为了更好服务用户，G2 会将 URL 等信息发送回 AntV 服务器：

```html
https://kcart.alipay.com/web/bi.do
```
除了 URL 与 G2 版本信息外，不会收集任何其他信息，一切为了能对 G2 的运行情况有更多了解，以更好服务于用户。如有担心，可以通过下面的代码关闭：

```js
// 关闭 G2 的体验改进计划打点请求
G2.track(false)
```