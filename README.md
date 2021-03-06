<img class="lyb" src="https://img-bed-five.vercel.app/img/lyb.png" style="width:200px;margin:0 auto;border-radius:50%" />

<p style="font-size:50px;font-weight:bold;width:100%;text-align:center;color:#fff;text-shadow:0 0 15px">冷弋白</p>
<p style="text-align:center;color:#aaa;position: relative;top:-10px;text-shadow:0 0 10px"><a href='https://wpa.qq.com/msgrd?v=3&uin=1329670984&site=qq&menu=yes' style='text-decoration: none;
'>点击此处联系我</a></p>
# 温馨提示

> 并不建议直接引入文件，推荐开发者在项目中新建`库文件`，按需复制需要的`函数`并粘贴进`库文件`，可避免作者更新，而导致项目报错
>
> 函数库地址：https://gitee.com/lengyibai/code-base

# 原生封装

## 返回数据类型

> 返回的数据类型为全小写的字符串

```js
console.log(
  $type('5555'), //string
  $type(123), //number
  $type(false), //boolean
  $type([5, 5]), //array
  $type(function () {}), //function
  $type({ a: 1 }), //object
);
```

## 判断数据类型

> 返回`Boolean`值

```js
console.log(
  $isArray([]), //true
  $isBoolean(false), //true
  $isObject({}), //true
  $isString(""), //true
  $isFunction(() => {}), //true
);
```

## 控制全屏显示

> 点击指定按钮或指定条件下全屏显示

```js
$isFull(); //开启全屏
$noFull(); //关闭全屏
```

## 随机数

> 随机生成指定范围的数据，生成的数字会包含两个参数
>
> 参数`min`：传递一个数字，最小值
>
> 参数`max`：传递一个数字，最大值
>
> 参数`retain`：保留几位小数，默认整数

```js
$random(min, max, retain);
```

## 字符串去重

### 全局

> 去掉字符串重复的字符

```js
$strDelRep(str);
```

> 参数`str`：一个字符串

```js
  const str = '1233211234567';
  console.log($strDelRep(str)); //'1234567'
```

### 连续

> 去掉字符串连续重复的字符

```js
$strDelReps(str);
```

> 参数`str`：一个字符串

```js
const str = '122333444455555';
console.log($strDelReps(str)); //'12345'
```

## 数组深度去重

> 去掉数组内重复的对象、数组、字符串
>
> 注：如果数组内包含只有一个数组元素的数组，则这个只有一个数组元素的数组会被直接去掉

```js
$arrDelRep(arr);
```

> 参数`arr`：一个数组
>

```js
  const arr = [
    'a',
    'a',
    1,
    1,
    ['a', 1],
    ['a', 1],
    { a: 1 },
    { a: 1 },
    true,
    true
  ];
  console.log($arrDelRep(arr)); //[ "a", 1, [ "a", 1 ], { "a": 1 }, true ]
```

## 对象去重

> 根据指定对象属性名，去掉数组内与包含唯一`id`相同的对象，只会保留第一个

```js
$objDelRep(arr, key);
```

> 参数`arr`：传递包含对象的是数组
>
> 参数`key`：根据指定属性来去重，一般为对象`id`值

```js
const arr = [
  { id: 1, name: 'lyb' },
  { id: 1, name: 'lengyibai' },
  { id: 2, name: '冷弋白' },
];
console.log($objDelRep(arr, 'id')); //[ { id: 1, name: 'lyb', }, { id: 2, name: '冷弋白', }, ];
```

## 获取浏览器谷歌内核版本

```js
console.log($chromeV());
```

# 功能类函数

## 防抖节流

### 使用方法

> 直接调用

```js
setInterval(
  $debounce(() => {
    console.log(666);
  }, 1000),
  100,
);
```

> 在函数内使用

```js
const lyb = $debounce(fn, 1000);
setInterval(() => {
  lyb();
}, 100);
```

> 在`Vue`内使用

```js
export default {
  data() {
    return {
      lyb: null,
    };
  },
  created() {
    lyb = $throttle(function () {}.bind(this), 250);
  },
  mounted() {
    setInterval(() => {
      lyb();
    }, 100);
  },
};
```

### 防抖

> 参数`fn`：传递一个函数
>
> 参数`wait`：传递一个毫秒
>
> 参数`mtm`：传递一个布尔值，是否立即执行，默认为`false`

#### 延迟执行（常用）

> 函数调用后，如果在规定时间内没有再次调用，那么就执行函数

```js
$debounce(fn, wait, false);
```

#### 立即执行

> 调用后立即执行一次
>
> 再次调用需要停止调用一定时间

```js
$debounce(fn, wait, true);
```

### 节流

> 参数`fn`：传递一个函数
>
> 参数`wait`：传递一个毫秒
>
> 参数`mtm`：传递一个布尔值，是否立即执行，默认为`false`

#### 延迟执行（常用）

> 每次调用需要等待一定时间才会执行
>
> 执行后才会进行下一次调用

```js
$throttle(fn, wait, false);
```

#### 立即执行

> 调用后立即执行操作
>
> 再次调用需要等待一定时间

```js
$throttle(fn, wait, true);
```

## 数字每三位加逗号

```js
console.log($fmtNum(1000)); //1,000
```

## 复制到剪切板

> 只能通过鼠标事件触发

```js
$copy(str, fn);
```

> 参数`str`：传递一个字符串/数字
>
> 参数`fn`：复制成功后将会调用，并可以接收参数，为复制的内容

```js
$copy('冷弋白', function () {
  console.log(text); //冷弋白
});
```

## 日期格式化

> 一般用于后端向前端传递时间戳，来转换为指定格式的时间
>
> 用于显示发表评论的时间
>
> `MM`、`dd`、`hh`、`mm`、`ss`可省略为一个字母，省略后低于`10`不会自动加前缀`0`
>
> 另外可以通过`w`和`n`获取星期和时间戳

```js
$fmtTime(dates, fmt);
```

> 参数`date`：传递时间类型的数据
>
> 参数`fmt`：传递时间格式

```js
const date = new Date('2000-05-09 09:30:05').getTime(); //假设这是后端传递过来的时间戳
console.log($fmtTime(date, 'YYYY-MM-DD hh:mm:ss w n')); //2000-5-09 09:30:05 周几 时间戳
```

## 根据时间段问候

> 可修改问候内容

```js
console.log($timeGreet({ a: '都第二天了，该睡了' })); //根据你当前的时间段显示内容
/*
4点之前a：午夜，默认提示午夜好
10点之前b：早上，默认提示早上好
12点之前c：上午，默认提示上午好
14点之前d：中午，默认提示中午好
18点之前e：下午，默认提示下午好
0点之前f：晚上，默认提示晚上好
*/
```

## 记录已过去时间或倒计时

> 一般记录网站已运行时间和倒计时

```js
$getCountTime(time);
```

> 参数`time`：传递过去或未来时间，如果是未来时间，将返回倒计时，如果是过去时间，则返回已过去时间

```js
setInterval(() => {
  console.log($getCountTime('2022-01-01 00:00:00')); //{ y: x, mon: x, d: x, h: x, min: x, s: x }
}, 1000);
```

## 中文转拼音

```js
console.log($pinyin('冷弋白')); //[ 'lengyibai', 'LengYiBai', 'lyb', 'LYB' ]
```

## 正则搜索

> 支持各种关键属性搜索、支持拼音搜索、支持拼音简写搜索、不区分大小写、支持模糊查询
>
> 如果输入框清空查询，则返回所有数据
>
> 注：依赖于`$pinyin`，如果库是直接引入的，可忽略

```js
$search(data, value, keys);
```

> 参数`data`：传递一个数组，里面存有对象形式的数据
>
> 参数`value`：支持传递数组和字符串和`-`分隔的字符串
>
> 参数`keys`：传递一个数组，代表搜索的属性

```js
const obj = [
  { id: 1, name: '张三', age: 20 },
  { id: 2, name: '李四', age: 24 },
  { id: 3, name: '王五', age: 24 },
  { id: 4, name: '赵六', age: 24 },
];

console.log($search(obj, 24, ['name', 'age']));
// [{ name: '李四', age: 24 }, { name: '王五', age: 24 }, { name: '赵六', age: 24 }]

console.log($search(obj, ['zs'], ['name', 'age']));
// [{ name: '张三', age: 20 }]

console.log($search(obj, 'LiS', ['name', 'age']));
// [ { name: '李四', age: 24 } ]

console.log($search(obj, ['张三', 'ww'], ['name', 'age']));
// [ { name: '张三', age: 20 }, { name: '王五', age: 24 } ]

console.log($search(obj, 'zs-lis', ['name', 'age']));
// [ { name: '张三', age: 20 }, { name: '李四', age: 24 } ]
```

### 针对 Element UI 的下拉多选进行查询

> 注：此时不需要依赖任何函数，但不支持拼音查询，况且也不可能拼音查询
>
> 如果下拉框清空查询，则需要使用`[""]`去查询，这样查询才能返回所有数据

```js
$searchMul(data, value, key);
```

> 参数`data`：传递一个数组，里面存有对象形式的数据
>
> 参数`value`：传递数组，数组内为需要搜索的值
>
> 参数`key`：传递字符串，代表搜索的属性

```js
const obj = [
  { id: 1, name: '张三', age: 20 },
  { id: 2, name: '李四', age: 24 },
  { id: 3, name: '王五', age: 24 },
  { id: 4, name: '赵六', age: 24 },
];

console.log($searchMul(obj, ['张三', '李四'], 'name'));
// [ { name: '张三', age: 20 }, { name: '王五', age: 24 } ]
```

## 判断是否为指定类型的文件链接

> 目前只有图片和视频，可修改源码设置新类型，也可直接传递参数

```js
$urlFileType(url, type);
```

> 参数`url`：传递字符串，代表文件路径
>
> 参数`type`：传递字符串，代表文件类型，目前可判断`image`和`video`
>
> 如果会在多个地方使用此函数进行判断，建议修改源码。如果只会使用一次，`type`可传递需要判断的类型数组，如`['zip', '7z', 'rar']`

```js
console.log($urlFileType('文件.123.MP4', 'video')); //true
console.log($urlFileType('文件.321.PNG', 'video')); //false
console.log($urlFileType('文件.231.AVI', 'image')); //true
console.log($urlFileType('文件.213.JPEG', 'image')); //false
console.log($urlFileType('文件.213.JPEG', ['zip', '7z', 'rar'])); //false
console.log($urlFileType('文件.213.7z', ['zip', '7z', 'rar'])); //true
```

## 全局替换指定字符串

> 替换字符串中所有匹配到的字符串

```js
$repStr(str, match, rep);
```

> 参数`str`：传递字符串
>
> 参数`match`：匹配指定字符，使用`|`可匹配多个进行替换
>
> 参数`rep`：替换为指定字符，默认替换为空白字符

```js
const id = 'id: GROUP@TGS#GROUP4X4JBGRH2';
console.log($repStr(id, 'GROUP', '')); //id: @TGS#4X4JBGRH2
```

## 获取文件名

```js
console.log($getFileName('冷弋白.lyb.png'); //冷弋白.lyb
```

## 获取文件后缀名

> 如果后缀有大写字母，将自动转换为小写

```js
console.log($getFileSuf('冷弋白.123.JPEG')); //jpeg
```

## 排序支持数字&字母&时间&中文

> 支持数组和数组内的对象

```js
$typeSort(data, rev);
$typeSort(data, key, rev);
```

| 对象属性 | 说明                                  | 类型    | 是否必填                                        | 默认值 |
| -------- | ------------------------------------- | ------- | ----------------------------------------------- | ------ |
| data     | 无                                    | Array   | 是                                              | -      |
| key      | 要进行排序的对象属性名                | String  | 只有数组：此参数代替`rev`<br />数组含对象：必填 | -      |
| rev      | 正序还是倒序，`true`正序，`false`倒序 | Boolean | 否                                              | true   |

```js
const data = [
  { id: 3, abbr: 'pg', name: '苹果', time: '2019-04-25 12:00:22' },
  { id: 1, abbr: 'hw', name: '华为', time: '2019-04-22 10:00:19' },
  { id: 2, abbr: 'xm', name: '小米', time: '2019-04-22 10:00:18' },
];

console.log($typeSort(data, 'name'));
/*
[
  { id: 1, abbr: 'hw', name: '华为', time: '2019-04-22 10:00:19' },
  { id: 3, abbr: 'pg', name: '苹果', time: '2019-04-25 12:00:22' },
  { id: 2, abbr: 'xm', name: '小米', time: '2019-04-22 10:00:18' }
]
*/

let num = [1, 5, 3, 2, 4, 5, 3, 6, 9];
console.log($typeSort(data, false)); //[ 9, 6, 5, 5, 4, 3, 3, 2, 1 ]
```

## 字节格式化

> 一般用于上传文件时的文件大小或后端返回的文件大小
>
> 返回一个数组，数组元素分别是`['大小','单位','大小单位']`

```js
console.log($fmtByte(2000)); //['1.95', 'KB', '1.95 KB']
console.log($fmtByte(2048)); //['2.00', 'KB', '2.00 KB']
```

## 秒数格式化

> 返回一个数组，数组元素分别是`['时','分','秒','时:分:秒']`

```js
console.log($fmtSec(99999)); //[ 27, 46, 39, '27:46:39' ]
```

## 小数、百分比互转

> 如果是小数转百分比，会返回一个`Number`类型，需要手动添加`%`，并且会四舍五入
>
> 转为百分比只会保留一位小数

```js
$potEoPct(i, ret);
```

> 参数`i`：传递字符串的百分比或数字
>
> 参数`ret`：传递数字，保留几位小数，默认不保留

```js
console.log($potEoPct(0.12345, 2)); //12.35
console.log($potEoPct('12.34%')); //0.1234
```

## 图片上传修改

> 点击图片，选择图片，进行修改
>
> 内部使用了`axios`需要在函数外手动引入`axios`
>
> 需要在源码内设置接口地址

```js
$editFile(event)
```

> 参数`event`：事件对象

```vue
<template>
   <input type="file" @change="fn" />
</template>

<script>
export default {
  methods: {
    fn(e) {
      $editFile(e).then(res => {
        console.log(res);
      });
    }
  }
};
</script>
```

## 图片压缩

> 超过一定大小进行压缩
>
> 超过一定尺寸进行压缩

```js
$imageOptimizer(obj)
```

| 对象属性     | 说明                                                         | 类型              | 是否必填 | 默认值   |
| ------------ | ------------------------------------------------------------ | ----------------- | -------- | -------- |
| el \|\| file | `input`表单或`file`类型的文件                                | Element \|\| File | 二选一   | -        |
| width        | 压缩的宽度，超过则压缩                                       | Number            | 否       | 自身宽度 |
| ratio        | 压缩率，0<`ratio`<=1                                         | Number            | 否       | 1        |
| maxsize      | 文件大小超过多大进行压缩，单位`kb`                           | Number            | 否       | 1024     |
| success      | 压缩成功回调<br />回调参数：<br />参数1：可直接传给后端的表单对象<br />参数2：`file`类型<br />参数3：base64，可放置在`a`标签上下载以及`img`标签上预览 | Function          | 是       | -        |

```html
<body>
  <input type="file" id="img">

  <!-- JS -->
  <script>
    const img = document.querySelector('#img');
    img.addEventListener('change', function () {
      $imageOptimizer({
        el: img, //上传图片的input元素
        //file:f, //file类型的文件
        width: 1000, //压缩尺寸
        ratio: 1, //压缩率
        maxsize: 1024, //超过多大进行压缩
        /* 成功回调 */
        success: (data, file, url) => {}
      });
    })
  </script>
</body>
```

## requestAnimationFrame计时器

> 比`setInterval`拥有更好的性能，比如切换软件窗口，会暂停执行，返回浏览器窗口继续执行，不会占用性能，而`setInterval`在切换、最小化浏览器窗口后依然会执行
>
> 唯一不足的是无法清除，以及频率比`setInterval`快百来毫秒，一般用于不需要清除的动画和不在意时间精度功能，如粒子效果

```js
$frameInterval(fn,fre)
```

> 参数与`setInterval`的前两个参数的功能一样

```js
const box = document.querySelector(".box");
let deg = 0;
$frameInterval(() => {
  deg++;
  console.log(deg);
  box.style.transform = `rotate(${deg}deg)`;
});
```

## 对象转Excel

> 需要安装依赖：`npm i xlsx@0.17.4`，且只能安装`0.17.4`版本
>
> 还需引入`import XLSX from "xlsx"`
>
> 用于导出表格

```js
$objToExc(obj)
```

| 对象属性 | 说明                                                         | 类型   | 是否必填 | 默认值     |
| -------- | ------------------------------------------------------------ | ------ | -------- | ---------- |
| name     | 导出的文件名                                                 | String | 否       | 未命名表格 |
| data     | 需要导出为Excel表格的数据                                    | Array  | 是       | -          |
| format   | 主要功能是更改对象的属性，来作为Excel的表头，不填则导出所有列，填一列导出一列，详细用法见下 | Object | 否       | {}         |

```html
<template>
    <button @click="$objToExc">点击导出</button>
</template>
<script>
import { $objToExc } from "./lyb.js";
export default {
  data() {
    return {
      data = [
        { a: 0, name: '张三', age: 20, b: 0 },
        { a: 1, name: '李四', age: 21, b: 1 },
        { a: 2, name: '王五', age: 22, b: 2 },
      ],
    };
  },
  methods: {
    $objToExc() {
      /*
      	将对象的name和age替换为姓名和年龄，在表格内就会展示姓名和年龄的表头，且只有姓名和年龄两列
      	不填则导出所有列
      */
      $objToExc({data:this.data, format:{ name: '姓名', age: '年龄' }});
    },
  },
};
</script>
```

## Excel转对象

> 相当于解析文件，很少遇到这种需求，但将`Excel`解析和过滤再导出也挺不错

```js
$excToObj(e)
```

> `e`：见代码

```html
<template>
    <input
      type="file"
      accept=".xls, .xlsx"
      @change="$excToObj"
    />
</template>
<script>
import { $excToObj } from "./lyb.js";
export default {
  methods: {
    $excToObj(e) {
      console.log($excToObj(e)); //打印的是解析Excel后的数据
    },
  },
};
</script>
```

## 获取地址栏参数

> 直接调用即可，返回一个参数对象

```js
$getPathParams()
```

# 样式类函数

## 自定义拖拽元素

> 自定义元素是否可拖拽
>
> 前提是父元素加了定位、被拖拽元素加了`绝对定位`

```js
$dragEl([dom,dom,...])
```

> 传递一个数组

| 说明                                                                                                                          | 类型  | 是否必填 | 默认值 |
| ----------------------------------------------------------------------------------------------------------------------------- | ----- | -------- | ------ |
| 传递一个或多个已经通过*document.querSelector*或*document.querSelectorAll*获取的元素，<br />需要存放在数组内，即使只有一个元素 | Array | 是       | -      |

```html
<body>
  <div></div>
  <div></div>
  <div></div>
  <li></li>
  <li></li>
  <p></p>

  <!-- JS -->
  <script>
    const div = document.querySelectorAll('div');
    const li = document.querySelectorAll('li');
    const p = document.querySelector('p');
    $dragEl([div, li, p]);
  </script>
</body>
```
