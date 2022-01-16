<img class="lyb" src="http://lengyibai.gitee.io/img-bed/img/lyb.png" style="width:200px;margin:0 auto;border-radius:50%" />

<p style="font-size:50px;font-weight:bold;width:100%;text-align:center;color:#fff;text-shadow:0 0 15px">冷弋白</p>
<p style="text-align:center;color:#aaa;position: relative;top:-10px;text-shadow:0 0 10px"><a href='https://wpa.qq.com/msgrd?v=3&uin=1329670984&site=qq&menu=yes' style='text-decoration: none;
'>点击此处联系我</a></p>
# 温馨提示

> 作者并不建议直接引入文件，推荐开发者在项目中新建`库文件`，按需复制需要的`函数`并粘贴进`库文件`，可避免作者更新，而导致项目报错
>
> 函数库地址：https://gitee.com/lengyibai/code-base

# 原生封装

## 本地存储

```js
const $lybP1 = {
  set(key, value) {
    localStorage.setItem(key, JSON.stringify(value));
  },
  get(key) {
    return JSON.parse(localStorage.getItem(key));
  },
  del(key) {
    localStorage.removeItem(key);
  },
  clear() {
    localStorage.clear();
  },
};
```

> 永久存储

| API                    | 描述         |
| ---------------------- | ------------ |
| $lybP1.set(key, value) | 设置值       |
| $lybP1.get(key)        | 获取值       |
| $lybP1.del(key)        | 删除指定值   |
| $lybP1.clear()         | 清空所有数据 |

## 返回数据类型

> 返回的数据类型为全小写的字符串

```js
$lybP2(o);
```

> 参数`o`：传递一个数据

具体操作如下

```js
console.log(
  $lybP2('5555'), //string
  $lybP2(123), //number
  $lybP2(false), //boolean
  $lybP2([5, 5]), //array
  $lybP2(function () {}), //function
  $lybP2({ a: 1 }), //object
);
```

## 控制全屏显示

> 点击指定按钮或指定条件下全屏显示

| 函数     | 描述             |
| -------- | ---------------- |
| $lybP3() | 调用函数开启全屏 |
| $lybP4() | 调用函数关闭全屏 |

## 随机数

> 随机生成指定范围的数据，生成的数字会包含两个参数

```js
$lybP5(min, max);
```

> 参数`min`：传递一个数字，最小值
>
> 参数`max`：传递一个数字，最大值
>
> 生成的数字会包含两个参数

## 对象去重

> 去掉数组内相同的对象

```js
$lybP6(arr);
```

> 参数`arr`：传递包含对象的是数组
>
> 参数`key`：根据指定属性来去重，一般为对象`id`值

具体操作如下

```js
const arr = [
  { id: 1, name: 'lyb' },
  { id: 1, name: 'lengyibai' },
  { id: 2, name: '冷弋白' },
];

console.log($lybP6(arr, 'id'));
```



# 功能类函数

## 获取图片路径

> 可判断是否为图片，并自定义不是图片和是图片后需要做的操作

```js
$lybS1(obj);
```

> 传递一个对象

| 对象属性 | 说明                                                                         | 类型     | 是否必填 | 默认值          |
| -------- | ---------------------------------------------------------------------------- | -------- | -------- | --------------- |
| el       | 传递已经通过*document.querSelector*获取的上传文件的按钮                      | DOM 元素 | 是       | -               |
| yes      | 用户选择的文件是图片后所做的操作，yes 会被传递一个参数，参数即这个图片的路径 | Function | 否       | null            |
| no       | 用户选择的文件不是图片后所做出的操作                                         | Function | 否       | null            |
| format   | 用于判断的格式                                                               | String   | 否       | '.jpeg.jpg.png' |

具体操作如下

```html
<body>
  <input type="file" name="" id="" />

  <!-- JS -->
  <script>
    const el = document.querySelector('input');
    $lybF1({
      el,
      no() {
        alert('不是');
      },
      yes(a) {
        document.body.style.backgroundImage = `url(${a})`; //给浏览器设置背景}
      },
      format: '.jpeg.jpg.png',
    });
  </script>
</body>
```

## 双击选中文字

> 双击选中元素内的所有文字

```js
$lybF2(el);
```

> 参数`el`：传递一个字符串或数组

具体操作如下

```html
<body>
  <div>我是标签div中的文字</div>
  <div class="div1">我是类名div1中的文字</div>
  <div id="div2">我是id名div2中的文字</div>

  <!-- JS -->
  <script>
    $lybF2('div');
    $lybF2('.div1');
    $lybF2('#div2');
    //或者
    $lybF2(['div', '.div1', '#div2']);
  </script>
</body>
```

## 防抖节流

### 使用方法

> 直接调用

```js
setInterval(
  $lybF(() => {
    console.log(666);
  }, 1000),
  100,
);
```

> 在函数内使用

```js
const lyb = $lybF(fn, 1000);
setInterval(() => {
  lyb();
}, 100);
```

> 在`Vue`内使用

```js
export default {
  data() {
    return {
      $lybF: null,
    };
  },
  created() {
    this.$lybF3 = $lybF(function () {}.bind(this), 250);
  },
  mounted() {
    setInterval(() => {
      this.$lybF3();
    }, 100);
  },
};
```

### 防抖

> 参数`fn`：传递一个函数
>
> 参数`wait`：传递一个毫秒

#### 延迟执行（常用）

> 函数调用后，如果在规定时间内没有再次调用，那么就执行函数

```js
$lybF3(fn, wait);
```

#### 立即执行

> 调用后立即执行一次
>
> 再次调用需要停止调用一定时间

```js
$lybF4(fn, wait);
```

### 节流

> 参数`fn`：传递一个函数
>
> 参数`wait`：传递一个毫秒

#### 延迟执行

> 每次调用需要等待一定时间才会执行
>
> 执行后才会进行下一次调用

```js
$lybF5(fn, wait);
```

#### 立即执行

> 调用后立即执行操作
>
> 再次调用需要等待一定时间

```js
$lybF6(fn, wait);
```

## 谷歌内核提示

> 如果浏览器版本未达到要求版本则提醒

```js
$lybF8(obj);
```

> 传递一个对象

| 对象属性 | 说明                                             | 类型     | 是否必填 | 默认值                               |
| -------- | ------------------------------------------------ | -------- | -------- | ------------------------------------ |
| v        | 要求版本                                         | Number   | 否       | 80                                   |
| yes      | 达到要求版本的提示，携带一个参数，参数即版本号   | Function | 否       | 弹窗显示浏览器版本号                 |
| no       | 未达到要求版本的提示，携带一个参数，参数即版本号 | Function | 否       | 弹窗提醒版本未达到要求，并显示版本号 |

具体操作如下

```js
$lybF8({
  v: 70,
  yes(v) {
    alert('您的浏览器版本为' + v);
  },
  no(v) {
    alert('您的浏览器版本为' + v + '，可能会影响体验');
  },
});
```

## 数字每三位加逗号

> 无详细介绍

```js
$lybF9(num);
```

> 参数`num`：传递一个数字

具体操作如下

```js
console.log($lybF9(666)); //1,000
```

## 复制到剪切板

> 只能通过鼠标事件触发

```js
$lybF10(str, fn);
```

> 参数`str`：传递一个字符串/数字
>
> 参数`fn`：复制成功后将会调用，并可以接收参数，为复制的内容

具体操作如下

```html
<body>
  <button>复制</button>

  <!-- JS -->
  <script>
    const btn = document.querySelector('button');
    btn.onclick = function () {
      $lybF10('666', function () {
        console.log(text); //666
      });
    };
  </script>
</body>
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
$lybF11(dates, fmt);
```

> 参数`date`：传递时间类型的数据
>
> 参数`fmt`：传递时间格式

具体操作如下

```js
const date = new Date('2000-05-09 09:30:05').getTime(); //假设这是后端传递过来的时间戳
console.log($lybF11(date, 'YYYY-MM-DD hh:mm:ss w n')); //2000-5-09 09:30:05 周几 时间戳
```

## 中文转拼音

> 返回一个数组，里面存着各种格式的拼音

```js
$lybF12(keyword);
```

> 参数`keyword`：传递汉字

具体操作如下

```js
console.log($lybF12('冷弋白')); //[ 'lengyibai', 'LengYiBai', 'lyb', 'LYB' ]
```

## 正则搜索

> 支持各种关键属性搜索、支持拼音搜索、支持拼音简写搜索、不区分大小写、支持模糊查询
>
> 如果输入框清空查询，则返回所有数据
>
> 注：依赖于`$lybF12`

```js
$lybF13(data, value, keys);
```

> 参数`data`：传递一个数组，里面存有对象形式的数据
>
> 参数`value`：支持传递数组和字符串和`-`分隔的字符串
>
> 参数`keys`：传递一个数组，代表搜索的属性
>

具体操作如下

```js
const obj = [
  { id:1, name: '张三', age: 20 },
  { id:2, name: '李四', age: 24 },
  { id:3, name: '王五', age: 24 },
  { id:4, name: '赵六', age: 24 },
];

console.log($lybF13(obj, 24, ['name', 'age']));
// [{ name: '李四', age: 24 }, { name: '王五', age: 24 }, { name: '赵六', age: 24 }]

console.log($lybF13(obj, ['zs'], ['name', 'age']));
// [{ name: '张三', age: 20 }]

console.log($lybF13(obj, 'LiS', ['name', 'age']));
// [ { name: '李四', age: 24 } ]

console.log($lybF13(obj, ['张三', 'ww'], ['name', 'age']));
// [ { name: '张三', age: 20 }, { name: '王五', age: 24 } ]

console.log($lybF13(obj, 'zs-lis', ['name', 'age']));
// [ { name: '张三', age: 20 }, { name: '李四', age: 24 } ]
```

### 针对Element UI的下拉多选进行查询

> 注：此时不需要依赖任何函数，但不支持拼音查询
>
> 如果下拉框清空查询，则需要进行一个判断，因为清空后组件会返回一个空数组，返回空数组则无法进行循环查询，则需要判断如果为空数组，则返回`[""]`去查询，这样查询才能返回所有数据

```js
$lybF13_arr(data, value, key);
```

> 参数`data`：传递一个数组，里面存有对象形式的数据
>
> 参数`value`：传递数组，数组内为需要搜索的值
>
> 参数`key`：传递字符串，代表搜索的属性

具体操作如下

```js
const obj = [
  { id:1, name: '张三', age: 20 },
  { id:2, name: '李四', age: 24 },
  { id:3, name: '王五', age: 24 },
  { id:4, name: '赵六', age: 24 },
];

console.log($lybF13(obj, ['张三', '李四'], ['name', 'age']));
// [ { name: '张三', age: 20 }, { name: '王五', age: 24 } ]
```

## 判断是否为指定类型的文件链接

> 目前只有图片和视频，可修改源码设置

```js
$lybF14(url, type);
```

> 参数`url`：传递字符串，代表文件路径
>
> 参数`type`：传递字符串，代表文件类型，目前有`image`和`video`

具体操作如下

```js
console.log($lybF14('文件.MP4', 'video')); //true
console.log($lybF14('文件.PNG', 'video')); //false
console.log($lybF14('文件.AVI', 'image')); //true
console.log($lybF14('文件.JPEG', 'image')); //false
```

## 全局替换指定字符串

> 替换字符串中所有匹配到的字符串

```js
$lybF15(str, match, rep);
```

> 参数`str`：传递字符串
>
> 参数`match`：匹配指定字符，使用`|`可匹配多个进行替换
>
> 参数`rep`：替换为指定字符，默认替换为空白字符

具体操作如下

```js
const id = 'id: GROUP@TGS#GROUP4X4JBGRH2';
console.log($lybF15(id, 'GROUP', '')); //@TGS#4X4JBGRH2
```

## 获取文件名

> 不会截取到`.`

```js
$lybF16(str);
```

> 参数`str`：传递字符串

具体操作如下

```js
console.log($lybF16('冷弋白.png'); //冷弋白
```

## 获取文件后缀名

> 可匹配多种后缀，如果后缀有大写字母，将自动转换为小写

```js
$lybF17(str);
```

> 参数`str`：传递字符串

具体操作如下

```js
console.log($lybF17('冷弋白.png')); //png
```

## 根据时间段问候

> 可修改问候内容

```js
$lybS18({
  a: '午夜好',
  b: '早上好',
  c: '上午好',
  d: '中午好',
  e: '下午好',
  f: '晚上好',
});
```

> 按照上面的格式，可修改任意一个

具体操作如下

```js
console.log($lybF18({ a: '都第二天了，该睡了' })); //根据你当前的时间段显示内容
/*
4点之前：午夜
10点之前：早上
12点之前：上午
14点之前：中午
18点之前：下午
0点之前：晚上
*/
```

## 排序支持数字&字母&时间&中文

> 支持数组和数组内的对象

```js
$lybF19(data, rev);
$lybF19(data, key, rev);
```

| 对象属性 | 说明                                  | 类型    | 是否必填                         | 默认值 |
| -------- | ------------------------------------- | ------- | -------------------------------- | ------ |
| data     | 无                                    | Array   | 是                               | -      |
| key      | 要进行排序的对象属性名                | String  | 只有数组：否<br />数组含对象：是 | -      |
| rev      | 正序还是倒序，`true`正序，`false`倒序 | Boolean | 否                               | true   |

具体操作如下

```js
var data = [
  { id: 3, abbr: 'pg', name: '苹果', time: '2019-04-25 12:00:22' },
  { id: 1, abbr: 'hw', name: '华为', time: '2019-04-22 10:00:19' },
  { id: 2, abbr: 'xm', name: '小米', time: '2019-04-22 10:00:18' },
];
let num = [1, 5, 3, 2, 4, 5, 3, 6, 9];

console.log($lybF18(data, 'name'));
/*
[
  { id: 1, abbr: 'hw', name: '华为', time: '2019-04-22 10:00:19' },
  { id: 3, abbr: 'pg', name: '苹果', time: '2019-04-25 12:00:22' },
  { id: 2, abbr: 'xm', name: '小米', time: '2019-04-22 10:00:18' }
]
*/
console.log($lybF18(data, false)); //[ 9, 6, 5, 5, 4, 3, 3, 2, 1 ]
```

## 字节格式化

> 一般用于上传文件时的文件大小或后端返回的文件大小
>
> 返回一个数组，数组元素分别是`['大小','单位','大小单位']`

```js
$lybF20(bytes);
```

> 参数`bytes`：传递文件字节大小

具体操作如下

```js
console.log($lybF20(2000)); //['1.95', 'KB', '1.95 KB']
console.log($lybF20(2048)); //['2.00', 'KB', '2.00 KB']
```

## 秒数格式化

> 返回一个数组，数组元素分别是`['时','分','秒','时:分:秒']`

```js
$lybF21(seconds);
```

> 参数`seconds`：传递秒数

具体操作如下

```js
console.log($lybF21(99999)); //[ 27, 46, 39, '27:46:39' ]
```

## 小数、百分比互转

> 如果是小数转百分比，会返回一个`Number`类型，需要手动添加`%`，并且会四舍五入
>
> 转为百分比只会保留一位小数

```js
$lybF22(i, ret);
```

> 参数`i`：传递字符串的百分比或数字
>
> 参数`ret`：传递数字，保留几位小数，默认不保留

具体操作如下

```js
console.log($lybF22(0.12345, 2)); //12.35
console.log($lybF22('12.34%')); //0.1234
```



# 样式类函数

## 自定义拖拽元素

> 自定义元素是否可拖拽
>
> 前提是父元素加了定位、被拖拽元素加了`绝对定位`

```js
$lybS1([dom,dom,...])
```

> 传递一个数组

| 说明                                                                                                                          | 类型  | 是否必填 | 默认值 |
| ----------------------------------------------------------------------------------------------------------------------------- | ----- | -------- | ------ |
| 传递一个或多个已经通过*document.querSelector*或*document.querSelectorAll*获取的元素，<br />需要存放在数组内，即使只有一个元素 | Array | 是       | -      |

具体操作如下

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
    $lybS1([div, li, p]);
  </script>
</body>
```

## 返回顶部

> 达到指定位置显示返回顶部按钮
>
> 点击按钮，以动画形式返回顶部

```js
$lybS3(obj);
```

> 传递一个对象

| 对象属性 | 说明                                              | 类型     | 是否必填 | 默认值                                                       |
| -------- | ------------------------------------------------- | -------- | -------- | ------------------------------------------------------------ |
| el       | 传递一个已经通过*document.querSelector*获取的元素 | DOM 元素 | 是       | -                                                            |
| y        | 达到多少像素显示返回顶部按钮                      | Number   | 否       | 300                                                          |
| fn1      | 返回顶部按钮如何出现                              | Function | 否       | 无需给按钮设置定位和偏移，已设置为左下角，从下往上的动画出现 |
| fn2      | 返回顶部按钮如何隐藏                              | Function | 否       | 无需给按钮设置定位和偏移，已设置为左下角，从上往下隐藏       |

具体操作如下

```html
<body>
  <div class="backTop">返回顶部</div>

  <!-- JS -->
  <script>
    const backTop = document.querSelector('.backTop');
    $lybS3({
      el: backTop,
      y: 300,
      fn1: () => {
        el.style.bottom = '-200px';
      },
      fn2: () => {
        el.style.bottom = '100px';
      },
    });
  </script>
</body>
```
