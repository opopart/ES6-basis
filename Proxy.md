# Proxy

​				用于修改某些操作的默认行为，等同于在语言层面进行修改。

​				语法： `var proxy =  new Proxy(target, handler)`

​							target：所要拦截的目标对象

​							handler：对象，描述拦截行为

​				==注意==：要使Proxy起作用，必须针对Proxy进行操作



## 实例方法



### get()

​		用于拦截某个属性的读取操作，该方法可以继承

​		==注意==：如果一个属性不可配置 或 不可写 ， 则该属性不能被代理， 通过Proxy对象访问该属性会报错

### set()

​		用于拦截某个属性的赋值操作

​		==注意==：如果目标对象自身的某个属性不可写也不可配置，那么set不得改变这个属性的值，只能返回同

​					样的值，否则报错

### apply()

​		用于拦截函数的调用、call和apply操作

​		接受三个参数，目标对象，目标对象的上下文(this)，目标对象的参数数组

### has()

​		用于拦截HasProperty操作，即判断对象是否具有某个属性(继承属性也包括)时，该方法生效

​		==注意==：原对象不可配置或禁止扩展，has拦截会报错， has对拦截for...in循环无效

### construct()

​		用于拦截new命令，返回值必须是一个对象，否则报错

​		接受两个参数，target：目标对象，args：构建函数的参数对象

### deleteProperty()

​		用于拦截delete操作，如果该方法抛出错误或者返回false，即表示当前属性无法被删除

​		==注意==：目标对象自身的不可配置属性不能被该方法删除，否则报错

### defineProperty()

​		用于拦截Object.defineProperty操作

​		==注意==：目标对象不可扩展 => 则不能添加目标对象中不存在的属性，否则报错

​					不可写 或 不可配置=> 该方法不能改变这两个设置 

### getOwnPropertyDescriptor()		

​		用于拦截Object.getOwnPropertyDescriptor(),返回一个属性描述对象或undefined

### getPrototypeOf()

​		用于拦截获取对象原型，即一下操作：

​				`Object.prototype.__proto__`

​				`Object.prototype.isPrototypeOf()`

​				`Object.getPrototypeOf()`

​				`Reflect.getPrototypeOf()`

​				`instanceof`

​		返回值需为对象或者null，否则报错。若目标对象不可拓展，则目标对象的原型对象

### isExtensible()

​		用于拦截Object.isExtensible操作

​		==具有强制性==：返回值必须与目标对象的isExtensible属性保持一致。否则报错

### ownKeys()

​		拦截对象自身属性的读取操作，即一下操作

​				Object.getOwnPropertyNames()

​				Object.getOwnPropertySymbols()

​				Object.keys()

### preventExtensions()

​		用于拦截Object.preventExtensions()，返回一个布尔值，若不是则转为布尔值

​		==强制性==：只有目标对象不可扩展时才返回true

### setPrototypeOf()

​		用于拦截Object,setPrototypeOf方法

​		若目标对象不可扩展 ，该方法不得改变目标对象的原型

​		返回布尔值，若不是则转为布尔值



### Proxy.revocable()

​		返回一个可以取消的Proxy实例

​		let  {proxy, revoke} = Proxy.revocable(target, handler)

​		proxy属性：Proxy实例

​		revoke属性：一个函数，执行后可以取消Proxy实例，执行后再访问Proxy实例会报错

​		使用场景：目标对象不允许访问，必须通过代理访问，一旦访问结束，就收回代理权



### this问题

​		目标对象内部的this关键字会指向Proxy代理

