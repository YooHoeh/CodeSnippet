<!-- TOC -->

- [CodeSnippet](#codesnippet)
  - [通用](#通用)
    - [文件头模板注释](#文件头模板注释)
  - [CSS](#css)
    - [清除浮动](#清除浮动)
  - [算法](#算法)
    - [二分查找](#二分查找)
  - [DOM & BOM](#dom--bom)
    - [在原网页跳转而不留下历史记录，同时可以使浏览器返回上一页无效](#在原网页跳转而不留下历史记录同时可以使浏览器返回上一页无效)
    - [在关闭页面前弹出确认框](#在关闭页面前弹出确认框)
  - [工具类](#工具类)
    - [柯里化函数](#柯里化函数)
    - [将数字转为 RMB 格式（每三位加一个逗号）的字符串](#将数字转为-rmb-格式每三位加一个逗号的字符串)
    - [将字符串每隔`step`位添加一个`symbol`](#将字符串每隔step位添加一个symbol)
    - [挑选出数组中重复的项生成一个新数组](#挑选出数组中重复的项生成一个新数组)
    - [解析身份证可提取信息](#解析身份证可提取信息)

<!-- /TOC -->

# CodeSnippet

> Userful code snippet like some amazing logic or typical file description or any others

## 通用

### 文件头模板注释

```js
/**
 * Author: YooHoeh
 * Description:
 * Date: Create in ${TIME} ${DATE}
 * Github:github.com/YooHoeh
 * Email:yoohoeh@163.com
 */
```

## CSS

### 清除浮动

```css
.clearfix::after {
  content: "";
  display: none;
  clear: both;
}
```

## 算法

### 二分查找

```js
/**
 * 二分查找
 * @param {Array} arr 待查找数组,数组需要已按照从小到大排序
 * @param {Any} x 待查找项
 * @return {Any} 如果找到返回位置下标，不存在返回`-1`
 */
function bSearch(arr,x) {
  let left = 0, //查找左边界
      right = arr.length-1,,  //查找右边界
      guess; //猜测位置（中间位置）
  while(left <= right) {
    guess = Math.floor( (1+right) / 2);
    if ( arr[guess] === x ) return guess
    else if (arr[left] > x ) right = guess - 1
    else left = guess + 1;
   }
   return -1
}
```

## DOM & BOM

### 在原网页跳转而不留下历史记录，同时可以使浏览器返回上一页无效

```js
location.replace("http://github.com/");
```

### 在关闭页面前弹出确认框

```js
window.onbeforeunload = function(e) {
  e = e || window.event;
  // 兼容 IE8 和 Firefox 4 之前的版本
  if (e) {
    e.returnValue = "关闭提示";
  }
  // Chrome, Safari, Firefox 4+, Opera 12+ , IE 9+
  return "关闭提示";
};
```

## 工具类

### 柯里化函数

```js
function curry(fn) {
  let curArgs = arguments[1] && arguments.length > 1 ? arguments[1] : []; //判断是否传入了参数
  return function() {
    let args = Array.from(arguments);
    if (curArgs.length + arguments.length < fn.length) {
      //判断已经传入的参数是否和所需的要参数个数相等
      return curry(fn, curArgs.concat(args)); //不相等则再次柯里化
    } else {
      //相等则直接调用函数
      return fn.apply(undefined, curArgs.concat(args));
    }
  };
}
```

### 将数字转为 RMB 格式（每三位加一个逗号）的字符串

```js
/**
 * 将数字转为RMB格式（每三位加一个逗号）的字符串
 * `最大支持17位！`
 * @param {Number} str 传入需要的数字
 */
function num2RMB(str) {
  const re = str => [...str].reverse().join(""); //将字符串反转
  str += ""; //将传入的数字转为字符串
  let tmp = ""; //输出的结果；
  for (let i = 1; i <= str.length; i++) {
    tmp += re(str)[i - 1];
    if (i % 3 == 0 && i != str.length) {
      tmp += ",";
    }
  }
  return re(tmp);
}
```

### 将字符串每隔`step`位添加一个`symbol`

```js
/**
 * 将字符串每隔`step`位添加一个`symbol`
 * @param {String} str 原字符串
 * @param {Number} step 每隔多少位
 * @param {String} symbol 添加的符号
 * @param {Number=} dirction 起始方向：`-1`为从左往右，`1`为从右往左，默认为`1`
 */
function insertSymbol(str, step, symbol, dirction = 1) {
  const re = str => [...str].reverse().join(""); //将字符串反转
  str += ""; //如果传入的是数字则转为字符串
  str = dirction === 1 ? str : re(str);
  let tmp = ""; //输出的结果；
  for (let i = 1; i <= str.length; i++) {
    tmp += re(str)[i - 1];
    if (i % step == 0 && i != str.length) {
      tmp += symbol;
    }
  }
  return dirction === 1 ? re(tmp) : tmp;
}
```

### 挑选出数组中重复的项生成一个新数组

```js
/**
 * 挑选出数组中重复的项生成一个新数组
 * @param {Array} arr 源数组
 * @return {Array} 重复项组成的数组
 */
function selectRepeatItem(arr) {
  var obj = {};
  var result = [];
  arr.map(function(i) {
    obj[i] == undefined ? (obj[i] = 0) : (obj[i] += 1);
  });
  for (var key in obj) {
    obj[key] == 0 && result.push(key - 0);
  }
  return result;
}
```

### 解析身份证可提取信息

```js
/**
 * 
 * @param {*} UUserCard  身份证号
 * @param {*} num  1、出生日期  2、性别  3、年龄
 */
let getIdInfo= (UUserCard, num) => {
    if (num == 1) {
        //获取出生日期
        birth = UUserCard.substring(6, 10) + "-" + UUserCard.substring(10, 12) + "-" + UUserCard.substring(12, 14);
        return birth;
    }
    if (num == 2) {
        //获取性别
        if (parseInt(UUserCard.substr(16, 1)) % 2 == 1) {
            //男
            return "男";
        } else {
            //女
            return "女";
        }
    }
    if (num == 3) {
        //获取年龄
        var myDate = new Date();
        var month = myDate.getMonth() + 1;
        var day = myDate.getDate();
        var age = myDate.getFullYear() - UUserCard.substring(6, 10) - 1;
        if (UUserCard.substring(10, 12) < month || UUserCard.substring(10, 12) == month && UUserCard.substring(12, 14) <= day) {
            age++;
        }
        return age;
    }
}
```

