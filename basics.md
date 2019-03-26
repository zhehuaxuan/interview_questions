## 数组操作

![image-20190320232446939](./imgs/16999daad829de4d)

> 转自稻草叔叔的https://juejin.im/user/56e17630731956005cb7f501

数组是前端用的最多的数据结构，也是JavaScript中的内置对象。上图是笔者在掘金上面看到的由稻草叔叔整理的**对于Array对象罗列的最简明的思维导图**。

对于API的学习总是枯燥的，结合实际的场景，才能更好的消化，下面我会罗列场景，并对上述的函数铺开讲解。

#### 扁平化n维数组

```
[1,[2,3]].flat() //[1,2,3]
[1,[2,3,[4,5]].flat(2) //[1,2,3,4,5]
[1[2,3,[4,5[...]].flat(Infinity) //[1,2,3,4...n] 
```

array.prototype.flat(depth)，depth代表**指定要提取嵌套数组的结构深度，默认值为 1**。

*思考：如何使用其他方法来实现数组的降维？*

MDN给出替代方案，链接[地址](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)。这篇[JavaScript专题之数组扁平化](https://github.com/mqyqingfeng/Blog/issues/36)的文章也没出数组扁平化方案。

主要有**递归**和**非递归**两种方式：

##### 递归

```javascript
// 方法 1
var arr = [1, [2, [3, 4]]];
function flatten(arr) {
    var result = [];
    for (var i = 0, len = arr.length; i < len; i++) {
        if (Array.isArray(arr[i])) {
            //判断如果数组元素本身也是数组，递归调用
            result = result.concat(flatten(arr[i]))
        }
        else {
            result.push(arr[i])
        }
    }
    return result;
}
console.log(flatten(arr))
```

使用reduce

```javascript
function flatten(arr) {
    return arr.reduce(function(prev, next){
        return prev.concat(Array.isArray(next) ? flatten(next) : next)
    }, [])
}
```

使用...拓展运算符

```javascript
function flatten(arr) {
    while (arr.some(item => Array.isArray(item))) {
        arr = [].concat(...arr);
    }
    return arr;
}
```

##### 非递归

**使用toString**

```javascript
var r = [1,[2,3,[4,5]]].toString()  //1,2,3,4,5  仅限于数组的元素都是数字
var res = r.split(",");
```

运用stack

```javascript
// 不使用递归，使用 stack 无限反嵌套多层嵌套数组
var arr1 = [1,2,3,[1,2,3,4, [2,3,4]]];
function flatten(input) {
  const stack = [...input];
  const res = [];
  while (stack.length) {
    // 使用 pop 从 stack 中取出并移除值
    const next = stack.pop();
    if (Array.isArray(next)) {
      // 使用 push 送回内层数组中的元素，不会改动原始输入 original input
      stack.push(...next);
    } else {
      res.push(next);
    }
  }
  // 使用 reverse 恢复原数组的顺序
  return res.reverse();
}
flatten(arr1);// [1, 2, 3, 1, 2, 3, 4, 2, 3, 4]
```



#### 去重

```
Array.from(new Set([1,2,3,3,4,4])) //[1,2,3,4]
[...new Set([1,2,3,3,4,4])] //[1,2,3,4]
```

主要利用Set对象来处理去重，这里重点是Array.from函数的使用。Array.from是数组的构造函数，我在这边需要强调两点：

> 1. from函数的第一个参数，可以只是类数组或者字符串
> 2. from函数的第二个参数是一个callback函数，用于对生成数组进行map操作

写两个例子

```
Array.from('foo'); 
// ["f", "o", "o"]
let s = new Set(['foo', window]); 
Array.from(s); 
// ["foo", window]
```

*思考题：如何实现函数，对数组去重？*

两种情况：

> 数组乱序：双重遍历数组，使用一个结果数组存储去重数据，外层循环遍历数组将符合条件的加入；
>
> 数组有序：直接遍历数组，比较相邻的数据是否重复

#### 排序

```
[1,2,3,4].sort((a, b) => a - b); // [1, 2,3,4],默认是升序
console.log([1,1000,2,3].sort((a, b) => a - b)); // [1, 2, 3, 1000] 升序
console.log([1,1000,2,3].sort());//[1, 1000, 2, 3]按照unicode编码顺序排序
```

注：使用sort函数进行数字大小比较时，需要在sort中自定义比较函数，如果没有定义，那么sort会按照字符编码的顺序进行排序。

*思考题：V8排序的原理是什么？*

可以参考[JavaScript专题之解读 v8 排序源码](https://github.com/mqyqingfeng/Blog/issues/52)

V8的排序全部都是原生实现，采用的算法跟数组的长度有关，当数组长度小于等于 10 时，采用插入排序，大于 10 的时候，采用快速排序。

要求手撕排序算法的代码，这部分可以移步[这里](todo)。这里的疑问主要是为什么需要选择10，什么是原地算法？

#### 求最大值

```
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

```
eval([1,2,3,4].join('+')] //10 
[1,2,3,4].arr.reduce((prev, cur) =>prev + cur) //10
```

#### 合并

```
[1,2,3,4].concat([5,6]) //[1,2,3,4,5,6]
[...[1,2,3,4],...[4,5]] //[1,2,3,4,5,6]
let a = [1,2,3,4];
a.push(...[1,2,3,4]);//[1,2,3,4,1,2,3,4]
```

#### 判断是否包含值

包含某个值

1. 使用`indexOf(searchElement,start)`进行查询，返回符合条件的第一个值的下标
2. 使用`find(callback)`返回符合条件的第一个值，否则返回`undefined`
3. 使用`some`如果符合条件返回`true`，不符合条件返回`false`
4. 使用`includes(searchElement,fromIndex)`进行筛选，`includes`的特点是可以是集合

```javascript
var array = [1, 4, 9, 16];
var index = array.indexOf(9);
console.log(index); //2
index = array.find((item)=>item==9);
console.log(index);//9
index = array.some((item)=>item==9);
console.log(index);//true
var pets = ['cat', 'dog', 'bat'];
console.log(pets.includes('cat')); //true
```

#### 每一项设置值

典型的使用`map()`函数，`map()` 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

```javascript
var array1 = [1, 4, 9, 16];
// pass a function to map
const map1 = array1.map(x => x * 2);
console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

#### 每一项是否满足/有一项满足

```javascript
[1,2,3].every(item=>{return item>2}) //false
[1,2,3].some(item=>{return item>2}) //true
```

and和or的区别。让我想到了Promise对象的使用。

#### 过滤数组

`filter()` 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。  

```javascript
var words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6); // ["exuberant", "destruction", "present"]
```

#### 对象和数组转化

```javascript
Object.keys({name:'张三',age:14}) //['name','age']
Object.values({name:'张三',age:14}) //['张三',14]
Object.entries({name:'张三',age:14}) //[[name,'张三'],[age,14]]
```
