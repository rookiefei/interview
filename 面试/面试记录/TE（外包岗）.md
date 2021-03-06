
## 2017.05.13
### 电面
* 介绍ES6新特性
* 解释原型链，以及如何获取对象的原型
* 解释同源策略，以及跨域的方式，扩展到`JSONP`并解释其原理和缺点
* 周一去面试...

### 笔试

__代码输出__：考察变量声明提升
```javascript
var a = 100;
var fn = ()=>{
    console.log(a);
    var a = 200;
    console.log(a);
}
fn();// undefined, 200
console.log(a); // 100
var a;
console.log(a); // 100
var a = 300;
console.log(a); // 300
```
__代码输出__：考察this
```javascript
var obj1 = {
  	name: "obj1",
  	fn(){
      	console.log(this.name);
  	}
};
var obj2 = { name: "obj2" };
var obj3 = { name: "obj3" };
obj1.fn(); // obj1
var newFn = obj1.fn;
newFn(); // "" 注意这里不是undefined
newFn.call(obj2); // obj2
obj3.fn = newFn;
obj3.fn(); // obj3

var newFn = obj1.fn.bind(obj1);
newFn(); // obj1
newFn.call(obj2); // obj1，注意这个地方是强绑定，所以一直为obj1
obj3.fn = newFn;
obj3.fn(); // obj1 ，同上
```
__代码输出__：考察ES6的原型
```
class A {
    say(){
        console.log("foo");
    }
}

let a = new A();

A.prototype = {
    say(){
        console.log("bar");
    }
}

a.say(); // "foo"
let b = new A();
b.say(); // "foo"
```
这道题虽然答对了，但是却理解错了。ES6中的class是语法糖，构造函数的`prototype`是无法修改其他指向的。


__函数实现__：实现一个函数，函数每调用一次则其返回值加1，要求使用箭头函数，考察闭包
```javascript
let fn = (()=>{
    let count = 0;
    return ()=>{
        return count++;
    }
})();
```

__冒泡排序__：考察基础算法
```javascript
let bubbleSort = function(arr){
    var len = arr.length;
    for (var i = 0; i < len; ++i){
        for (var j = 0; j < len - i; ++j){
            if (arr[j+1] > arr[j]){
                var tmp = arr[j+1];
                arr[j+1] = arr[j];
                arr[j] = tmp;
            }
        }
    }
}
```

__Web安全__：列举你知道的Web安全漏洞和防范方法
* XSS，
* CSRF

__性能优化__：列举前端可以采取的常见优化方式
* 减少HTTP请求
* 页面加载时间
* 代码效率

__跨域__：什么是同源策略，列举跨域方案
* 同源限制：
* 跨域方案：
  * `document.domain`
  * `CORS`
  * `JSONP`
  * 服务器中转

__算法__：列举你知道的算法，以及时间空间复杂度
* 冒泡
* 选择
* 插入
* 快速

## 面试
这个全是凭记忆整理了。
* 解释笔试试题思路
* HTTP相关知识
  * `host`首部行的作用
  * `Expries`和`CaChe-Controle`的区别
  * `Cookie`中的`HttpOnly`
* `ES6`的特性
* `Vue`的使用，是否了解内部原理
* `PHP`和`NodeJS`的掌握情况
* `Event Loop`和`Web Worker`
* 有没有用过抓包工具
* 学习途径和方法
* 离职原因，上一份工作的开发流程和工作任务
* 最后让在Mac上敲代码，十分紧张敲了两行就没敲了。

## 总结
面试官十分好，面试完直接就说他这边OK了，然后介绍了工作内容和团队情况，主要负责JS功能实现，然后说HR下午负责谈薪酬。最后由于薪酬的问题不打算去，不过这次面试感觉还是很不错的。