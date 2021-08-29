# 怎么格式化 y 轴的标签

很常见的需求，比如显示的某个城市的气温变化趋势，这个时候，我们更期望把 y 轴的标签格式化成温度的单位。直接上代码：

```ts
import { Chart } from '@antv/g2';

const data = [
  { month: 'Jan', temperature: 7 },
  { month: 'Feb', temperature: 6.9 },
  { month: 'Mar', temperature: 9.5 },
  { month: 'Apr', temperature: 14.5 },
  { month: 'May', temperature: 18.4 },
  { month: 'Jun', temperature: 21.5 },
  { month: 'Jul', temperature: 25.2 },
  { month: 'Aug', temperature: 26.5 },
  { month: 'Sep', temperature: 23.3 },
  { month: 'Oct', temperature: 18.3 },
  { month: 'Nov', temperature: 13.9 },
  { month: 'Dec', temperature: 9.6 },
];

const chart = new Chart({
  container: 'container',
  autoFit: true,
  height: 500,
  appendPadding: 4,
});

chart.data(data);
chart.scale({
  temperature: {
    min: 0,
  },
});

// 这里将 axis.label 的显示文本格式化（加上 °C 单位）
chart.axis('temperature', {
  label: {
    formatter: (val) => {
      return val + ' °C';
    },
  },
});

chart
  .line()
  .position('month*temperature')
  .shape('smooth');

chart.render();
```

大概的逻辑，就是通过设置 axis 的配置，让 label 的 formatter 为我们自定义的函数。


## 总结一下

我们可以看到 [G2 axis 的组成成分和名称](https://g2.antv.vision/zh/docs/manual/concepts/component/axis)，以及不同部分的配置项，这些配置项都能帮助我们去自定义图形上的 UI 展示，抽 10 分钟，看一遍以后遇到 axis 的问题，应该都能找到一些大概的解法。
