---
title: 数组
date: 2020-5-12
categories: [web]
tags: [array]


---



# 数组类



### 数组合并

```auto
const arr1 = [1, 2, 3]
const arr2 = [4, 5, 6]
const arr3 = [7, 8, 9]
const arr = [...arr1, ...arr2, ...arr3]
```

`arr1.concat(arr2, arr3)`同样可以实现合并，但是用了`...`操作符之后就不会再想用其他的了~

### 数组去重

```auto
const arr = [1, 1, 2, 2, 3, 4, 5, 5]
const newArr = [...new Set(arr)]
```

`new Set(arr)`接受一个数组参数并生成一个set结构的数据类型。set数据类型的元素不会重复且是`Array Iterator`，所以可以利用这个特性来去重。

### 数组并集

```js
const union = function (a, b, k) {
    return a.concat(b.filter(i => (k ? !a.map(i => i[k]).includes(i[k]) : !a.includes(i))))
}
```

示例：

```js
let a = [1, 2, 3, 4, 5]
let b = [1, 2, 4, 5, 6]
union(a, b) //[1,2,3,4,5,6]

// 场景2：
let a1 = [
    { id: 1, name: '张三', age: 20 },
    { id: 2, name: '李四', age: 21 },
    { id: 3, name: '小二', age: 23 }
]
let b1 = [
    { id: 2, name: '李四', age: 21 },
    { id: 4, name: '小明', age: 24 },
    { id: 5, name: '小红', age: 25 }
]

// 通过 id 获取并集
union(a1, b1, 'id')
/*
[
  {id: 1, name: "张三", age: 20}
  {id: 2, name: "李四", age: 21}
  {id: 3, name: "小二", age: 23}
  {id: 4, name: "小明", age: 24}
  {id: 5, name: "小红", age: 25}
]
*/
```

### 数组交集

```js
const intersection = function (a, b, k) {
    return a.filter(t => (k ? b.map(i => i[k]).includes(t[k]) : b.includes(t)))
}
```

示例：

```js
let a = [1, 2, 3, 4, 5]
let b = [1, 2, 4, 5, 6]
intersection(a, b) // [1,2,4,5]

// 场景2：
let a1 = [
    { id: 1, name: '张三', age: 20 },
    { id: 2, name: '李四', age: 21 },
    { id: 3, name: '小二', age: 23 }
]
let b1 = [
    { id: 2, name: '李四', age: 21 },
    { id: 4, name: '小明', age: 24 },
    { id: 5, name: '小红', age: 25 }
]
intersection(a1, b1, 'id') //[ { id: 2, name: '李四', age: 21 }]
```

### 数组差集

```js
const except = function (a, b, k) {
    return [...a, ...b].filter(i => ![a, b].every(t => (k ? t.map(i => i[k]).includes(i[k]) : t.includes(i))))
}
```

示例：

```js
let a = [1, 2, 3, 4, 5]
let b = [1, 2, 4, 5, 6]

except(a, b) // [3,6]

let a1 = [
    { id: 1, name: '张三', age: 20 },
    { id: 2, name: '李四', age: 21 },
    { id: 3, name: '小二', age: 23 }
]
let b1 = [
    { id: 2, name: '李四', age: 21 },
    { id: 4, name: '小明', age: 24 },
    { id: 5, name: '小红', age: 25 }
]


except(a1, b1, 'id')
/*
[
  {id: 1, name: "张三", age: 20}
  {id: 3, name: "小二", age: 23}
  {id: 4, name: "小明", age: 24}
  {id: 5, name: "小红", age: 25}
]
*/
```

## 数组常用遍历

数组常用遍历有 `forEach、every、some、filter、map、reduce、reduceRight、find、findIndex` 等方法，很多方法都可以达到同样的效果。数组方法不仅要会用，而且要用好。要用好就要知道什么时候用什么方法。

### 遍历的混合使用

`filter`、`map`方法返回值仍旧是一个数组，所以可以搭配其他数组遍历方法混合使用。注意遍历越多效率越低~

```auto
const arr = [1, 2, 3, 4, 5]
const value = arr
    .map(item => item * 3)
    .filter(item => item % 2 === 0)
    .map(item => item + 1)
    .reduce((prev, curr) => prev + curr, 0)
```

### 检测数组所有元素是否都符合判断条件

```auto
const arr = [1, 2, 3, 4, 5]
const isAllNum = arr.every(item => typeof item === 'number')
```

### 检测数组是否有元素符合判断条件

```auto
const arr = [1, 2, 3, 4, 5]
const hasNum = arr.some(item => typeof item === 'number')
```

### 找到第一个符合条件的元素/下标

```auto
const arr = [1, 2, 3, 4, 5]
const findItem = arr.find(item => item === 3) // 返回子项
const findIndex = arr.findIndex(item => item === 3) // 返回子项的下标
```





## 各种数组遍历的方法

### **`for`** 语句

代码:

```auto
var arr = [1,2,4,6]
for(var i = 0, len = arr.length; i < len; i++){
    console.log(arr[i])
}
```

### **`forEach`** 语句

代码:

```auto
var arr = [1,5,8,9]
arr.forEach(function(item) {
    console.log(item);
})
```

### **`for-in`** 语句

一般会使用`for-in`来遍历对象的属性的,不过属性需要 

代码:

```auto
var obj = {
    name: 'test',
    color: 'red',
    day: 'sunday',
    number: 5
}
for (var key in obj) {
    console.log(obj[key])
}
```

### **`map`** 方法 (不改变原数组)

`map` 方法会给原数组中的每个元素都按顺序调用一次 callback 函数。callback 每次执行后的返回值（包括 undefined）组合起来形成一个新数组。 callback 函数只会在有值的索引上被调用；那些从来没被赋过值或者使用 delete 删除的索引则不会被调用。让数组通过某种计算产生一个新数组,影射成一个新的数组,

代码:

```auto
var arr = [1,2,3]
var firearr = arr.map(v => v * 5)

var arr = [
{name:"zs",age:12},
{name:"ls",age:13},
{name:"ww",age:14},
];

var item =  arr.map((ele,index)=>{
return {
name:ele.name+"__技术部员工",
age:ele.age+10
}
})

console.log(item);
```

### **`filter`** 方法 (不改变原数组)

`filter` 为数组中的每个元素调用一次 callback 函数，并利用所有使得 callback 返回 true 或 等价于 true 的值 的元素创建一个新数组。callback 只会在已经赋值的索引上被调用，对于那些已经被删除或者从未被赋值的索引不会被调用。那些没有通过 callback 测试的元素会被跳过，不会被包含在新数组中。筛选出过滤出数组中符合条件的项,组成新数组.

代码:

```auto
var arr = [2,3,4,5,6]
var morearr = arr.filter(function (number) {
    return number > 3
})
```

### **`every`** 方法

every 方法为数组中的每个元素执行一次 callback 函数，直到它找到一个使 callback 返回 false（表示可转换为布尔值 false 的值）的元素。如果发现了一个这样的元素，every 方法将会立即返回 false。否则，callback 为每一个元素返回 true，every 就会返回 true。检测数组中的每一项是否符合条件,如果每一项都符合条件,就会返回true,否则返回false,有点像遍历数组且操作callback。只会为那些已经被赋值的索引调用。不会为那些被删除或从来没被赋值的索引调用。

代码:

```auto
var arr = [1,2,3,4,5]
var result = arr.every(function (item, index) {
    return item > 0
})
```

### **`some`** 方法

some 为数组中的每一个元素执行一次 callback 函数，直到找到一个使得 callback 返回一个“真值”（即可转换为布尔值 true 的值）。如果找到了这样一个值，some 将会立即返回 true。否则，some 返回 false。callback 只会在那些”有值“的索引上被调用，不会在那些被删除或从来未被赋值的索引上调用。检查数组中是否有某些项符号条件,如果有一项就返回true,否则返回false,有点像遍历数组或者操作.

代码:

```auto
var arr = [1,2,3,4,5]
var result = arr.some(function (item,index) {
    return item > 3
})
```