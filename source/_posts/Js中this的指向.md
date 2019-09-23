---
title: Js中this的指向
date: 2019-07-19 17:09:30
tags: [js]
categories: JavaScript
---

#### this的指向理解

归根结底，this指向就一句话：谁最终调用函数，this指向谁！！！

    ① this指向的，永远只可能是对象！
    ② this指向谁，永远不取决于this写在哪！而是取决于函数在哪调用。
    ③ this指向的对象，我们称之为函数的上下文context，也叫函数的调用者。

　下面，请看具体情况。

1. 通过函数名()直接调用：this指向window
```
    function func(){
            console.log(this);
        }
        //① 通过函数名()直接调用：this指向window
        func(); // this--->window
```
2. 通过对象.函数名()调用的：this指向这个对象
```
    function func(){
            console.log(this);
        }
            //② 通过对象.函数名()调用的：this指向这个对象
            // 狭义对象
            var obj = {
                name:"obj",
                func1 :func
            };
            obj.func1(); // this--->obj
            // 广义对象
            document.getElementById("div").onclick = function(){
                this.style.backgroundColor = "red";
            }; // this--->div
```
3. 函数作为数组的一个元素，通过数组下标调用的：this指向这个数组
```
    function func(){
            console.log(this);
        }
        //③ 函数作为数组的一个元素，通过数组下标调用的：this指向这个数组
        var arr = [func,1,2,3];
        arr[0]();  // this--->arr
```

4. 函数作为window内置函数的回调函数调用：this指向window（ setInterval setTimeout 等）
```
    function func(){
            console.log(this);
        }
        //④ 函数作为window内置函数的回调函数调用：this指向window
        setTimeout(func,1000);// this--->window
        //setInterval(func,1000);
```

5. 函数作为构造函数，用new关键字调用时：this指向新new出的对象
```
    function func(){
            console.log(this);
        }
        //⑤ 函数作为构造函数，用new关键字调用时：this指向新new出的对象
        var obj = new func(); //this--->new出的新obj
```

#### 构造函数中的this理解

构造函数通过new生成实例，this的指向定位到这些实例对象上。

```
    function Person(name, age, job) {
        this.name = name; // this就是用来绑定到实例对象上
        this.age = age;
        this.job = job;
        this.sayName = function() { alert(this.name) } 
    }
    var person1 = new Person('Zaxlct', 28, 'Software Engineer');
    var person2 = new Person('Mick', 23, 'Doctor');

    console.log(person1.sayName()) //其中的this指向实例化对象person1
    console.log(person2.sayName()) //其中的this指向实例化对象person2
```

#### 关于this的一些误区 demo

```
　　var a =0;
    demo.a=2;
    function demo(){
        console.log('ok');
        this.a++
    }
    demo();//ok
    console.log(demo.a);//2
    console.log(a); //1
```

上面的demo已经得知，如果this是指向函数本身，那么demo.a的值应该为3，但还是2说明调用的不是demo函数。

 window对象的a却增加了，说明demo函数中的this是指向window。

 因为直接调用了demo(); Function demo 定义在window对象下，是全局函数，所以直接调用demo()等于是调用window对象下的demo方法，this自然指向window。

 `this.a++` 就会选中了同样在window下的 `var a = 0` ;

