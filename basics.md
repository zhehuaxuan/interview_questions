## 数组操作

![image-20190320232446939](./imgs/16999daad829de4d)

> 转自稻草叔叔的https://juejin.im/user/56e17630731956005cb7f501

数组是前端用的最多的数据结构，也是JavaScript中的内置对象。上图是笔者在掘金上面看到的由稻草叔叔整理的**对于`Array`对象罗列的最简明的思维导图**。    

对于API的学习总是枯燥的，结合实际的场景，才能更好的消化，下面我会罗列场景，并对上述的函数铺开讲解。

#### 扁平化n维数组

```javascript
[1,[2,3]].flat() //[1,2,3]
[1,[2,3,[4,5]].flat(2) //[1,2,3,4,5]
[1,[2,3,[4,5]]].toString()  //'1,2,3,4,5'
[1[2,3,[4,5[...]].flat(Infinity) //[1,2,3,4...n] 
```

array.prototype.flat(depth)，depth代表**指定要提取嵌套数组的结构深度，默认值为 1**。

*思考：如何使用其他方法来实现数组的降维？*

mdn给出了替代方案，链接地址：<https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat>

主要可以使用concat，reduce函数，也可以使用非递归的方式(使用stack)实现。

#### 去重

```javascript
Array.from(new Set([1,2,3,3,4,4])) //[1,2,3,4]
[...new Set([1,2,3,3,4,4])] //[1,2,3,4]
```

主要利用Set对象来处理去重，这里重点是Array.from函数的使用。Array.from是数组的构造函数，我在这边需要强调两点：

> 1. from函数的第一个参数，可以只是类数组或者字符串
> 2. from函数的第二个参数是一个callback函数，用于对生成数组进行map操作

写两个例子🌰：

```javascript
Array.from('foo'); 
// ["f", "o", "o"]
let s = new Set(['foo', window]); 
Array.from(s); 
// ["foo", window]
```

*思考题：如何实现函数，对数组去重？*

#### 排序

```javascript
[1,2,3,4].sort((a, b) => a - b); // [1, 2,3,4],默认是升序
[1,2,3,4].sort((a, b) => b - a); // [4,3,2,1] 降序
```

思考题1：js对于字符串是如何排序的？

思考题2：v8排序的原理是什么？

#### 求最大值

```javascript
Math.max(...[1,2,3,4]) //4
[1,2,3,4].reduce( (prev, cur,curIndex,arr)=> {
 return Math.max(prev,cur);
}) //4
```

reduce函数的参数是一个reducer函数，

**reducer** 函数接收4个参数:

1. Accumulator (acc) (累计器)
2. Current Value (cur) (当前值)
3. Current Index (idx) (当前索引)
4. Source Array (src) (源数组)

reduce思想的典型应用就是Redux的reducer

#### 求和

```javascript
eval([1,2,3,4].join('+')] //10 
[1,2,3,4].arr.reduce((prev, cur) =>prev + cur) //10
```

### 合并

```javascript
[1,2,3,4].concat([5,6]) //[1,2,3,4,5,6]
[...[1,2,3,4],...[4,5]] //[1,2,3,4,5,6]
let a = [1,2,3,4];
a.push(...[1,2,3,4]);//[1,2,3,4,1,2,3,4]
```

#### 判断是否包含某个值



#### 每一项设置值





#### 每一项是否满足/有一项满足



#### 过滤数组



#### 对象和数组转化



## 手动实现instanceof

主要考察原型链的原理

```javascript
/**
** @param source 对象
** @param target 构造函数
**/
function isInstanceof(source,target){
    var right = target.prototype;//函数的原型
    var left = source.__proto__;//对象的__proto__
    while(left){
        //如果source对象的__proto__指向target的原型
        if(left==right){
            return true;
        }
        //查找原型链上的对象
        left = left.__proto__;
    }
    return false;
}
```



## 手动实现apply和call





## 手动实现bind





## 手动模拟实现new Object()





## 对象继承的几种方法？优缺点？

#### 原型链继承

```javascript
function Parent(){}
function Son(){}
Son.prototype = new Parent();
```

**缺点：**

> 1.父对象的引用属性能够被子对象影响
>
> 2.不能向父对象传参

#### 构造器继承

```javascript
function Parent();
function Son(){
    Parent.call(this);
}
```

**缺点：**

> 

### 讲一讲EventLoop？



### 如何实现对象的浅拷贝？应用场景？



### 如何实现深拷贝









