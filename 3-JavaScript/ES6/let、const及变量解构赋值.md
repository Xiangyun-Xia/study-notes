> **声明：本文内容依照阮一峰老师[ECMAScript 6 入门](http://es6.ruanyifeng.com/)**一书所总结。

#### let和const

- 相同点
  1. 都存在块级作用域
  2. 都不存在变量声明提升
  3. 都会造成“暂时性死区”
  4. 在一个作用域下不可重复声明
- 不同点
  1. const一旦声明必须立即赋值
  2. const声明的变量指向的内存地址不得改动。

#### 变量解构赋值

- 数组的解构赋值

  - 解构成功

    ```javascript
    let [a, b, c] = [1, 2, 3];
    ```

  - 解构不成功

    ```javascript
    let [foo] = [];
    ```

  - 不完全解构

    ```javascript
    let [x, y] = [1, 2, 3];
    ```

  - 默认值

    ```javascript
    let [foo = true] = [];
    ```

  - 解构条件：只要某种数据结构具有 Iterator 接口，都可以采用数组形式的解构赋值。

- 对象的解构赋值

  - 与数组的区别：对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

  - 应用：可以很方便地将现有对象的方法，赋值到某个变量。

    ```javascript
    let { log, sin, cos } = Math;
    ```

- 字符串的解构赋值

  - 原理：字符串被转换成了一个类似数组的对象。

    ```javascript
    const [a, b, c, d, e] = 'hello';
    ```

  - 类似数组的对象都有一个`length`属性，因此还可以对这个属性解构赋值。

    ```javascript
    let {length : len} = 'hello';
    len // 5
    ```

- 数值和布尔值的解构赋值

  ```javascript
  let {toString: s} = 123;
  s === Number.prototype.toString // true
  
  let {toString: s} = true;
  s === Boolean.prototype.toString // true
  ```

- 函数参数的解构赋值

  ```javascript
  [[1, 2], [3, 4]].map(([a, b]) => a + b);
  // [ 3, 7 ]
  ```

