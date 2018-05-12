# js_get----set
关于JavaScript中Get/Set访问器

  
有时候大家可能会纳闷，在使用JavaScript的时候，只需要给一个系统变量赋值就可以触发一系列操作去相应。

但是我们在写Js的时候，修改了一个自定义变量，却连个P都没有。是不是很郁闷呢？

其实，我们现在就可以做类似系统变量那样的功能了！

  
 做个假设，我们有一个变量，要求可以输入出生年份并自动计算当前年龄。

  如：
   
           // 定义一个年龄变量并赋予初始值
            var age = 18;
            // 我们手动输入的出生年份
            age = 1994;
            // 此时age=?
            
      
按需求来说，age这个时候应该是等于23。

很明显要做这个操作我们要调用一个函数来进行处理，但是能不能不手动调用函数来完成这个功能呢？   

下面我们来介绍一下此章主角 Get/Set访问器！


    说明了，就是我们可以限制一个变量是否可以被访问或是否可以被重写。

    另外还有一个功能是，我们在访问或重写时可以执行其他语句进行处理


 使用方法一：
 
               var age = 18;
                var test = {
                    get age (){
                        return age;
                    },
                    set age (value){
                        if(value > 100) {
                            age= new Date().getFullYear() - value
                        }
                        else age = value;
                    }
                };
                 test.age=2005
                console.log(test.age)   //2108-2005=13   输出 13


  可是以上方法比较麻烦也不好理解。
  我们来看看第二种方法是否更有实用性：


              function Person() {
                  var age = new Date().getFullYear() - 18;
                  Object.defineProperty(this, "age", {
                      get: function () { alert("内部存储数据为:" + age);
                          return new Date().getFullYear() - age;
                      },
                      set: function (value) {
                          age = value;
                      }
                  });
              }
           var obj=new Person()
              obj.age=2005;
             console.log(obj.age)   //13



 继续看下面  例子
 
 
                var obj={
                   _age:103,
                   get value_age(){
                     return this._age;
                  },
                 set value_age(value){
                   if(value>0&&value<200){
                     this._age=value+5
                   }else{
                       throw  new Error("失败")
                   }
                 }
              }
                    obj.value_age=122
                   console.log(obj.value_age)  //127
  
  
  
 例子     这个例子来自 js高级编程 第六章的讲解
 
               var book = {
                    _year: 2004,
                    edition: 1
                };
                Object.defineProperty(book, "year", {
                    get: function() {
                        return this._year;
                    },
                    set: function(newValue) {
                        if (newValue > 2004) {
                            this._year = newValue;
                            this.edition += newValue - 2004;
                        }
                    }
                });
                book.year = 2005;
                alert(book.edition); //2
 
 
  


















