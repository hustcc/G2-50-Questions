# 怎么给柱形图的 x 轴进行排序

如下图所示，展示的三家国外互联网公司的员工类型占比，如果我们期望 x 轴显示的数据顺序为 `非技术岗`、`技术岗`、`整体`，那么该如何做？

![image](https://user-images.githubusercontent.com/7856674/131275633-e19234f6-9a11-486f-91da-064f3e39c0bd.png)

有两种方式：

 - **数据排序**

将数据传入到 G2 之前，对数据进行排序，排序顺序就是按照 `非技术岗`、`技术岗`、`整体` 来。这种方式是最基本的方式，最简单，也最容易理解。

 - **scale 数据顺序**

但是更加数据可视化一些的方式，是修改 x 字段的数据映射顺序，默认的映射顺序是按照传入到 G2 中的顺序，我们可以去修改这个顺序即可，这就非常简单了。

```ts
import { Chart } from '@antv/g2';

const data = [
  { company: 'Apple', type: '整体', value: 30 },
  { company: 'Facebook', type: '整体', value: 35 },
  { company: 'Google', type: '整体', value: 28 },
  { company: 'Apple', type: '非技术岗', value: 40 },
  { company: 'Facebook', type: '非技术岗', value: 65 },
  { company: 'Google', type: '非技术岗', value: 47 },
  { company: 'Apple', type: '技术岗', value: 23 },
  { company: 'Facebook', type: '技术岗', value: 18 },
  { company: 'Google', type: '技术岗', value: 20 },
  { company: 'Apple', type: '技术岗', value: 35 },
  { company: 'Facebook', type: '技术岗', value: 30 },
  { company: 'Google', type: '技术岗', value: 25 }
];

const chart = new Chart({
  container: 'container',
  autoFit: true,
  height: 500,
});

chart.data(data);

// 这里修改 x 轴字段 type 的映射范围和顺序
chart.scale('type', {
  values: ['非技术岗', '技术岗', '整体']
});

chart
  .interval()
  .position('type*value').color('company')
  .adjust([{
    type: 'dodge',
  }]);

chart.render();
```

![image](https://user-images.githubusercontent.com/7856674/131276173-9261d551-97ef-4a52-9a15-a4082e3df784.png)


## 小结一下

我们前面有不少问题都是在讲 scale，scale 是图形语法甚至可视化技术中非常重要的改良，好好理解它吧。在 G2 中，通过 values 去修改数据映射顺序，可以实现：

 - x 轴显示的顺序
 - 图例项的顺序
 - 额外增加一些数据项
 - ...