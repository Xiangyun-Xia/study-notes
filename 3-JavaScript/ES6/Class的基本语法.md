## Class的基本语法

> 参考文章：[ECMAScript 6 入门](http://es6.ruanyifeng.com/#docs/class)

#### 概述

基本上，ES6 的`class`可以看作只是一个语法糖，它的绝大部分功/能，ES5 都可以做到，新的`class`写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

举个栗子：

```javascript
// ES5
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

// ES6
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}

// 即ES5的构造函数Point，对应ES6的Point类的构造方法。
```

#### 基本语法

- 在类的实例上面调用方法，其实就是调用原型上的方法。

  ```javascript
  class B {}
  let b = new B();
  
  b.constructor === B.prototype.constructor // true
  ```

- 由于类的方法都定义在`prototype`对象上面，所以类的新方法可以添加在`prototype`对象上面。`Object.assign`方法可以很方便地一次向类添加多个方法。

  ```javascript
  class Point {
    constructor(){
      // ...
    }
  }
  
  Object.assign(Point.prototype, {
    toString(){},
    toValue(){}
  });
  ```

- `prototype`对象的`constructor`属性，直接指向“类”的本身，这与 ES5 的行为是一致的。

  ```javascript
  Point.prototype.constructor === Point // true
  ```

- 不同的是，类的内部所有定义的方法，都是不可枚举的；而ES5的写法中，函数原型上的方法是可枚举的。

  ```javascript
  // ES6
  class Point {
    constructor(x, y) {
      // ...
    }
  
    toString() {
      // ...
    }
  }
  
  Object.keys(Point.prototype)
  // []
  Object.getOwnPropertyNames(Point.prototype)
  // ["constructor","toString"]
  
  //ES5
  var Point = function (x, y) {
    // ...
  };
  
  Point.prototype.toString = function() {
    // ...
  };
  
  Object.keys(Point.prototype)
  // ["toString"]
  Object.getOwnPropertyNames(Point.prototype)
  // ["constructor","toString"]
  ```

- 类必须使用`new`调用，否则会报错。这是它跟普通构造函数的一个主要区别，后者不用`new`也可以执行。

  ```javascript
  class Foo {
    constructor() {
      return Object.create(null);
    }
  }
  
  Foo()
  // TypeError: Class constructor Foo cannot be invoked without 'new'
  ```

- 与函数一样，类也可以使用表达式的形式定义。
- 类不存在变量提升（hoist），这一点与 ES5 完全不同。

#### Class的继承

- Class 可以通过`extends`关键字实现继承，这比 ES5 的通过修改原型链实现继承，要清晰和方便很多。

  ```javascript
  class Point {
  }
  
  class ColorPoint extends Point {
  }
  ```

- 在子类的构造函数中，只有调用`super`之后，才可以使用`this`关键字，否则会报错。这是因为子类实例的构建，基于父类实例，只有`super`方法才能调用父类实例。

  ```javascript
  class Point {
    constructor(x, y) {
      this.x = x;
      this.y = y;
    }
  }
  
  class ColorPoint extends Point {
    constructor(x, y, color) {
      this.color = color; // ReferenceError
      super(x, y);
      this.color = color; // 正确
    }
  }
  ```

- 父类的静态方法，也会被子类继承。

  ```javascript
  class A {
    static hello() {
      console.log('hello world');
    }
  }
  
  class B extends A {
  }
  
  B.hello()  // hello world
  ```


