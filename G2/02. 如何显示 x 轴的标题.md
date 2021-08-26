# 如何显示 x 轴的标题

G2 绘制出图形之后，默认的 x 轴是不显示标题的，但是有很多业务场景是需要标识出 x 轴的数据是什么含义，做法很简单，如下示例：

```ts
import { Chart } from '@antv/g2';

const data = [
  { type: '未知', value: 654, percent: 0.02 },
  { type: '17 岁以下', value: 654, percent: 0.02 },
  { type: '18-24 岁', value: 4400, percent: 0.2 },
  { type: '25-29 岁', value: 5300, percent: 0.24 },
  { type: '30-39 岁', value: 6200, percent: 0.28 },
  { type: '40-49 岁', value: 3300, percent: 0.14 },
  { type: '50 岁以上', value: 1500, percent: 0.06 },
];

const chart = new Chart({
  container: 'container',
  autoFit: true,
  height: 500,
  padding: [50, 20, 50, 20],
});
chart.data(data);

// 看这里： 设置 type 字段，也就是 x 轴的 title 为空对象，默认是 null，表示不显示
chart.axis('type', {
  title: {},
});

chart.interval().position('type*value');

chart.render();
```

![column-with-x-title](https://user-images.githubusercontent.com/7856674/130890333-cc75cc2b-d77c-4b49-b40f-9e7bae38dec9.png)

同样的，对于 axis 坐标轴，G2 是拆分成好几个部分，每个部分在 axis 配置中是一个单独的键值存储的。可以看 [G2 官方关于 axis 的文档](https://g2.antv.vision/zh/docs/manual/concepts/component/axis)。

![parts-of-axis](https://user-images.githubusercontent.com/7856674/130890486-53278b72-98a7-42ff-bbd9-310f4466fdd1.png)

按照上图的描述，完整的 axis 配置就是：

```ts
chart.axis('type', {
  title: {},
  grid: {},
  label: {},
  line: {},
  tickLine: {},
});
```

具体的配置，在代码类型定义、官网文档都描述的很详细，去试一试吧。


## 总结一下

G2 的整个图表，分成为两个大部分：组件（component）、图形（geometry）。对于不同的组件会将他拆成不同的区域，对于不同的区域具备有不同配置项。按照这样的思路去看文档，可能会相对简单一些。

最后，给一个 G2 官网所有[组件列表的文档](https://g2.antv.vision/zh/docs/manual/concepts/component/overview)，其实大部分的可视化图表都有这样的组件。