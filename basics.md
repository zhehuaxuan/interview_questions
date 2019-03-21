## 数组操作

![image-20190320232446939](./imgs/16999daad829de4d)

> 转自稻草叔叔的https://juejin.im/user/56e17630731956005cb7f501

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









