一. JavaScript基础

### 1.数据类型

#### 1.1 数值（Number）

* 在JS中所有的整数和浮点数都是Number类型
* JS中的数值并不是无限大的，当数值超过一定范围后会显示近似值
* **Infinity 是一个特殊的数值表示无穷 **
* 所以在JS中进行一些精度比较高的运算时要十分注意
* **NaN 也是一个特殊的数值，表示非法的数值**

```javascript
let a = 10
a = 10.5
a = Infinity
a = 1.11111111111111111111111111111111111111111111
a = 0.0000000000000000000000000000000000001
a = 0.1 + 0.2
a = 1 - "a" // NaN (Not a Number)
a = NaN
```

#### 1.2 大整数（BigInt） 

* 大整数用来表示一些比较大的整数 
* **大整数使用n结尾**，它可以表示的数字范围是无限大 

`a = 99999999999999999999999999999999999999999999999999n `

### 2. 字符串（String）

* 模板字符串
  * **使用反单引号` 来表示模板字符串**
  * 模板字符串中可以嵌入变量
  * 使用typeof检查一个字符串时会返回 "string"

```javascript
            let name = "猪八戒"

            let str = `你好，${name}`
```

### 3. 流程控制

#### 3.1 代码块

* 使用 {} 来创建代码块，**代码块可以用来对代码进行分组**
  * 同一个代码中的代码，就是同一组代码，一个代码块中的代码**要么都执行要么都不执行**
* **let 和 var**
  *  **在JS中，使用let声明的变量具有块作用域**
  * 在代码块中声明的变量无法在代码块的外部访问
  * **使用var声明的变量，不具有块作用域**

```javascript
{
	var a = 10
}
console.log(a)
```

![1662806701188](C:\Users\79426\AppData\Local\Temp\1662806701188.png)



### 4. 对象

#### 4.1 对象的属性

*  属性名 
  * 通常属性名就是一个字符串，所以属性名可以是任何值，没有什么特殊要求，但是如果你的**属性名太特殊**了，不能直接使用，**需要使用[]来设置**，虽然如此，但是我们还是强烈建议属性名也按照标识符的规范命名
  * 也可以使用**符号（symbol）**作为属性名，来添加属性，获取这种属性时，也必须使用symbol，**使用symbol添加的属性，通常是那些不希望被外界访问的属性**
  * **使用[]去操作属性时，可以使用变量** 
* 属性值 
  * 对象的属性值可以是任意的数据类型，也可以是一个对象 
* 使用typeof检查一个对象时，会返回object 



#### 4.2 对象字面量

* 对象字面量 
  * 可以直接使用{} 来创建对象 
  * 使用{}所创建的对象，可以直接向对象中添加属性 

语法：

​	{

​		属性名：属性值

​		[属性名]：属性值

​	}

```javascript
let mySymbol = Symbol()

        let obj2 = {
            name:"孙悟空", 
            age:18,
            ["gender"]:"男",
            [mySymbol]:"特殊的属性",
            hello:{
                a:1,
                b:true
            }
        }
```



#### 4.3 枚举属性

* 枚举属性，指将对象中的所有的属性全部获取 

##### for-in语句

语法：

​	**for(let propName in 对象)**{

​		语句...

​	}

* for-in的循环体会执行多次，有几个属性就会执行几次，每次执行时，都会将一个属性名赋值给我们所定义的变量
* 注意：并不是所有的属性都可以枚举，比如 使用符号添加的属性 

```javascript
        let obj = {
            name:'孙悟空',
            age:18,
            gender:"男",
            address:"花果山",
            [Symbol()]:"测试的属性" // 符号添加的属性是不能枚举
        }

        for(let propName in obj){
            console.log(propName, obj[propName])
        }
```



#### 4.4 可变类型

*  原始值都属于不可变类型，一旦创建就无法修改
* 在内存中不会创建重复的原始值

```js
		let a = 10 
        let b = 10
        a = 12 
	// 当我们为一个变量重新赋值时，绝对不会影响其他变量
```

>  - 对象属于可变类型
>  - 对象创建完成后，可以任意的添加删除修改对象中的属性
>  - 注意：
>      - 当对两个对象进行相等或全等比较时，比较的是对象的内存地址
>      - 如果有两个变量同时指向一个对象，
>          通过一个变量修改对象时，对另外一个变量也会产生影响



#### 4.5 改变量和改对象

> **修改对象**
>
> - 修改对象时，如果有其他变量指向该对象,则所有指向该对象的变量都会受到影响
>   - a.name = "Tom"
>   - a = {}
>
> **修改变量**
>
> * 修改变量时，只会影响当前的变量
>   * a = 10
>
> >在使用变量存储对象时，很容易因为改变变量指向的对象，提高代码的复杂度

> **所以通常情况下，声明存储对象的变量时会使用const**
>
> **注意：**
>  	**const只是禁止变量被重新赋值，对对象的修改没有任何影响** 

```js
			const obj = {
                name: "孙悟空",
            }
```



#### 4.5 方法（method） 

* 方法（method）
  * 当一个对象的属性指向一个函数
  * 那么我们就称这个函数是该对象的方法
  * 调用函数就称为调用对象的方法

```js
        let obj = {}

        obj.name = "孙悟空"
        obj.age = 18

        // 函数也可以成为一个对象的属性
        obj.sayHello = function(){
            alert("hello")
        }

        console.log(obj)

        obj.sayHello()
```



### 5.函数

#### 5.1 函数

* 函数（Function）

  *  函数也是一个对象
  * 它具有其他对象所有的功能
  * 函数中可以存储代码，且可以在需要时调用这些代码

* 语法： 

  function 函数名(){

  ​	语句...

  }

* 调用函数： 

  * 调用函数就是执行函数中存储的代码 

  * 语法：

    ​	函数对象()

* 使用typeof检查函数对象时会返回function 

```js
// 创建一个函数对象
        function fn(){
            console.log("萨瓦迪卡")
            console.log("阿尼哈撒有")
        }

        console.log(typeof fn)
```



#### 5.2 函数的创建方式

*  函数的定义方式： 

  * 1.函数声明 

    ```JS
    function 函数名(){
    
    	语句...
    
    }
        
    function fn(){
    	console.log("函数声明所定义的函数~")
    }
    ```

  * 2.函数表达式 

    ```JS
    const 变量 = function(){
    	语句...
    }
            
    const fn2 = function(){
        console.log("函数表达式")
    }
    ```

  * 3.箭头函数 

    ```JS
    () => {
    	语句...
    	}
        
    const fn3 = () => {
        console.log("箭头函数")
    }
    
    const fn4 = () => console.log("箭头函数")
    ```



#### 5.3 参数

* 形式参数

  *  在定义函数时，可以在函数中指定数量不等的形式参数（形参）
  * 在函数中定义形参，就相当于在函数内部声明了对应的变量但是没有赋值

* 实际参数

  * 在调用函数时，可以在函数的()传递数量不等的实参

  *  实参会赋值给其对应的形参

    *  参数：

      	1.  如果实参和形参数量相同，则对应的实参赋值给对应的形参

                      2.  如果**实参多于形参**，则**多余的实参不会使用**
                
                      3. 如果**形参多于实参**，则**多余的形参为undefined**

    * 参数的类型：

      ​	JS中不会检查参数的类型，可以传递任何类型的值作为参数

```js
1.函数声明
        function 函数名([参数]){
            语句...
        }
2.函数表达式
    const 变量 = function([参数]){
        语句...
    }
3.箭头函数
    ([参数]) => {
        语句...
    }
```

##### 5.3.1 箭头函数的参数

```js
<script>
    const fn = (a, b) => {
        console.log("a =", a);
        console.log("b =", b);
    }
    // 当箭头函数中只有一个参数时，可以省略()
	//const fn2 = (a) => {
    const fn2 = a => {
        console.log("a =", a);
    }
    // fn2(123)
    // 定义参数时，可以为参数指定默认值
    // 默认值，会在没有对应实参时生效
    const fn3 = (a=10, b=20, c=30) => {
        console.log("a =", a);
        console.log("b =", b);
        console.log("c =", c);
    }
    fn3(1, 2)
</script>
```

##### 5.3.2 对象作为参数

```js
原始代码 1 ：
		// 3. 执行函数        
		function fn(a){
            console.log("a =", a)
            // a = {name : 孙悟空}
            console.log(a.name)
            // 孙悟空
            
        }
        // 1. 对象可以作为参数传递
        let obj = {name:"孙悟空"}

        // 2. 传递实参时，传递并不是变量本身，而是变量中存储的值
        // 相当于将 name:"孙悟空" ——> fn(name:"孙悟空")
        fn(obj)
```

![1662885629980](C:\Users\79426\AppData\Local\Temp\1662885629980.png)

```js
问题 1 ：形参和实参指向同一个对象，在函数里修改对象
		function fn(a){
            a.name = "猪八戒"
            // 修改对象时，如果有其他变量指向该对象则所有指向该对象的变量都会受到影响
            // 注意： 此时 obj 和 a 指向同一个对象
            console.log(a)
        }
        let obj = {name:"孙悟空"}
        fn(obj)

		console.log(obj)//结果是多少？
```

![1662885472099](C:\Users\79426\AppData\Local\Temp\1662885472099.png)

```js
问题 2 ： 形参和实参指向不同对象，在函数里修改对象
		function fn(a){
            a = {} 
            // 将新对象赋值给变量a，a指向的是一个新的对象
            // 修改变量时，只会影响当前的变量
            a.name = "猪八戒"
            // 注意： 此时 obj 和 a 指向不同对象
            console.log(a)
        }
        let obj = {name:"孙悟空"}
        fn(obj)

		console.log(obj)//结果是多少？
```

![1662886049445](C:\Users\79426\AppData\Local\Temp\1662886049445.png)

```js
原始代码 2 ：
		// 3. 执行函数        
		function fn(a){
            a.name = "猪八戒"
            console.log(a)
        }
        let obj = {name:"孙悟空"}
        fn(obj)
        function fn2(a = 1){
            console.log("a =", a)
        }

        fn2() //a = 1
```

```js
问题 1 ：给 a 的默认值传一个对象
		function fn2(a = {name:"沙和尚"}){
            console.log("a =", a)
            a.name = "唐僧"
            console.log("a =", a)
        }

        fn2() // 沙和尚 唐僧
```

![1662886556547](C:\Users\79426\AppData\Local\Temp\1662886556547.png)

```js
问题 2 ：打印两次 fn2() ，看两次调用的默认对象是否是同一个对象
		function fn2(a = {name:"沙和尚"}){
            console.log("a =", a)
            a.name = "唐僧"
            console.log("a =", a)
        }

        fn2() // 沙和尚 唐僧
		fn2() // 沙和尚 唐僧 or 唐僧 唐僧 ？
```

![1662886764920](C:\Users\79426\AppData\Local\Temp\1662886764920.png)

**说明：两次调用的默认对象不是同一个对象，函数每次调用，都会重新创建默认值** 

```js
问题 3 ：在外面创建对象再调用
		let obj2 = {name:"沙和尚"}
        
        function fn2(a = obj2){
            console.log("a =", a)
            a.name = "唐僧"
            console.log("a =", a)
        }

        fn2() // 沙和尚 唐僧
        fn2() // 唐僧 唐僧
```

![1662886941139](C:\Users\79426\AppData\Local\Temp\1662886941139.png)

**说明：**

​	**如果是直接将字面量写在形参位置，那么每次都会创建一个新对象，每次改都是独立的**

​	**如果是在外面创建的对象，形参 = 外面创建的对象，那么每次调用都是共用一个对象**

##### 5.3.3 函数作为参数

```js
 		function fn(a){
            console.log("a =", a)
            // a()
        }

        /* 
            在JS中，函数也是一个对象（一等函数）
                别的对象能做的事情，函数也可以
        */

        let obj = {name:"孙悟空"}
        fn(obj)// a = {name : 孙悟空}
```

```js
		function fn2(){
            console.log("我是fn2")
        }

        fn(fn2)
		// a 指向 fn2 ，把函数作为参数传递给另一个函数
```

![1662887884717](C:\Users\79426\AppData\Local\Temp\1662887884717.png)

```js
在函数里直接调另一个传入的函数
		function fn(a){
             a()
        }
        function fn2(){
            console.log("我是fn2")
        }

        fn(fn2)
		//我是fn2
```

```js
在函数里创建匿名函数、箭头函数
		fn(function(){
            console.log("我是匿名函数~")
        })

        fn(()=>console.log("我是箭头函数"))
```



#### 5.4 箭头函数的返回值

* 箭头函数的返回值可以直接写在箭头后
*  如果直接在箭头后设置对象字面量为返回值时，对象字面量必须使用()括起来

```js
        const sum = (a, b) => a + b

        const fn = () => ({name:"孙悟空"})

        let result = sum(123, 456)

        result = fn()

        console.log(result)
```



#### 5.5 Window 对象

* **Window对象**
  * 在浏览器中，浏览器为我们提供了一个window对象，可以直接访问
  *  **window对象代表的是浏览器窗口**，通过该对象可以对浏览器窗口进行各种操作
    * 除此之外**window对象还负责存储JS中的内置对象和浏览器的宿主对象**
  *  window对象的属性可以通过window对象访问，也可以直接访问
  * **函数就可以认为是window对象的方法**

```js
 window.a = 10 
// 向window对象中添加的属性会自动成为全局变量
```

* **var**
  * var 用来声明变量，作用和let相同，但是**var不具有块作用域**
  * *在全局中使用var声明的变量，都会作为window对象的属性保存**
  *  **使用function声明的函数，都会作为window的方法保存**
  * *使用let声明的变量不会存储在window对象中**，而存在一个秘密的小地方（无法访问）**
  * ** **var虽然没有块作用域，但有函数作用域**

```js
var b = 20 // window.b = 20
```



#### 5.6 提升

* 变量的提升
  * **使用var声明的变量，它会在所有代码执行前被声明**
  * 所以我们可以在变量声明前就访问变量
* 函数的提升
  * **使用函数声明创建的函数，会在其他代码执行前被创建**
  *  所以我们可以在函数声明前调用函数
* ***let声明的变量实际也会提升，但是在赋值之前解释器禁止对该变量的访问***



#### 5.7 立即执行函数

**希望可以创建一个只执行一次的匿名函数** 

* 在开发中应该尽量减少直接在全局作用域中编写代码！（no var）
* 所以我们的代码要尽量编写在局部作用域（let）
* **如果使用let声明的变量，可以使用{}来创建块作用域**

```js
        {
            let a = 10
        }
```

* **立即执行函数（IIFE）**

  * **立即是一个匿名的函数，并它只会调用一次**
  * 可以利用IIFE来创建一个一次性的函数作用域，避免变量冲突的问题

* **语法：**

  **（ function{} ）（）或 （  function{}（））**

  **function开头的代码会被提升，所以需要一个名字才能创建**

  ​	**在function前面套上括号，就以括号开头了，不会被提升，但此时还未执行**

  ​	函数调用：

  ​		函数对象后面加上括号  ： 函数对象（）

```js
(function(){
    let a = 10
    console.log(111)
})();
或
(function(){
    let a = 20
    console.log(222)
}())
```

**注意：格式为（xxx)(yyy) 时，JS解析会认为（xxx)是函数，会调用（xxx)，若（xxx)不是函数，则会报错，所以要注意写分号**

#### 5.8 this

* this

  * 函数在执行时，JS解析器每次都会传递进一个隐含的参数

  * 这个参数就叫做 this

  *  this会指向一个对象

    * **this所指向的对象会根据函数调用方式的不同而不同**
      1. **以函数形式调用时，this指向的是window**
      2. **以方法的形式调用时，this指向的是调用方法的对象**

    ​            ...

  * 通过this可以在方法中引用调用方法的对象

#### 5.9 箭头函数的this

* 箭头函数：

  * ([参数]) => 返回值

* 例子：

  * 无参箭头函数：() => 返回值

  *  一个参数的：a => 返回值

  *  多个参数的：(a, b) => 返回值

  *   只有一个语句的函数：() => 返回值

  *  只返回一个对象的函数：() => ({...})

  * 有多行语句的函数：

    () => {

    ​        ....    
            return 返回值
     }

* **箭头函数没有自己的this，它的this由外层作用域决定**

* **箭头函数的this和它的调用方式无关**

##### 1.在对象外，以函数形式调用

```js
function fn() {
    console.log("fn -->", this)
    //window
}
const fn2 = () => {
    console.log("fn2 -->", this) // 总是window
    //window
}
            // fn() // window
            // fn2() // window
```

##### 2.在对象外，以方法形式调用

```js
const obj = {
    name:"孙悟空",
    fn, // fn:fn
    fn2,
}

obj.fn() // obj
obj.fn2() // window--->箭头函数没有自己的this，它的this由外层作用域决定,箭头函数的this和它的调用方式无关
```

##### 3.在对象外，通过对象.方法调用

```js
const obj = {
    name:"孙悟空",
    fn, // fn:fn
    fn2,
    sayHello(){
        console.log(this.name)
       // 孙悟空
    }
}
obj.sayHello() 
```

##### 4.在对象中，通过函数调用

```js
const obj = {
    name:"孙悟空",
    fn, // fn:fn
    fn2,
    sayHello(){
        console.log(this.name)
    //注意点1：
       	function t(){
    		console.log("t -->", this)
            // 2. 所以t里this是window
		}
		t()// 1. t是以函数形式调用
   	//注意点2：
        const t2 = () => {
    		console.log("t2 -->", this)
            //2. 所以t2里this是obj
		}
		t2()
        //1. 这是箭头函数，箭头函数的this是他的外层函数
    }
}
obj.sayHello() 
```

#### 5.10 严格模式

JS运行代码的模式有两种：

* 正常模式
  *  默认情况下代码都运行在正常模式中， 在正常模式，语法检查并不严格
  * 它的原则是：能不报错的地方尽量不报错
  *  这种处理方式导致代码的运行性能较差
* 严格模式
  * 在严格模式下，语法检查变得严格
    1. 禁止一些语法
    2.  更容易报错
    3.  提升了性能
* 在开发中，应该尽量使用严格模式，
  * 这样可以将一些隐藏的问题消灭在萌芽阶段， 同时也能提升代码的运行性能

```js
        "use strict" // 全局的严格模式

        let a = 10

        // console.log(a)

        function fn(){
            "use strict" // 函数的严格的模式
        }
```

### 6. 面向对象

#### 6.1 类

* 使用Object创建对象的问题：

1.  无法区分出不同类型的对象
2. 不方便批量创建对象

* 在JS中可以通过类（**class**）来解决这个问题：

​    1.  类是对象模板，可以将对象中的属性和方法直接定义在类中
        定义后，就可以直接通过类来创建对象
    2.  通过同一个类创建的对象，我们称为同类对象
        **可以使用instanceof来检查一个对象是否是由某个类创建**
        如果某个对象是由某个类所创建，则我们称该对象是这个类的实例

* 语法：
  * class 类名 {} // 类名要使用大驼峰命名
  *  const 类名 = class {}  
* ​    通过类创建对象
  *  new 类()

#### 6.2 属性

* 类的代码块，默认就是严格模式	
  * 类的代码块是用来设置对象的属性的，不是什么代码都能写
* **静态属性只能通过类去访问 ：类.属性**

```js
class Person{
   name = "孙悟空" // Person的实例属性name p1.name
   age = 18       // 实例属性只能通过实例访问 p1.age
   static test = "test静态属性" // 使用static声明的属性，是静态属性（类属性） Person.test
   static hh = "静态属性"   // 静态属性只能通过类去访问 Person.hh
}
const p1 = new Person()
console.log(p1)
```

#### 6.3 方法

**静态方法（类方法） 通过类来调用 静态方法中this指向的是当前类**

```js
class Person{
    name = "孙悟空"
    // sayHello = function(){
    // } // 添加方法的一种方式
    sayHello(){
        console.log('大家好，我是' + this.name)
    } // 添加方法（实例方法） 实例方法中this就是当前实例
    static test(){
        console.log("我是静态方法", this)
    } // 静态方法（类方法） 通过类来调用 静态方法中this指向的是当前类
}
const p1 = new Person()
// console.log(p1)
Person.test()
p1.sayHello()
```

![1662912061729](C:\Users\79426\AppData\Local\Temp\1662912061729.png)

#### 6.4 构造方法

* 在类中可以添加一个特殊的方法constructor
* 该方法我们称为构造函数（构造方法）
* 构造函数会在我们调用类创建对象时执行

```js
class Person{
    constructor(name, age, gender){
        // console.log("构造函数执行了~", name, age, gender)
        // 可以在构造函数中，为实例属性进行赋值
        // 在构造函数中，this表示当前所创建的对象
        this.name = name
        this.age = age
        this.gender = gender
    }
}
const p1 = new Person("孙悟空", 18, "男")
```

#### 6.5 封装

* 封装

  * 对象就是一个用来存储不同属性的容器

  * 对象不仅存储属性，还要负责数据的安全

  *  直接添加到对象中的属性，并不安全，因为它们可以被任意的修改

  * 如何确保数据的安全：

    1. 私有化数据

    		将需要保护的数据设置为私有，只能在类内部使用

    2. 提供setter和getter方法来开放对数据的操作

       ​	属性设置私有，通过getter setter方法操作属性带来的好处

       ​		-可以控制属性的读写权限

       ​		-可以在方法中对属性的值进行验证

  * 封装主要用来保证数据的安全

  * **实现封装的方式：**

    *  **1.属性私有化 加#**
    *  **2.通过getter和setter方法来操作属性**

    ​            get 属性名(){
                    return this.#属性
                }
                set 属性名(参数){
                    this.#属性 = 参数
                }

```js
class Person {
    // #address = "花果山" // 实例使用#开头就变成了私有属性，私有属性只能在类内
    #name
    #age
    #gender
    constructor(name, age, gender) {
        this.#name = name
        this.#age = age
        this.#gender = gender
    }
    sayHello() {
        console.log(this.#name)
    }
    // getter方法，用来读取属性
    getName(){
        return this.#name
    }
    // setter方法，用来设置属性
    setName(name){
        this.#name = name
    }
    getAge(){
        return this.#age
    }
    setAge(age){
        if(age >= 0){
            this.#age = age
        }
    }
    get gender(){
        return this.#gender
    }
    set gender(gender){
        this.#gender = gender
    }
}
const p1 = new Person("孙悟空", 18, "男")
// p1.age = "hello"
// p1.getName()
p1.setAge(-11) // p1.age = 11  p1.age
// p1.setName('猪八戒')
p1.gender = "女"
console.log(p1.gender)
```

#### 6.6 多态

* 多态
  * 在JS中不会检查参数的类型，所以这就意味着任何数据都可以作为参数传递
  *  要调用某个函数，无需指定的类型，只要对象满足某些条件即可
  * 如果一个东西走路像鸭子，叫起来像鸭子，那么它就是鸭子
  *  多态为我们提供了灵活性

```js
 class Person{
     constructor(name){
         this.name = name
     }
 }
 class Dog{
     constructor(name){
         this.name = name
     }
 }
 class Test{
 }
 const dog = new Dog('旺财')
 const person = new Person("孙悟空")
 const test = new Test()
 // console.log(dog)
 // console.log(person)
 /* 
     定义一个函数，这个函数将接收一个对象作为参数，他可以输出hello并打印对象的name属性

 */
function sayHello(obj){
     // if(obj instanceof Person){
         console.log("Hello,"+obj.name)
     // }
}
sayHello(dog)
```

#### 6.7 继承

* 继承

  * **可以通过extends关键来完成继承**

  * 当一个类继承另一个类时，就相当于将另一个类中的代码复制到了当前类中（简单理解）

  * 继承发生时，被继承的类称为 父类（超类），继承的类称为 子类

  * 通过继承可以减少重复的代码，并且可以在不修改一个类的前提对其进行扩展

  * **通过继承可以在不修改一个类的情况下对其进行扩展**

  * OCP 开闭原则：

    **程序应该对修改关闭，对扩展开放**

​    **封装 —— 安全性**
    **继承 —— 扩展性**
    **多态 —— 灵活性**

```js
class Animal{
    constructor(name){
        this.name = name
    }
    sayHello(){
        console.log("动物在叫~")
    }
}
class Dog extends Animal{
    
}
class Cat extends Animal{
    
}
const dog = new Dog("旺财")
const cat = new Cat("汤姆")
dog.sayHello()
cat.sayHello()
console.log(dog)
console.log(cat)
```

![1662912880363](C:\Users\79426\AppData\Local\Temp\1662912880363.png)

```js
class Animal{
    constructor(name){
        this.name = name
    }
    sayHello(){
        console.log("动物在叫~")
    }
}
class Dog extends Animal{
    // 在子类中，可以通过创建同名方法来重写父类的方法
    sayHello(){
        console.log("汪汪汪")
    }
    
}
class Cat extends Animal{
    // 重写构造函数
    constructor(name, age){
        // 重写构造函数时，构造函数的第一行代码必须为super()
        super(name) // 调用父类的构造函数
        this.age = age
    }
    
    sayHello(){
        // 调用一下父类的sayHello
        super.sayHello() // 在方法中可以使用super来引用父类的方法
        console.log("喵喵喵")
    }
}
        
const dog = new Dog("旺财")
const cat = new Cat("汤姆", 3)
dog.sayHello()
cat.sayHello()
console.log(dog)
console.log(cat)
```

![1662913033364](C:\Users\79426\AppData\Local\Temp\1662913033364.png)

#### 6.8 对象的结构

* 对象中存储属性的区域实际有两个：

  1. 对象自身

      直接通过对象所添加的属性，位于对象自身中

     在类中通过 x = y 的形式添加的属性，位于对象自身中

  2. **原型对象（prototype）**

      - 对象中还有一些内容，会存储到其他的对象里（原型对象）
      - 在对象中会有一个属性用来存储原型对象，这个属性叫做 _ **_proto_** _

```js
class Person {
    name = "孙悟空"
    age = 18
    // constructor(){
    //     this.gender = "男"
    // }
    sayHello() {
        console.log("Hello，我是", this.name)
    }
}
const p = new Person()
// p.address = "花果山"
// p.sayHello = "hello"
console.log(p.sayHello)
```

#### 6.9 原型对象

##### 6.9.1 访问原型对象

- 访问一个对象的原型对象
  - **对象** . _ **_proto_** _
  - **Object.getPrototypeOf(对象)**
- 原型对象中的数据：
  - 对象中的数据（属性、方法等）
  - constructor （对象的构造函数）
- 注意：
  - 原型对象也有原型，这样就构成了一条原型链，根据对象的复杂程度不同，原型链的长度也不同
    - p对象的原型链：p对象 --> 原型 --> 原型 --> null
    -  obj对象的原型链：obj对象 --> 原型 --> null
- 原型链：
  - 读取对象属性时，会优先对象自身属性
  - 如果对象中有，则使用，没有则去对象的原型中寻找
  - 直到找到Object对象的原型（Object的原型没有原型（为null））
    -  如果依然没有找到，则返回undefined
- **作用域链，是找变量的链，找不到会报错**
-  **原型链，是找属性的链，找不到会返回undefined**

```js
class Person {
    name = "孙悟空"
    age = 18
    sayHello() {
        console.log("Hello，我是", this.name)
    }
}
const p = new Person()
// console.log(p)
console.log(p.__proto__.__proto__.__proto__)
console.log(p.constructor)
console.log(Object.getPrototypeOf(p) === p.__proto__)
const obj = {} // obj.__proto__
```

![1662913888872](C:\Users\79426\AppData\Local\Temp\1662913888872.png)

* 所有的同类型对象它们的原型对象都是同一个，
  * 也就意味着，同类型对象的原型链是一样的
* 原型的作用：
  * 原型就相当于是一个公共的区域，可以被所有该类实例访问，
    * 可以将该类实例中，所有的公共属性（方法）统一存储到原型中
    *  这样我们只需要创建一个属性，即可被所有实例访问
  * JS中继承就是通过原型来实现的,
    * 当继承时，子类的原型就是一个父类的实例
  * 在对象中有些值是对象独有的，像属性（name，age，gender）每个对象都应该有自己值，
    *  但是有些值对于每个对象来说都是一样的，像各种方法，对于一样的值没必要重复的创建
  * 尝试：
        函数的原型链是什么样子的？
        Object的原型链是什么样子的？

    ```js
class Animal{
}
class Cat extends Animal{
}
class TomCat extends Cat{
}
// TomCat --> cat --> Animal实例 --> object --> Object原型 --> null
// cat --> Animal实例 --> object --> Object原型 --> null
// p对象 --> object --> Object原型 --> null
const cat = new Cat()
console.log(cat.__proto__.__proto__.__proto__.__proto__)//null
    ```

##### 6.9.2 修改原型对象

* 大部分情况下，我们是不需要修改原型对象

​    注意：
        千万不要通过类的实例去修改原型
            1. 通过一个对象影响所有同类对象，这么做不合适
            2. 修改原型先得创建实例，麻烦
            3. 危险

* 处理通过 _ **_proto_** _ 能访问对象的原型外，
  * 还可以通过类的prototype属性，来访问实例的原型
* 修改原型时，最好通过通过类去修改

​    好处
        1. 一修改就是修改所有实例的原型
        2. 无需创建实例即可完成对类的修改
    原则：
        **1. 原型尽量不要手动改**
        **2. 要改也不要通过实例对象去改**
        **3. 通过 类.prototype 属性去修改**
        **4. 最好不要直接给prototype去赋值**

```js
class Person {
    name = "孙悟空"
    age = 18
    sayHello() {
        console.log("Hello，我是", this.name)
    }
}
            
Person.prototype.fly = () => {
    console.log("我在飞！")
}
class Dog{
}
const p = new Person()
const p2 = new Person()
// 通过对象修改原型，向原型中添加方法，修改后所有同类实例都能访问该方法 不要这么做
// p.__proto__.run = () => {
//     console.log('我在跑~')
// }
// p.__proto__ = new Dog() // 直接为对象赋值了一个新的原型 不要这么做
// console.log(p)
// console.log(p2)
// p.run()
// p2.run()
// console.log(Person.prototype) // 访问Person实例的原型对象
p.fly()
p2.fly()
```

#### 6.10 instanceof和hasOwn

##### 6.10.1 instanceof

* instanceof 用来检查一个对象是否是一个类的实例

  * instanceof检查的是对象的原型链上是否有该类实例
  *  只要原型链上有该类实例，就会返回true

   dog -> Animal的实例 -> Object实例 -> Object原型

* **Object是所有对象的原型，所以任何和对象和Object进行instanceof运算都会返回true**

```js
class Animal {}
class Dog extends Animal {}
const dog = new Dog()
console.log(dog instanceof Dog) // true
console.log(dog instanceof Animal) // true
console.log(dog instanceof Object) // true
const obj = new Object()
// console.log(obj.__proto__)
// console.log(Object.prototype)
// dog.__proto__ / Dog.prototype
```

##### 6.10.2 Object.hasOwn

*  in
  * 使用in运算符检查属性时，**无论属性在对象自身还是在原型中，都会返回true**
*  对象.hasOwnProperty(属性名) **(不推荐使用)**
  -  用来检查一个对象的自身是否含有某个属性
* **Object.hasOwn(对象, 属性名)** 
  * 用来检查一个对象的自身是否含有某个属性

```js
class Person {
    name = "孙悟空"
    age = 18
    sayHello() {
        console.log("Hello，我是", this.name)
    }
}
const p = new Person()
console.log("sayHello" in p)
console.log(p.hasOwnProperty("sayHello"))
console.log(p.__proto__.__proto__.hasOwnProperty("hasOwnProperty"))
console.log(Object.hasOwn(p, "sayHello"))
```

![1662915138799](C:\Users\79426\AppData\Local\Temp\1662915138799.png)

#### 6.11 旧类（了解）

* 早期JS中，直接通过函数来定义类
  * 一个函数如果直接调用 xxx() 那么这个函数就是一个普通函数
  * 一个函数如果通过new调用 new xxx() 那么这个函数就是一个构造函数

```js
// 1.
function Person(){
    
}
const p = new Person()
console.log(p)
//等价于class Person{}
// 2.
class MyClass{}
new MyClass()
// 2.只有MyClass（）会报错，必须通过 new 创建 MyClass
// 方式 1 中 new 不是必须的，不加 new 则是普通函数，加 new 则是构造函数，可以用来创建对象 
// 缺点：容易给代码造成紊乱 ，难区分是函数还是构造函数
// 后来类必须通过 new 来创建对象
```

![1662964942731](C:\Users\79426\AppData\Local\Temp\1662964942731.png)

```js
var Person = (function () {
    function Person(name, age) {
        // 在构造函数中，this表示新建的对象
        this.name = name
        this.age = age
        // this.sayHello = function(){
        //     console.log(this.name)
        // }
        // 问题 ： 将方法创建在对象里会出现每次创建对象都会创建方法，造成冗余，所以应该将方法添加进原型
    }
    // 向原型中添加属性（方法）
    Person.prototype.sayHello = function () {
        console.log(this.name)
    }
    //new Person()//错误的，后面代码还没执行
    // 静态属性
    Person.staticProperty = "xxx"
    // 静态方法
    Person.staticMethod = function () {}
    return Person
})()

// 为了将代码段隔离起来，避免外部的修改（例如静态方法/属性还没添加就在中间创建对象了）将所有方法放进一个立即执行函数里，返回一个Person --->闭包
```

* 旧类中的继承

```js
var Animal = (function(){
    function Animal(){
    }
    return Animal
})()
var Cat = (function(){
    function Cat(){
    }
    // 继承Animal
    // 将Animal的实例赋值给Cat的原型，实现继承
    Cat.prototype = new Animal()
    return Cat
})()
var cat = new Cat()
console.log(cat)
function person(){
}
```

#### 6.12 new 运算符

* new运算符是创建对象时要使用的运算符

  *  使用new时，到底发生了哪些事情：
  *  https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new

* 当使用new去调用一个函数时，这个函数将会作为构造函数调用

* 使用new调用函数时，将会发生这些事

   1.  创建一个普通的JS对象（Object对象 {}）, 为了方便，称其为新对象

  2.  将构造函数的prototype属性设置为新对象的原型
  3.  使用实参来执行构造函数，并且将新对象设置为函数中的this
  4.  如果构造函数返回的是一个非原始值，则该值会作为new运算的返回值返回**（千万不要这么做）**
  5.  如果**构造函数的返回值是一个原始值或者没有指定返回值**，则**新的对象将会作为返回值返回**，**通常不会为构造函数指定返回值**

#### 6.13 总结

* 面向对象本质就是，编写代码时所有的操作都是通过对象来进行的。
* 面向对象的编程的步骤：

​        1. 找对象
        2. 搞对象

* 学习对象：

      1.  明确这个对象代表什么，有什么用    

  2. 如何获取到这个对象

          3. 如何使用这个对象（对象中的属性和方法）

* 对象的分类：

  * 内建对象
            - 由ES标准所定义的对象

    ​	- 比如 Object Function String Number ...

  * 宿主对象
            - 由浏览器提供的对象

    ​	- BOM、DOM

  * 自定义对象
            - 由开发人员自己创建的对象

  

### 7. 数组

#### 7.1 for-of

* **for-of 语句可以用来遍历可迭代对象**

* 语法：

  **for( 变量 of 可迭代的对象 ){**

  **​        语句...**
   **}**

* 执行流程：
      for-of 的循环体会执行多次，**数组中有几个元素就会执行几次**
          每次执行时都会将一个元素赋值给变量

* **可以遍历数组和字符串，但只能按顺序**

```js
const arr = ["孙悟空", "猪八戒", "沙和尚", "唐僧"]
for(let value of arr){
    console.log(value)
}
 for(let value of "hello"){
     console.log(value)
 }
```

#### 7.2 数组的方法

* ##### Array.isArray()

  ​    - 用来检查一个对象是否是数组   
* ##### at()

  * 可以根据索引获取数组中的指定元素
      * **at可以接收负索引作为参数**
* **concat()**
  *  **用来连接两个或多个数组**
  *  非破坏性方法，不会影响原数组，而是返回一个新的数组

```js
 const arr = ["孙悟空", "猪八戒", "沙和尚", "唐僧"]
 console.log(arr.at(-2))
 // console.log(arr[arr.length - 2])
 const arr2 = ["白骨精", "蜘蛛精", "玉兔精"]
 let result = arr.concat(arr2, ["牛魔王","铁扇公主"])
 console.log(result)
```

![1663061445355](C:\Users\79426\AppData\Local\Temp\1663061445355.png)



* **indexOf()**

  * 获取元素在数组中第一次出现的索引
  * 参数：
    1.  要查询的元素
    2.  查询的起始位置

* **lastIndexOf()**

  * 获取元素在数组中最后一次出现的位置
  * 返回值：
           1.  找到了则返回元素的索引
           2.  没有找到返回-1

* **join()**

  * 将一个数组中的元素连接为一个字符串
  * ["孙悟空", "猪八戒", "沙和尚", "唐僧", "沙和尚"] -> "孙悟空,猪八戒,沙和尚,唐僧,沙和尚"
  * 参数：
            指定一个字符串作为连接符

* **slice()**

  *  用来截取数组（非破坏性方法）  

  * 参数：

            1. 截取的起始位置（包括该位置）
      
            2.  截取的结束位置（不包括该位置）
      
                ​	- 第二个参数可以省略不写，如果省略则会一直截取到最后
      
                ​	- 索引可以是负值
      
                **如果将两个参数全都省略，则可以对数组进行浅拷贝（浅复制）**

```js
let arr = ["孙悟空", "猪八戒", "沙和尚", "唐僧", "沙和尚"]
let result = arr.indexOf("沙和尚")
result = arr.indexOf("沙和尚", 3)
result = arr.lastIndexOf("沙和尚", 3)
result = arr.indexOf("白骨精")
result = arr.join()
result = arr.join("@-@")
result = arr.join("")
arr = ["孙悟空", "猪八戒", "沙和尚", "唐僧"]
result = arr.slice(0, 2)
result = arr.slice(1, 3)
result = arr.slice(1, -1)
result = arr.slice()
```

![1663063083121](C:\Users\79426\AppData\Local\Temp\1663063083121.png)

* **push()**
  * 向数组的末尾添加一个或多个元素，并返回新的长度

* **pop()**
  * 删除并返回数组的最后一个元素

* **unshift()**

  * 向数组的**开头添加一个或多个元素，并返回新的长度**

* **shift()**

  *  **删除并返回数组的第一个元素**

* **reverse()**

  * **反转数组**

* **splice()**

  *  可以删除、插入、替换数组中的元素

  * 参数：

    1.  删除的起始位置
    2.  删除的数量
    3.  要插入的元素

  * 返回值：

    ​	**返回被删除的元素**

```js
let arr = ["孙悟空", "猪八戒", "沙和尚"]
let result = arr.push("唐僧", "白骨精")
console.log(arr)
result = arr.pop()
let length = arr.unshift("牛魔王")
arr.shift()
console.log(arr)
arr = ["孙悟空", "猪八戒", "沙和尚", "唐僧"]
console.log(arr);
result = arr.splice(1, 2)
console.log(result);
// result = arr.splice(1, 1, "牛魔王", "铁扇公主", "红孩儿")
result = arr.splice(1, 0, "牛魔王", "铁扇公主", "红孩儿")
console.log(result)
console.log(arr)
arr = ["a", "b", "c", "d"]
arr.reverse()
```

![1663074402157](C:\Users\79426\AppData\Local\Temp\1663074402157.png)

* **sort()**

  * sort用来对数组进行排序（会对改变原数组）

  * sort默认会将数组升序排列

    ​	**注意：sort默认会按照Unicode编码进行排序，所以如果直接通过sort对数字进行排序可能会得到一个不正确的结果**

  * 参数：

    * 可以传递一个回调函数作为参数，通过回调函数来指定排序规则

​           		**(a, b) => a - b 升序排列**
            		**(a, b) => b - a 降序排列**

* **forEach()**

  * **用来遍历数组**

  * **它需要一个回调函数作为参数，这个回调函数会被调用多次**

    ​        **数组中有几个元素，回调函数就会调用几次**
            **每次调用，都会将数组中的数据作为参数传递**

  * 回调函数中有三个参数：

    * element 当前的元素
    * index 当前元素的索引
    * array 被遍历的数组

* **filter()**

  *  **将数组中符合条件的元素保存到一个新数组中返回**
  *  **需要一个回调函数作为参数，会为每一个元素去调用回调函数，并根据返回值来决定是否将元素添加到新数组中**
  * 非破坏性方法，不会影响原数组

* **map()**
  * **根据当前数组生成一个新数组**
  * **需要一个回调函数作为参数，**
    * 回调函数的返回值会成为新数组中的元素
  * 非破坏性方法不会影响原数组

* **reduce()**

  * **可以用来将一个数组中的所有元素整合为一个值**
  * 参数：

  ​        1.  回调函数，通过回调函数来指定合并的规则
          2.  可选参数，初始值

```JS
arr.sort()
//(11) [0, 1, 10, 2, 3, 4, 5, 6, 7, 8, 9]
arr.sort((a, b) => a - b)
//(11) [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
arr.sort((a, b) => b - a)
//(11) [10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
arr = ["孙悟空", "猪八戒", "沙和尚", "唐僧"]
arr.forEach((element, index, array) => {
    // console.log(array)
    /*
        (4) ['孙悟空', '猪八戒', '沙和尚', '唐僧']
        (4) ['孙悟空', '猪八戒', '沙和尚', '唐僧']
        (4) ['孙悟空', '猪八戒', '沙和尚', '唐僧']
        (4) ['孙悟空', '猪八戒', '沙和尚', '唐僧']
    */
})
arr.forEach((element, index) => console.log(index, element))
/*
    0 '孙悟空'
    1 '猪八戒'
    2 '沙和尚'
    3 '唐僧'
*/
arr = [1, 2, 3, 4, 5, 6, 7, 8]
// 获取数组中的所有偶数
let result = arr.filter((ele) => ele > 5)
arr = ["孙悟空", "猪八戒", "沙和尚"]
// html多个数据添加标签
result = arr.map((ele) => "<li>" + ele + "</li>")
arr = [1, 2, 3, 4, 5, 6, 7, 8]
result = arr.reduce((a, b) => {
    /* 
        1, 2
        3, 3
        6, 4
        10, 5
    a : 1+1, b: 2
    */
    console.log(a, b)
    return a + b
}) 
result = arr.reduce((a, b) => a + b, 10)
/ 10 --->指定a的初始值
    /* 
        10, 1
        11, 2
        13, 3
        16, 4
        20, 5
        25, 6
        31, 7
        38, 8
        46
    */
console.log(result)
// 46
```



#### 7.3 对象的复制

* 如何去复制一个对象 复制必须要产生新的对象
* **当调用slice时，会产生一个新的数组对象，从而完成对数组的复制**

```js
const arr = ["孙悟空", "猪八戒", "沙和尚"]
const arr3 = arr.slice()
arr3[0] = "唐僧"
console.log(arr)
console.log(arr3)
```

![1663063617314](C:\Users\79426\AppData\Local\Temp\1663063617314.png)

* **... (展开运算符)**
  * 可以将一个数组中的元素展开到另一个数组中或者作为函数的参数传递
  * 通过它也可以对数组进行浅复制

```js
const arr = ["孙悟空", "猪八戒", "沙和尚"]
const arr2 = arr.slice()
const arr3 = [...arr]
function sum(a, b, c) {
    return a + b + c
}
const arr4 = [10, 20, 30]
let result = sum(arr4[0], arr4[1], arr4[2])
result = sum(...arr4)

const obj = { name: "孙悟空", age: 18 }
// const obj2 = Object.assign({}, obj)
const obj2 = { address: "花果山", age: 28 }
Object.assign(obj2, obj)
console.log(obj2)
const obj3 = { address: "高老庄", ...obj, age: 48 } // 将obj中的属性在新对象中展开
console.log(obj3);
```

![1663073282250](C:\Users\79426\AppData\Local\Temp\1663073282250.png)

* 对象的复制
  *  **Object.assign(目标对象, 被复制的对象)**
  *  将被复制对象中的属性复制到目标对象里，并将目标对象返回
* 也可以使用展开运算符对对象进行复制

#### 7.4 浅拷贝和深拷贝

* 浅拷贝（shallow copy）
  * **通常对对象的拷贝都是浅拷贝**
  * 浅拷贝顾名思义，只对对象的浅层进行复制（只复制一层）
  * **如果对象中存储的数据是原始值，那么拷贝的深浅是不重要**
  * **浅拷贝只会对对象本身进行复制，不会复制对象中的属性（或元素）**
* 深拷贝（deep copy）
  * **深拷贝指不仅复制对象本身，还复制对象中的属性和元素**
  * 因为性能问题，通常情况不太使用深拷贝

```js
// 创建一个数组
const arr = [{name:"孙悟空"}, {name:"猪八戒"}]
const arr2 = arr.slice() // 浅拷贝
const arr3 = structuredClone(arr) // 专门用来深拷贝的方法
console.log(arr)
console.log(arr3)
```

浅拷贝：

![1663063843596](C:\Users\79426\AppData\Local\Temp\1663063843596.png)

深拷贝：

![1663064047541](C:\Users\79426\AppData\Local\Temp\1663064047541.png)

#### 7.5 数组去重

##### 7.5.1 方法一 ： splice 的运用

```js
const arr = [1, 2, 1, 3, 2, 2, 4, 5, 5, 6, 7]
// 编写代码去除数组中重复的元素
// 分别获取数组中的元素
for (let i = 0; i < arr.length; i++) {
    // 获取当前值后边的所有值
    for (let j = i + 1; j < arr.length; j++) {
        // 判断两个数是否相等
        if (arr[i] === arr[j]) {
            // 出现了重复元素，删除后边的元素
            arr.splice(j, 1)
            /* 
                当arr[i] 和 arr[j]相同时，它会自动的删除j位置的元素，然后j+1位置的元素，会变成j位置的元素
                而j位置已经比较过了，不会重复比较，所以会出现漏比较的情况
                解决办法，当删除一个元素后，需要将该位置的元素在比较一遍
            */
            j--
        }
    }
}
console.log(arr)
```

##### 7.5.2 方法二 ： push 的运用

```js
const arr = [1, 2, 1, 3, 2, 2, 4, 5, 5, 6, 7]
const newArr = []
for(let ele of arr){
    if(newArr.indexOf(ele) === -1){
        newArr.push(ele)
    }
}
console.log(newArr)
```

#### 7.6 回调函数

##### 7.6.1 filter()函数用来对数组进行过滤

```js
class Person {
    constructor(name, age) {
        this.name = name
        this.age = age
    }
}
const personArr = [
    new Person("孙悟空", 18),
    new Person("沙和尚", 38),
    new Person("红孩儿", 8),
    new Person("白骨精", 16),
]
// filter()函数用来对数组进行过滤
function filter(arr) {
    const newArr = []
    for (let i = 0; i < arr.length; i++) {
        if (arr[i].age < 18) {
            newArr.push(arr[i])
        }
    }
    return newArr
}
result = filter(personArr)
console.log(result)
```

##### 7.6.2 问题

* 目前我们的函数只能过滤出数组中age属性小于18的对象
  * 我们希望过滤更加灵活：
    * 比如：过滤数组中age大于18的对象
      * age大于60的对象
      * age大于n的对象
      * 过滤数组中name为xxx的对象
      * 过滤数组中的偶数
                     ...
* **一个函数的参数也可以是函数**
  * **如果将函数作为参数传递，那么我们就称这个函数为回调函数（callback）**

```js
class Person {
    constructor(name, age) {
        this.name = name
        this.age = age
    }
}
const personArr = [
    new Person("孙悟空", 18),
    new Person("沙和尚", 38),
    new Person("红孩儿", 8),
    new Person("白骨精", 16),
]
function filter(arr, cb) {
    const newArr = []
    // console.log("-->", cb)
    // cb()
    for (let i = 0; i < arr.length; i++) {
        // arr[i].age >= 18
        // arr[i].age > 60
        // arr[i].age > n
        // arr[i].name === "xxx"
        // arr[i] % 2 === 0
        if (cb(arr[i])) {
            newArr.push(arr[i])
        }
    }
    return newArr
}
function fn(a){
    return a.name === "孙悟空"
}
result = filter(personArr, fn)
console.log(result)
```

![1663075228781](C:\Users\79426\AppData\Local\Temp\1663075228781.png)

#### 7.7 高阶函数

##### 7.7.1 高阶函数引例

* **如果一个函数的参数或返回值是函数，则这个函数就称为高阶函数**
* 为什么要将函数作为参数传递？（回调函数有什么作用？）
  * **将函数作为参数，意味着可以对另一个函数动态的传递代码**

```js
class Person {
    constructor(name, age) {
        this.name = name
        this.age = age
    }
}
const personArr = [
    new Person("孙悟空", 18),
    new Person("沙和尚", 38),
    new Person("红孩儿", 8),
    new Person("白骨精", 16),
]
function filter(arr, cb) {
    const newArr = []
    for (let i = 0; i < arr.length; i++) {
        if (cb(arr[i])) {
            newArr.push(arr[i])
        }
    }
    return newArr
}
// 我们这种定义回调函数的形式比较少见，通常回调函数都是匿名函数
// function fn(a) {
//     return a.name === "孙悟空"
// }
result = filter(personArr, a => a.name === "孙悟空")
console.log(result);
result = filter(personArr, a => a.age >= 18)
console.log(result);
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
result = filter(arr, a => a % 2 === 0)
console.log(result)
```

![1663075462058](C:\Users\79426\AppData\Local\Temp\1663075462058.png)

##### 7.7.2 高阶函数

* 希望在someFn()函数执行时，可以记录一条日志
* 在不修改原函数的基础上，为其增加记录日志的功能
* 可以通过高阶函数，来动态的生成一个新函数

```js
function someFn() {
    console.log(2);
    return "hello"
}
function outer(cb){
    return () => {
        console.log(1);
        console.log("记录日志~~~~~")
        const result = cb()
        // result = hello
        return result
    }
}
let result = outer(someFn)
console.log("result = " + result)
//result 只返回了第一个return
console.log("result() = " +result());
//result() 变成了立即执行函数，继续执行后续代码

function test(){
    console.log("test~~~~")
    return "test"
}
let newTest = outer(test)
// 既有test的全部功能又能记录日记
newTest()
```

![1663077828371](C:\Users\79426\AppData\Local\Temp\1663077828371.png)

#### 7.8 闭包

* 创建一个函数，第一次调用时打印1，第二次调用打印2，以此类推
* 可以利用函数，来隐藏不希望被外部访问到的变量
* 闭包：
  *  闭包就是能访问到外部函数作用域中变量的函数
* 什么时候使用：
  *  **当我们需要隐藏一些不希望被别人访问的内容时就可以使用闭包**
* 构成闭包的要件：
      1.  函数的嵌套
      2.  内部函数要引用外部函数中的变量
      3.  内部函数要作为返回值返回
* **函数在作用域，在函数创建时就已经确定的（词法作用域）**
  * **和调用的位置无关**
  * **闭包利用的就是词法作用域**

```js
function outer(){
    let num = 0 // 位于函数作用域中
    return () => {
        num++
        console.log(num)
    }
}
const newFn = outer()
// console.log(newFn)
newFn()
newFn()
newFn()
// 每次的num都是独立的
```

```js
function fn(){
    console.log(a)
}
function fn2(){
    let a = "fn2中的a"
    fn()
}
// fn2()
function fn3(){
    let a = "fn3中的a"
    function fn4(){
        console.log(a)
    }
    return fn4
}
let fn4 = fn3()
fn4()//输出 "fn3中的a"
```

#### 7.9 闭包的注意事项

* 闭包的生命周期：

  1. **闭包在外部函数调用时产生，外部函数每次调用都会产生一个全新的闭包**

          2. **在内部函数丢失时销毁（内部函数被垃圾回收了，闭包才会消失）**

* 注意事项：

  * 闭包主要用来隐藏一些不希望被外部访问的内容，

    ​	这就意味着闭包需要占用一定的内存空间

  * 相较于类来说，**闭包比较浪费内存空间（类可以使用原型而闭包不能）**，
            需要**执行次数较少时，使用闭包**
            需要大量创建实例时，使用类

```js
function outer(){
    let someVariable = "someValue"
    return function(){
        console.log(someVariable)
    }
}
function outer2(){
    let num = 0
    return () => {
        num++
        console.log(num)
    }
}
let fn1 = outer2() // 独立闭包
let fn2 = outer2() // 独立闭包
fn1()
fn2()
// fn1 = null
// fn2 = null
// 销毁
```

#### 7.10 可变参数

* arguments

  * arguments是函数中又一个隐含参数
  * arguments是一个类数组对象（伪数组）
    * 和数组相似，可以通过索引来读取元素，也可以通过for循环变量，但是它不是一个数组对象，不能调用数组的方法
  * arguments用来存储函数的实参，
    * 无论用户是否定义形参，实参都会存储到arguments对象中
    *  可以通过该对象直接访问实参

* 可变参数，在定义函数时可以将参数指定为可变参数

  * 可变参数可以接收任意数量实参，并将他们统一存储到一个数组中返回
  * 可变参数的作用和arguments基本是一致，但是也具有一些不同点：

  ​        1. 可变参数的名字可以自己指定
          2. 可变参数就是一个数组，可以直接使用数组的方法
          3. 可变参数可以配合其他参数一起使用

```js
function fn() {
    arguments.forEach((ele) => console.log(ele))
}
// fn(1, 10, 33)
// 定义一个函数，可以求任意个数值的和
function sum() {
    // 通过arguments，可以不受参数数量的限制更加灵活的创建函数
    let result = 0
    for (let num of arguments) {
        result += num
    }
    return result
}
function fn2(...abc) {
    console.log(abc)
}
function sum2(...num) {
    return num.reduce((a, b) => a + b, 0)
}
// 当可变参数和普通参数一起使用时，需要将可变参数写到最后
function fn3(a, b, ...args) {
    // for (let v of arguments) {
    //     console.log(v)
    // }
    console.log(args)
}
fn3(123, 456, "hello", true, "1111")
```

#### 7.11 函数

* 根据函数调用方式的不同，this的值也不同：

  ​    1.  以函数形式调用，this是window
      2.  以方法形式调用，this是调用方法的对象
      3.  构造函数中，this是新建的对象
      **4.  箭头函数没有自己的this，由外层作用域决定**
      **5.  通过call和apply调用的函数，它们的第一个参数就是函数的this**

  ​    **6.  通过bind返回的函数，this由bind第一个参数决定（无法修改） **

* 调用函数除了通过 函数() 这种形式外，还可以通过其他的方式来调用函数

  * 比如，我们可以通过调用函数的call()和apply()来个方法来调用函数

  ​        **函数.call()**
          **函数.apply()**
          - call 和 apply除了可以调用函数，还可以用来指定函数中的this
          - call和apply的第一个参数，将会成为函数的this
          **- 通过call方法调用函数，函数的实参直接在第一个参数后一个一个的列出来**
          **- 通过apply方法调用函数，函数的实参需要通过一个数组传递**

* **bind()** 是函数的方法，可以**用来创建一个新的函数**

```js
function fn() {
    console.log("函数执行了~", this)
}
const obj = { name: "孙悟空", fn }
// fn.call(obj)
// fn.apply(console)
function fn2(a, b) {
    console.log("a =", a, "b =", b, this)
}
// fn2.call(obj, "hello", true)
fn2.apply(obj, ["hello", true])
```

```js
function fn(a, b, c) {
    console.log("fn执行了~~~~", this)
    console.log(a, b, c)
}
const obj = {name:"孙悟空"}
const newFn = fn.bind(obj, 10, 20, 30)
newFn()
const arrowFn = () => {
    console.log(this)
}
// arrowFn.call(obj)
const newArrowFn = arrowFn.bind(obj)
// newArrowFn()
class MyClass{
    fn = () => {
        console.log(this)
        //外层是MyClass
    }
}
const mc = new MyClass()
// mc.fn.call(window)
```

#### 8. 内建对象

#### 8.1 解构赋值

```js
const arr = ["孙悟空", "猪八戒", "沙和尚"]
let a,b,c
    // a = arr[0]
    // b = arr[1]
    // c = arr[2]
;[a, b, c] = arr // 解构赋值
let [d, e, f, g] = ["唐僧", "白骨精", "蜘蛛精", "玉兔精"] // 声明同时解构
console.log(d, e, f, g)
;[d, e, f, g] = [1, 2, 3] //1 2 3 undefined
;[d, e, f = 77, g = 10] = [1, 2, 3]// 1 2 3 10
[d, e, f, g] = ["唐僧", "白骨精", "蜘蛛精", "玉兔精"]
;[d, e, f = 77, g = g] = [1, 2, 3]// 1 2 3 '玉兔精'
let [n1, n2, ...n3] = [4, 5, 6, 7] 
// 解构数组时，可以使用...来设置获取多余的元素
// 4 5 (2) [6, 7]
function fn(){
    return ["二郎神", "猪八戒"]
}
let [name1, name2] = fn()
// 可以通过解构赋值来快速交换两个变量的值
let a1 = 10
let a2 = 20
;[a1, a2] = [a2, a1] // [20, 10]
const arr2 = ["孙悟空", "猪八戒"]
// console.log(arr2)
;[arr2[0], arr2[1]] = [arr2[1], arr2[0]]
// console.log(arr2)
/* 
    数组中可以存储任意类型的数据，也可以存数组,
        如果一个数组中的元素还是数组，则这个数组我们就称为是二维数组
*/
const arr3 = [["孙悟空", 18, "男"], ["猪八戒" ,28, "男"]]
let [[name, age, gender], obj] = arr3
console.log(name, age, gender)// 孙悟空 18 男
console.log(obj)// (3) ['猪八戒', 28, '男']
```

#### 8.2 对象的解构

```js
const obj = { name: "孙悟空", age: 18, gender: "男" }
// let { name, age, gender } = obj // 声明变量同时解构对象
let name, age, gender
;({ name, age, gender } = obj)
//js解析时，以大括号开头的解析成代码块，对象给代码块赋值会很奇怪，所以小括号开头消除误会
let { address } = obj // 没有的属性返回undefined
// console.log(name, age, gender)
let {name:a, age:b, gender:c, address:d="花果山"} = obj
// 起别名abcd，将name赋给a....
console.log(a, b, c, d) // 孙悟空 18 男 花果山
```

