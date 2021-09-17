# 如何自定义 legend 的icon(marker)

在某些业务场景下，可能会有这样的需求：需要个性化定制每个图例前面的图标。G2 提供了 legendOption.items 用于配置图例项的内容，[legendOption.marker](https://antv-g2.gitee.io/zh/docs/api/general/legend#legendoptionmarker) 用于配置图例项的 marker 图标。

如下示例：

```js
import { Chart } from '@antv/g2';

const data = [
  { item: '事例一', count: 40, percent: 0.4 },
  { item: '事例二', count: 21, percent: 0.21 },
  { item: '事例三', count: 17, percent: 0.17 },
  { item: '事例四', count: 13, percent: 0.13 },
  { item: '事例五', count: 9, percent: 0.09 },
];

const chart = new Chart({
  container: 'container',
  autoFit: true,
  height: 500,
});

chart.coordinate('theta', {
  radius: 0.75,
});

chart.data(data);

chart.scale('percent', {
  formatter: (val) => {
    val = val * 100 + '%';
    return val;
  },
});

chart.tooltip({
  showTitle: false,
  showMarkers: false,
});

// 看这里：利用 legend 配置中的 items 即可为每个图例配置不同的图形标志
chart.legend({
  items: [
    {
      name: '事例一',
      marker: {
        style: { // 通过 style 可以设置纹理等
          fill: 'p(a)https://gw.alipayobjects.com/zos/rmsportal/ibtwzHXSxomqbZCPMLqS.png'
        }
      },
    },
    {
      name: '事例二',
      marker: {
        symbol: 'square', // 设置不同的 symbol 值展示不同的 icon
      },
    },
    {
      name: '事例三',
      marker: {
        symbol: 'diamond',
      },
    },
    {
      name: '事例四',
      marker: {
        symbol: 'triangle',
      },
    },
    {
      name: '事例五',
      marker: {
        symbol: 'triangle-down',
      },
    },
  ]
});

chart
  .interval()
  .position('percent')
  .color('item')
  .label('percent', {
    content: (data) => {
      return `${data.item}: ${data.percent * 100}%`;
    },
  })
  .adjust('stack');

chart.interaction('element-active');

chart.render();

```

![](https://cdn.nlark.com/yuque/0/2021/png/22203542/1631882399093-6c461426-7df0-4154-845f-b2754af1143b.png)

## 注意事项

目前，G2 尚未支持使用自定义图片设置图例

## 总结一下

Legend 作为图表的辅助元素，在 G2 官网的[教程和文章--Lengend图例](https://antv-g2.gitee.io/zh/docs/manual/tutorial/legend/#gatsby-focus-wrapper)一节就可以清楚知道如何配置图例，对图例的整体样式做设置，以及如何设置各个图例项的样式等，帮助您快速熟悉 Legend。当需要查看详细的 API 时，则应该到 G2 官网的 [G2 详细手册](https://antv-g2.gitee.io/zh/docs/api/general/legend/#legendoptionlayout) 查看相关内容。
