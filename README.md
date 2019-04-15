<!-- TOC -->

- [CodeSnippet](#codesnippet)
  - [Common](#common)
    - [Author infomatiom for all of file](#author-infomatiom-for-all-of-file)
  - [JavaScript](#javascript)
    - [在原网页跳转而不留下历史记录，同时可以使浏览器返回上一页无效](#在原网页跳转而不留下历史记录同时可以使浏览器返回上一页无效)
    - [在关闭页面前弹出确认框](#在关闭页面前弹出确认框)
    - [柯里化函数](#柯里化函数)
    - [将数字转为 RMB 格式（每三位加一个逗号）的字符串](#将数字转为-rmb-格式每三位加一个逗号的字符串)

<!-- /TOC -->

# CodeSnippet

> Userful code snippet like some amazing logic or typical file description or any others

## Common

### Author infomatiom for all of file

```js
/**
 *Author: YooHoeh
 *Description:
 *Date: Create in ${TIME} ${DATE}
 *Github:github.com/YooHoeh
 *Email:yoohoeh@163.com
 */
```

## JavaScript

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
    if (i % 3 == 0 && i != re(str).length) {
      tmp += ",";
    }
  }
  return re(tmp);
}
```
