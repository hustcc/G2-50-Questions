# 怎么设置 y 轴显示的最大最小值范围

之前关注房子的时候，看到一些图，类似如下的：

![image](https://user-images.githubusercontent.com/7856674/131236964-82301fcf-625f-4a76-b9a6-630593713975.png)

左边的图描述的是广州房价 1 年的趋势变化，从折线图上可以看到趋势还是比较陡峭的，但是这个图是一个错误的可视化案例，因为 y 轴的最小值不是从 0 开始的，导致折线图的趋势看起来比较陡峭，而实际上并没有图中这么恐怖的涨幅。

我们用 G2 绘制一个类似的图。

```ts
import { Chart } from '@antv/g2';

const data = [
  { year: '1991', value: 3800 },
  { year: '1992', value: 4000 },
  { year: '1993', value: 3500 },
  { year: '1994', value: 4500 },
  { year: '1995', value: 4900 },
  { year: '1996', value: 5000 },
  { year: '1997', value: 5200 },
  { year: '1998', value: 4000 },
  { year: '1999', value: 5000 },
];
const chart = new Chart({
  container: 'container',
  autoFit: true,
});

chart.data(data);
chart.line().position('year*value').label('value');
chart.point().position('year*value');

chart.render();
```

![image](https://user-images.githubusercontent.com/7856674/131237252-498ad60a-c9d8-4e7e-bd55-ed0c2077982c.png)

这个图中实际的数据浮动在 25% 左右，但是实际的效果 100% 的浮动效果。这是一个错误的可视化表达，正确的应该是，设置 y 轴显示的最小值从 0 开始。那么怎么做的？

在 G2 中，做到这个非常简单，只需要设置对应 `scale` 字段描述的 min = 0 即可。

```diff
+ chart.scale('value', {
+   min: 0,
+ });
```

绘制出来的效果如下所示，可以看出这样才能反映出真实的数据情况和洞察。

![image](https://user-images.githubusercontent.com/7856674/131237364-77399652-bdfa-4be3-88cc-93a527b817d1.png)


## 总结一下

`scale` 是可视化中非常重要的一个概念，在 G2 中，它代表着一个字段的描述信息，包含有：

 - 数据映射的方式、范围（min、max）
 - 字段信息（id、别名、格式化等等）

而 G2 的 axis 分别对应着 x、y 字段的 scale，所以坐标轴显示上的一些问题，很多都可以在 scale 中找到解决办法。更多 [G2 scale 教程](https://g2.antv.vision/zh/docs/manual/tutorial/scale)，可以看这链接。