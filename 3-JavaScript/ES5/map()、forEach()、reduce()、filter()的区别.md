- **map()**

  **map()**方法按照原始数组元素顺序依次处理元素，返回一个新的数组，数组中的元素为原始数组调用函数处理后的值。可看作是对原数组进行**映射**。

  注意：**map()**方法不会对空数组进行检测。

  ```javascript
  array.map(function(currentValue,index,arr), thisValue)
  //参数：当前元素、当前元素的索引、当前元素所属的数组
  
  var wallets = people.map(function (dude) {
    return dude.wallet;
  });
  ```

- **forEach()**

  **forEach()**方法用于**遍历**数组的每个元素，将元素传给回调函数。

  注意：**forEach()**对于空数组是不会调用回调函数的。 

  ```javascript
  array.forEach(function(currentValue, index, arr), thisValue)
  //参数：当前元素、当前元素的索引、当前元素所属的数组
  
  people.forEach(function (dude) {
    dude.pickUpSoap();
  });
  ```

- **reduce()**

  **reduce()**方法是让数组中的前项和后项做某种计算，并**累计**最终值。

  ```javascript
  array.reduce(function(total, currentValue, currentIndex, arr), initialValue)初始值
  //参数：初始值(计算结束的返回值)、当前元素、当前元素的索引、当前元素所属的数组
  
  var totalMoney = wallets.reduce(function (countedMoney, wallet) {
    return countedMoney + wallet.money;
  }, 0);
  ```

- **filter()**

  **filter()**方法会**筛选**出数组中符合条件的项，组成一个新数组。

  ```javascript
  array.filter(function(currentValue,index,arr), thisValue)
  //参数：当前元素、当前元素的索引、当前元素所属的数组
  
  var fatWallets = wallets.filter(function (wallet) {
    return wallet.money > 100;
  });
  ```

#### 总结

- 相同点：
  1. 都会循环遍历数组中的每一项；
  2. **map()**、**forEach()**和**filter()**方法里每次执行匿名函数都支持3个参数，参数分别是：当前元素、当前元素的索引、当前元素所属的数组；
  3. 匿名函数中的this都是指向window；
  4. 只能遍历数组。
- 不同点：
  1. **map()**速度比**forEach()**快；
  2. **map()**和**filter()**会返回一个新数组，不对原数组产生影响；**forEach()**不会产生新数组，返回undefined；**reduce()**函数是把数组缩减为一个值(比如求和、求积)；
  3. **map()**里可以用return，而**forEach()**里用return不起作用，**forEach()**不能用break，会直接报错；
  4. **reduce()**有4个参数，第一个参数为初始值。

> 参考文章：
>
> 1. [forEach()和map()的区别：](https://blog.csdn.net/boysky0015/article/details/72983766)
> 2. [JS中的forEach、$.each、map方法推荐](https://www.cnblogs.com/chaoyuehedy/p/6905422.html)
> 3. [ES5中新增的Array方法详细说明](http://www.zhangxinxu.com/wordpress/?p=3220)
> 4. [如何形象地解释 JavaScript 中 map、foreach、reduce 间的区别？](https://www.zhihu.com/question/24927450)