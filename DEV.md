## 初始化面板

- 用户数据生成 `data.js`

```js
// 想展示的数量
const SHOW_LENGTH = 119;
/**
 * 初始化生成用户墙， 7 * 17，如果不够就补充循环，如果多了就截断
 * Row：7 行
 * Column：17 列
 */
function generateInitialUsers() {
  const initialUsers = [];
  for (let i = 0; i < SHOW_LENGTH; i++) {
    const symbol = generateRandomString(3);
    const name = generateRandomString(6);
    const atomicWeight = i;
    // 行数
    const row = (i % 17) + 1;
    const column = Math.floor(i / 17) + 1;

    const element = [symbol, name, atomicWeight, row, column];

    initialUsers.push(...element);
  }
  return initialUsers;
}
```

上面是核心代码，本质上来讲非常简单，就是根据屏幕大小以及想要展示的内容，来进行特殊处理，比如 7 行 17 列，那么就是一共展示 119 个。

> 只要对应着调整，就可以获得想要的布局，记得要适当修改 js 里生成表格的位置，才会变的居中。

## 如何让动画旋转

让球体动起来，很简单，换种思维就是让相机旋转就行了，相机绕着 Y 轴旋转，球体就会动起来。这里需要注意相机的 position 属性，因为相机的位置是相对于原点的，所以需要计算一下相机的位置，才能让相机绕着原点旋转，x 通过 cos 函数计算，z 通过 sin 函数计算，y 为 0。

```js
let ang = 0;
setTimeout(() => {
  setInterval(() => {
    // 旋转相机位置，球体就旋转了
    ang += Math.PI / 50;
    camera.position.x = Math.cos(ang) * 3000;
    camera.position.z = Math.sin(ang) * 3000;
    camera.position.y = 0;
  }, 10);
}, 2000);
```

- 如何让动画停止

让动画停止就更简单了，只需要将相机恢复到原来的位置就可以了，然后不让角度增加

```js
setTimeout(() => {
  clearInterval(timer);
  camera.position.x = 0;
  camera.position.z = 3000;
  camera.position.y = 0;
  ang = 0;
}, 10000);
```
