##  原始类型(Primitive Type)

```
boolean
null
undefined
number
string
symbol
```

## null与undefined的区别

```
console.log(null==undefined); // true  因为两者都默认转换成了false
console.log(typeof undefined); // "undefined"  
console.log(typeof null);  //"object"  
console.log(null===undefined); // false "==="表示绝对相等，null和undefined类型是不一样的，所以输出“false”

null 
	Null类型，代表“空值”，代表一个空对象指针，
	使用typeof运算得到 “object”，所以你可以认为它是一个特殊的对象值。
	
undefined
	Undefined类型，当一个声明了一个变量未初始化时，得到的就是undefined
	
null表示没有对象，即该处不应该有值

    1） 作为函数的参数，表示该函数的参数不是对象
    2） 作为对象原型链的终点

undefined表示缺少值，即此处应该有值，但没有定义

    1）定义了形参，没有传实参，显示undefined
    2）对象属性名不存在时，显示undefined
    3）函数没有写返回值，即没有写return，拿到的是undefined
    4）写了return，但没有赋值，拿到的是undefined

null和undefined转换成number数据类型
    null 默认转成 0
    undefined 默认转成 NaN

```

## typeof 和 instanceof 的区别

```
# typeof 对于原始类型来说，除了 null 都可以显示正确的类型
	typeof 1 // 'number'
    typeof '1' // 'string'
    typeof undefined // 'undefined'
    typeof true // 'boolean'
    typeof Symbol() // 'symbol'
    
    // typeof 对于对象来说，除了函数都会显示 object
   	typeof [] // 'object'
    typeof {} // 'object'
    typeof console.log // 'function'
    
# 想判断一个对象的正确类型，这时候可以考虑使用 `instanceof`，因为内部机制是通过原型链来判断
	
	const Person = function() {}
    const p1 = new Person()
    p1 instanceof Person // true

    var str = 'hello world'
    str instanceof String // false

    var str1 = new String('hello world')
    str1 instanceof String // true
    
    // 对于原始类型来说，你想直接通过 `instanceof` 来判断类型是不行的
    
```

## == 和 === 的区别

```
# `==` 来说，如果对比双方的类型不一样的话，就会进行类型转换
	1. 首先会判断两者类型是否**相同**。相同的话就是比大小了
    2. 类型不相同的话，那么就会进行类型转换
    3. 会先判断是否在对比 `null` 和 `undefined`，是的话就会返回 `true`
    4. 判断两者类型是否为 `string` 和 `number`，是的话就会将字符串转换为 `number`
    5. 判断其中一方是否为 `boolean`，是的话就会把 `boolean` 转为 `number` 再进行判断
    6. 判断其中一方是否为 `object` 且另一方为 `string`、`number` 或者 `symbol`，是的话就会把 `object` 转为原始类型再进行判断
    
# `===` 来说就简单多了，就是判断两者类型和值是否相同
```

## 深浅拷贝

```
对象类型在赋值的过程中其实是复制了地址，从而会导致改变了一方其他也都被改变的情况。通常在开发中我们不希望出现这样的问题，我们可以使用浅拷贝来解决这个情况

	let a = {
      age: 1
    }
    let b = a
    a.age = 2
    console.log(b.age) // 2
	
# 浅拷贝
	可以通过 `Object.assign` 来解决这个问题,只会拷贝所有的属性值到新的对象中，如果属性值是对象的话，拷贝的是地址，所以并不是深拷贝。
	
	let a = {
      age: 1
    }
    let b = Object.assign({}, a)
    a.age = 2
    console.log(b.age) // 1
	
	// 还可以通过展开运算符 `...` 来实现浅拷贝
	
    let a = {
      age: 1
    }
    let b = { ...a }
    a.age = 2
    console.log(b.age) // 1
    
# 深拷贝 通常可以通过 JSON.parse(JSON.stringify(object)) 来解决
    let a = {
      age: 1,
      jobs: {
        first: 'FE'
      }
    }
    let b = JSON.parse(JSON.stringify(a))
    a.jobs.first = 'native'
    console.log(b.jobs.first) // FE
    
 	局限性:
 		- 会忽略 `undefined`
        - 会忽略 `symbol`
        - 不能序列化函数
        - 不能解决循环引用的对象
```

## 原型 prototype

```
- `Object` 是所有对象的爸爸，所有对象都可以通过 `__proto__` 找到它
- `Function` 是所有函数的爸爸，所有函数都可以通过 `__proto__` 找到它
- 函数的 `prototype` 是一个对象
- 对象的 `__proto__` 属性指向原型， `__proto__` 将对象和原型连接起来组成了原型链
```

