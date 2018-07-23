本文内容参考：[ECMAScript 6 入门](http://es6.ruanyifeng.com/#docs/object#Object-assign)

#### 背景

在上一个项目开发中，看到项目内存在很多`Object.assign()`写法的代码，由于之前没有接触过，感觉比较疑惑。通过网上查询发现，这是ES6对对象进行的扩展之一，于是系统的了解了一下ES6中对对象进行的扩展。

#### 学习

- 属性的简洁表示法

  ES6 允许直接写入变量(变量需要存在)和函数，作为对象的属性和方法。

  ```javascript
  let birth = '2000/01/01';
  const Person = {
    name: '张三',
    //等同于birth: birth
    birth,
    // 等同于hello: function ()...
    hello() { console.log('我的名字是', this.name); }
  };
  ```

- 属性名表达式

  ES6 允许字面量定义对象时，使用中括号+变量名作为对象的属性名，即把表达式放在方括号内。

  ```javascript
  let lastWord = 'last word';
  
  const a = {
    'first word': 'hello',
    [lastWord]: 'world'
  };
  
  a['first word'] // "hello"
  a[lastWord] // "world"
  a['last word'] // "world"
  ```

- Object.is()

  ES5 比较两个值是否相等，只有两个运算符：相等运算符（`==`）和严格相等运算符（`===`）。它们都有缺点，前者会自动转换数据类型，后者的`NaN`不等于自身，以及`+0`等于`-0`。JavaScript 缺乏一种运算，在所有环境中，只要两个值是一样的，它们就应该相等。

  ES6 提出`“Same-value equality”`（同值相等）算法，用来解决这个问题。`Object.is`就是部署这个算法的新方法。它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。

  不同之处只有两个：一是`+0`不等于`-0`，二是`NaN`等于自身。

  ```javascript
  +0 === -0 //true
  NaN === NaN // false
  
  Object.is(+0, -0) // false
  Object.is(NaN, NaN) // true
  ```

- Object.assign()

  `Object.assign`方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。

  `Object.assign`方法的第一个参数是目标对象，后面的参数都是源对象。

  ```javascript
  const target = { a: 1 };
  
  const source1 = { b: 2 };
  const source2 = { c: 3 };
  
  Object.assign(target, source1, source2);
  target // {a:1, b:2, c:3}
  ```

  **注意**：

  1. 如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。
  2. 如果只有一个参数，`Object.assign`会直接返回该参数。
  3. 如果该参数不是对象，则会先转成对象，然后返回。
  4. 由于`undefined`和`null`无法转成对象，所以如果它们作为参数，就会报错。
  5. 如果非对象参数出现在源对象的位置（即非首参数），那么处理规则有所不同。首先，这些参数都会转成对象，如果无法转成对象，就会跳过。这意味着，如果`undefined`和`null`不在首参数，就不会报错。
  6. 其他类型的值（即数值、字符串和布尔值）不在首参数，也不会报错。但是，除了字符串会以数组形式，拷贝入目标对象，其他值都不会产生效果。
  7. `Object.assign`拷贝的属性是有限制的，只拷贝源对象的自身属性（不拷贝继承属性），也不拷贝不可枚举的属性（`enumerable: false`）。

  **常见用途**：

  1. 为对象添加属性

     ```javascript
     class Point {
       constructor(x, y) {
         Object.assign(this, {x, y});
       }
     }
     ```

  2. 为对象添加方法

     ```javascript
     Object.assign(SomeClass.prototype, {
       someMethod(arg1, arg2) {
         ···
       },
       anotherMethod() {
         ···
       }
     });
     
     // 等同于下面的写法
     SomeClass.prototype.someMethod = function (arg1, arg2) {
       ···
     };
     SomeClass.prototype.anotherMethod = function () {
       ···
     };
     ```

  3. 克隆对象

     ```javascript
     function clone(origin) {
       return Object.assign({}, origin);
     }
     ```

  4. 合并多个对象

     ```javascript
     const merge =
       (target, ...sources) => Object.assign(target, ...sources);
     
     const merge =
       (...sources) => Object.assign({}, ...sources);
     ```

  5. 为属性指定默认值

- Object.keys()，Object.values()，Object.entries()