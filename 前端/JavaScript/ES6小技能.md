# 解构赋值

语法解释：
let {属性名:重命名} = 进行结构赋值的对象 || {};

    let obj={a:"小明",b:12};
    const {a:name,b:ahe} = obj || {};

> 解构的对象不能为`undefined`、`null`。否则会报错，故要给被解构的对象一个默认值。


# 合并数据

## 数组合并去重

    const a = [1,2,3]; 
    const b = [1,5,6]; 
    const c = a.concat(b);//[1,2,3,1,5,6]

> `Array.concat()` 
> 连接两个或多个数组，不会更改现有数组，而是返回一个新数组和结果

ES6

    const c = [...new Set([...a,...b])];
    //[1,2,3,5,6]

> `Set` 对象存储的值总是唯一的 （完成去重）
> `...` ES6 展开语法（完成合并）
> [展开语法 - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

## 对象合并去重

    const obj1 = { a:1, };
    const obj2 = { b:1, };
    const obj = Object.assign({}, obj1, obj2);
    //{a:1,b:1}

> `Object.assign()`方法用于将所有可枚举属性的值从一个或多个源对象分配到目标对象.
> 语法：
> ```Object.assign(目标对象, ...源对象)```
> [Object.assign() - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

ES6

    const obj = {...obj1,...obj2};//{a:1,b:1}

[展开语法 - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

# 拼接字符串

    const name = '小明'; 
    const score = 59; 
    let result = ''; 
    if(score > 60){ 
        result = `${name}的考试成绩及格`; 
    }
    else{ 
        result = `${name}的考试成绩不及格`; 
    }

在`${}`中可以放入任意的JavaScript表达式
优化：

    const result = `${name}
    			    ${score > 60 ? 
    			    '的考试成绩及格':'的考试成绩不及格'}`;

  # if 条件判断


    if(
        type == 1 ||
        type == 2 ||
        type == 3 ||
        type == 4 ||
    ){
       //...
    }

`includes()` 方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 `true`，否则返回 `false`。
[Array.prototype.includes() - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)

ES6 优化

    const condition = [1,2,3,4]; 
    if( condition.includes(type) ){ //... }

# 列表搜索

在项目中，一些没分页的列表的搜索功能由前端来实现，搜索一般分为精确搜索和模糊搜索。搜索也要叫过滤，一般用`filter`来实现。

    const a = [1,2,3,4,5];
    const result = a.filter( 
      item =>{
        return item === 3
      }
    )

如果是精确搜索，可以使用ES6中的`find`，当`find`方法中找到符合条件的项，就不会继续遍历数组。

    const a = [1,2,3,4,5];
    const result = a.find( 
      item =>{
        return item === 3
      }
    )

# 扁平化数组

    const deps = { 
    '采购部':[1,2,3], 
    '人事部':[5,8,12], 
    '行政部':[5,14,79], 
    '运输部':[3,64,105], 
    } 
    let member = []; 
    for (let item in deps){ 
        const value = deps[item]; 
        if(Array.isArray(value)){ 
        member = [...member,...value] 
        } 
    } 
    member = [...new Set(member)]

提取所有部门人员的id到一个数组中，ES6优化：
对象的属性值进行遍历 `Object.values`
[Object.values() - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/values)
多维数组进行扁平化处理 `flat`
使用`Infinity`作为`flat`的参数，可展开任意深度的嵌套数组
[Array.prototype.flat() - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)

    const deps = { 
        '采购部':[1,2,3], 
        '人事部':[5,8,12], 
        '行政部':[5,14,79], 
        '运输部':[3,64,105], 
    }
    let member = Object.values(deps).flat(Infinity)

> `flat`方法不支持IE浏览器。


# 获取对象属性值

访问对象的深嵌套属性时，要检查属性是否存在，然后才能获取属性的值，否则就会报错，ES5中借助 `&&` 来完成检查操作

    const name = obj.a && obj.a.b;

ES6可选链操作符使用 `?.` 来表示，可以判断操作符之前属性是否有效，从而链式读取对象的属性或返回 `undefined`

    const name = obj?.obj.a.b;

# 向对象添加属性

当给对象添加属性时，如果属性名是动态变化的

    let obj = {};
    let index = 1;
    let key = `topic${index}`;
    obj[key] = '话题内容';


