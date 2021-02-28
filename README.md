# 概要
## 编程方式
1. 面向过程编程：一组函数的顺序执行
1. 面向对象编程： OOP把对象作为程序的基本单元,一个对象包含了数据和操作数据的函数。
1. 泛型编程：让类型参数化,方便程序员编码。类型参数化: 使的程序(算法)可以从逻辑功能上抽象,把被处理对象(数据)的类型作为参数传递。

## 类与对象
类是对一类事物的统称，是抽象的，不能直接使用。对象是一个具体存在的，看得见摸得着，可以直接拿来使用。类通过实例化获得对象。

# 第一原则：针对接口而非实现编程
## 接口interface
接口说明一个对象应该具有哪些方法，但并不规定这些方法应该如何实现。


接口提供了一份记载着可供公众访问的方法的契约。也就是定义了对象间具有的关系。只要接口不变，这个关系的双方都是可替换的。


一个理想的软件系统应该为所有类定义接口，这些类只向外提供它们实现的接口中规定的方法。其他方法都是私有的，外界只能通过接口中定义的存取操作与之打交道。但实际的系统很少能真正达到这样的境界。优质的代码应尽量向这个目标靠拢，但又不能过于刻板，把那些本不需要这些特性的简单项目复杂化。
所以实际使用中：
1.	避免定义接口外的公共方法，因为其他对象可能会对那些本不属于接口的方法产生依赖，而这是不安全的。因为这些方法随时都可能发生改变或删除，从而导致整个系统失灵。
1.	把原本要求以一个特定的类为参数的函数改为要求以一个特定的接口为参数的函数，那么如何实现了该接口的对象都可以作为参数传递它。这样一来，彼此不相关的对象也可以被同等对待。
1.	一批对象彼此存在着极大的差异，只要它们都实现了Comparable接口，那么高层模块就可以互相换用实现接口的对象。
## 优点
1. 既定的一批接口具有自我描述性，能促进代码的重用。接口可以告诉程序员一个类实现了哪些方法，从而帮助其使用这个类。
1. 有助于稳定不同类之间的通信方式。如果事先知道了接口，就能减少在集成两个对象过程中出现的问题。借助于它，你可以实现就说明你希望的一个类具有哪些特性和操作。一个程序员可以针对所需要的类定义一个接口，并把它转交给另一个程序员，第二个程序员可以随心所欲地编写自己的代码，只要他定义的类实现了那个接口就行。
1. 测试和调试因此也能变得更轻松。如果一个对象不像所要求的类型，或者没有实现必要的方法，那么就会得到包含有用信息的明确的错误提示。这样一来，逻辑错误可以被限制在方法自身，而不是在对象的构成之中
1. 让代码变得更稳固：因为对接口的如何改变在所有实现它的类中都必须体现出来。如果接口添加了一个操作，而某个实现它的类并没有相应的添加这个操作，那么你肯定会立即见到一个错误。
## 信息隐藏原则与接口扮演的角色
假设每天晚上同事会向你提交一份关于当天收益的报告单。接口定义非常清楚：你要求对方提供信息，同时收集原始数据计算收益，然后像你汇报。就算你跳槽去了别的公司，由于这个接口存在，所以你的接替者很容易用同样的方式得到信息汇报。
有一天你希望能听取同事的汇报更频繁地得到这种信息，找到了原始数据的存放地点，并且自己收集和计算相关数据。后来原始数据发生了变化，原本用json，改为xml，而且计算方法也会根据会计和税收法规进行调整，而你不精通这些法规。如果你要辞职，那么首先必须教会接替者这些工作，这比从同事那里请求最终计算结果要麻烦。
上述场景中，你对收益信息的内部细节形成了依赖。如果这种内部实现发生变化，你必须重新学习整个系统并从头开始。用面向对象设计的术语来说，你与原始数据之间形成了强耦合。信息隐藏原则有助于减轻系统中两个参与者之间的依赖性。它指出，两个参与者必须通过明确的通道传送消息。在本例中，这些通道就是对象间的接口。

## 接口和抽象类
* 接口的设计目的，是对类的行为进行约束
* 而抽象类的设计目的，是代码复用


Python没有接口的概念，只有抽象类。


接口和抽象类都是继承树的上层，他们的共同点如下：
1. 都是上层的抽象层。
1. 都不能被实例化
1. 都能包含抽象的方法，这些抽象的方法用于描述类具备的功能，但是不比提供具体的实现。


他们的区别如下：在抽象类中可以写非抽象的方法，从而避免在子类中重复书写他们，这样可以提高代码的复用性，这是抽象类的优势。

# 三大特性：封装、继承、多态
封装、继承、多态，整个顺序不能改，这是一个递进的过程
1.	封装：类内和类外，私有和共有。隐藏了类内部实现机制，保护数据，暴露给外面的只是一些访问方法，有私有属性和私有方法无法在外部被访问
2.	继承：在封装的基础上，想要有代码的复用才会有继承
3.	多态：C++有虚函数和非虚函数，python本身就是多态语言，相同的消息对不同的类做出不同的反应

## 封装（encapsulation）
### 封装与信息隐藏原则
封装：对对象的内部数据表现形式和实现细节进行隐藏，通过封装可以强制实施信息隐藏。


封装与信息隐藏之间是什么关系？你可以把它们视为同一概念的两种表述。信息隐藏是目的，而封装是藉以达到这个目的的技术。
### 优缺点
封装提高类类的独立性，总的来说，使代码更可靠，便于开发和维护
1. 私用变量有利于避免命名空间冲突。
1. 保护内部数据的完整性。减少其他函数所需的检查错误代码的数量，并确保数据不会处于无效状态。
1. 降低类与类之间的耦合：通过将一个方法或属性声明为私用的，可以让对象的实现细节对其他对象保密以降低对象之间的耦合。
1. 易于重构：对象重构因此可以变得更轻松。因为用户不知道对象的内部细节，所以你可以随心所欲地修改对象内部的数据结构和算法，对此外人不会知道，也不必知道。


缺点：


1. 私用方法很难进行单元测试。因为其内部变量都是私用的，所以在对象外部无法访问到它们，只对公用方法进行单元测试是一种广为接受的处理方式。
1. 使用封装意味着不得不与复杂的作用域链打交道，而这会使错误调试更加困难。一般来说这不算大问题，但有时候你会很难区分来自不同作用域的大批同名变量。
1. 过度封装也是一个潜在问题。封装可能会损害类的灵活性，致使无法被用于某些你未曾想到过的目的。
### Javascript封装
封装主要有两点:
1. 也就是把客观事物封装成抽象的类
1. 可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏：控制访问权限：private、public、protected


Js中可以模拟第一点，但是无法做到第二点，哪怕时ES6出了class，仍然无法有效进行封装数据。
#### 约定_开头private
约定下划线开头的属性或方法是私有的（实际和其他变量没有任何区别），下面结合get、set方法做数据劫持。
```javascript
let name = {
  _weight: 200, // 约定俗成的假定这个是私有的，程序员看见后不会访问这个属性
  get weight () {
    return this._weight/2
  },
  set weight (value) {
    this._weight = value * 2
  }
}
console.log(name.weight)
for(let i in name) {console.log(i)} // _weight weight
```
缺点，实际这只是一种约定，这个属性仍然能够访问到并修改
#### Symbol
实际上不论基于什么特性，都不能替代可读性，后续你需要通过上下文来判断这是一个唯一值还是一个私有变量。不建议使用Symbol


#### 立即执行函数
(function(){})()
立即执行函数原理是闭包
```javascript
let fun = (function() {
  let name = 'ccc'
  return function (param) {
    console.log(name+param)
  }
})()
fun('dddd') // cccdddd
```
立即执行函数有闭包拥有的所有缺点，且不具有可读性。
###	继承与掺元类
一般来说，在设计类的时候，我们希望：
1. 减少重复性代码
3. 尽量弱化对象间的耦合
继承符合第一个原则，不过让一个类继承另一个类可能会导致两者产生强耦合，即一个类依赖于另一个类的内部实现。需要考虑一些有助于避免这种问题的技术，其中包括掺元类为其他类提供方法这种技术。
有一种重用代码的方法不需要用到严格的继承。如果想把一个函数用到多个类中，可以通过扩充（augmentation）的方法让这些类共享该函数。其实际做法大体为：先创建一个包含各种通用方法的类，然后用它扩充其他类。这种包含通用方法的类称为掺元类（mixin class）。它们通常不会被实例化或直接调用，其存在的目的只是向其他类提供自己的方法。
```javascript
var Mixin = function(){};
Mixin.prototype = {
  // serialize方法将便利this的所有成员，将它们的值作为字符串输出
  // 这是一个简化的例子，更健壮的版本可以参考http://json.org/json.js中的toJSONString方法。
  // 这个方法可能在很多类中都会用到，但没必要让那些类都继承Mixin，把这个方法复制到这些类中也不明智
  serialize: function(){
    var output = [];
    for(key in this){
      output.push(key+":"+this[key]);
    }
    return output.join(',')
  }
}
// 这里为了方便只写了这样一个Author，实际这个可以已经添加了其他Mixin等的类
function Author(name){
  this.name = name;
}
// argument扩充了Author类，添加了Mixin中的方法
argument(Author, Mixin);
var author = new Author('Ross');
console.log(author.serialize())

// 这是一个简化版的argument，用一个for in循环遍历givingClass.prototype中的每一个成员，并将其添加到receivingClass.prototype中。如果有同名成员，不覆盖，转而处理下一个。
function argument(receivingClass, givingClass) {
  for(methodName in givingClass.prototype) {
    if (!receivingClass.prototype[methodName]){
      receivingClass.prototype[methodName] = givingClass.prototype[methodName];
    }
  }
}
```
上面的arugment是一个简化版本：如果掺元类中包含许多方法，但你只想复制其中的一两个，那么上面这个版本的augument是无法满足的，可以： 
 
 
####	达到多继承效果
前面使用Mixin类扩充了Author类，这达到了多继承效果，C++、python等允许子类继承多个超类，JS不能多继承。因为一个对象只能拥有一个原型对象，不过一个类用多个惨元类扩充。
不过适合这种方案的场合并不是很多，只有那些通用到足以使其在彼此大不相同的各种类中都能派上用场的方法才适合于共享（要是那些类彼此差异不是那么大，那么普通的继承往往更适合）


# 基于原型的Javascript
Javascript基于原型设计，这是一门很“奇怪”的语言，为了模仿其他语言的特性付出了巨大的代价：

* 为了模块化有了commonJS、AMD、CMD、seaJS，千呼万唤终于有了ES Module，然而node天然不支持，后续版本虽然支持，但存在很多问题，node与第三方插件在ES Module使用不同。
* 为了模仿强类型语言的部分功能，有了各种类型工具，再到Typescript。
* 在面向对象上又为实现“类”付出了巨大“代价”，前端开发人员应该都见识过创建和继承对象的各种方法，看见过prototype和constructor的区别，然而这一切都只是为了“模仿”面向对象程序，创建与继承的各种优缺点差异，都比不过一个class。


class是否本质是个function，是否将方法挂在prototype，其实没有太大的意义。有了明确的类，我们就可以毫无历史包袱的思考封装、继承、多态。当然也不是，JS仍然不能有效的封装，但至少我们可以考虑反射和自省，可以专注于类与类之间的相互关系。


## 类方法与静态方法
```javascript
class Test{
  static s(){}
};
Test.c= function () {};
Test.prototype

```

```javascript
constructor: class Test
  c: ƒ ()
    arguments: null
    caller: null
    length: 0
    name: ""
    prototype: {constructor: ƒ}
    __proto__: ƒ ()
    [[FunctionLocation]]: VM856:1
    [[Scopes]]: Scopes[2]
  arguments: (...)
  caller: (...)
  length: 0
  name: "Test"
  prototype: {constructor: ƒ}
  s: ƒ s()
    arguments: (...)
    caller: (...)
    length: 0
    name: "s"
    __proto__: ƒ ()
    [[FunctionLocation]]: VM856:1
    [[Scopes]]: Scopes[2]
    __proto__: ƒ ()
    [[FunctionLocation]]: VM856:1
    [[Scopes]]: Scopes[2]
  __proto__: Object
```

### 鸭子类型（duck typing）
“当看到一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子。” 我们并不关心对象是什么类型，到底是不是鸭子，只关心行为。
#### python
```python
class Cat:
    def say(self):
        print('miaomiao')

class Dog:
    def say(self):
        print('wangwang')

class Duck:
    def say(self):
        print('gaga')

def say(obj):
    obj.say()

cat = Cat()
dog = Dog()
duck = Duck()

say(cat) # miaomiao
say(dog) # wangwang
say(duck) # gaga
```
上面只关心行为，不过另一方面来说，类型会决定行为模式，同样的方法使用不同类型的参数会产生多种形态，也就是多态。
理解多态的方式很多，鸭子类型只是其中一种，我们也可以通过继承来理解，上面class可以多个父类，也有say方法，根据各自特性不同，重写say方法不同，所以同样的调用say方法，实现方式不同
#### JS
不使用ducktype
```javascript
function bird(){
    this.name="bird";
}
function duck(){
    this.name="duck";
}
const type=(animal)=>{
    if(animal instanceof bird){
        console.log("I am a bird");
    }else if(animal instanceof duck){
        console.log("I am a duck");
    }
}
var b=new bird();
var d=new duck();
type(b);
type(d);
使用Duck Typing：
var bird={
    name:'bird',
    speak:function(){
        console.log("I am a "+this.name);
    }
}
var duck={
    name:"duck",
    speak:function(){
        console.log("I am a "+this.name);
    }
}
const type=(animal)=>{
    if(typeof animal.speak == "function"){
        animal.speak();
        return true;
    }
    return false;
}
type(bird);
type(duck);
```
使用条件：事先知道要处理对象的方法 


总结：简单来说，就是把条件判断中后的方法，添加到对应处理对象中去，对使用者来说，只需要调用方法名即可。

## 五大基本原则
### 开放封闭原则（Open Close Principle，OCP）
一个软件实体如类、模块和函数应该对扩展开放，对修改关闭。即软件实体应尽量在不修改原有代码的情况下进行扩展。


尽量少修改代码，因为每次添加新功能如果修改原有方法，很可能导致已经调用这个原有方法的方法出错。


比如：
* 对扩展开放：允许新增子类
*	对修改关闭：如下不需要修改函数running，而可以获得不同的结果，只需传入参数不同。

定义一个running的函数，传入一个参数，此时，我们无需更改running的内容，即可通过改变传入参数的值改变输出内容，当我们调用Animal()类时，running Animal，当我们调用Dog()时候，running Dog.
 
### 里式替换原则（Liskov Substitution Principle，LSP）
所有引用父类的地方必须能透明地使用其子类的对象。这就意味着，父类拥有的所有方法，子类必须也能调用：
1. 调用方式相同
1. 参数相同
1. 返回值类型相同
唯一不同的是，不同的类和对象，实现的具体细节不同
### 依赖倒置原则（Dependence Inversion Principle，DIP）
高层模块不应该依赖底层模块，两者都应该一来起抽象；抽象不应该依赖细节，细节应该依赖抽象。换言之，要针对接口编程，而不是针对实现编程。（调用者为高层,被调用者为低层）
也就是说，只要实现了接口，高层和底层模块都可以被替换。
###	接口隔离原则（ISP，Interface Segregation Principle）


使用多个专门的接口，而不使用单一的总接口，即客户端不应该依赖那些它不需要的接口。


这里的客户端是指调用底层模块的高层模块。


假设定义了一个动物接口，比如动物会走、游泳、飞
 
然后定义一个老虎类，实现动物接口，问题在于，老虎只会走不会飞和游泳（假如这两个都不会），这就出现问题了，老虎实际实现不了这个接口
 
所以我们应该把上面的接口拆开，拆成陆地动物、水中动物和天空动物
 
对于老虎来说，只要实现1个陆地动物接口，对于鸟类来说，需要实现2个接口：陆地动物、天空动物。
###	单一职责原则（SRP）
不要存在多余一个导致类变更的原因，通俗的说，即一个类只负责一项责任。

1.5	内省introspection和反射reflection
1.5.1	python
In computing, type introspection is the ability of a program to examine the type or properties of an object at runtime. Some programming languages possess this capability.
在计算机科学中，内省是指计算机程序在运行时（Run time）检查对象（Object）类型（以及属性等）的一种能力，通常也可以称作运行时类型检查。


方法	作用	类型


help()	查看函数或者模块用途的详细说明	自省


dir()	返回对象所有属性	自省


type()	查看对象类型	自省


isinstance()	判断一个对象是否是一个已知的类型	自省


issubclass()	判断一个类是不是另一个类的子类	自省


id()	返回地址值	自省


callable()	判断对象是否可调用	自省


Introspection should not be confused with reflection, which goes a step further and is the ability for a program to manipulate the values, meta-data, properties and/or functions of an object at runtime.
也就是说自省和反射不是同一回事，自省是获取对象类型的能力，而反射是操纵对象的值，元数据，属性和/或函数的能力。
可以通过字符串的形式来操作对象的属性，有对应的4种方法：


1.	getattr()：获取


2.	hasattr()：查询是否存在


3.	setattr()：修改、新增


4.	delattr()：删除

1.6	类与类之间的关系（python实现）
强弱顺序： 泛化 = 实现 > 组合 > 聚合 > 关联 > 依赖
1、	依赖关系：一个对象以局部变量、方法或参数的形式出现在另一个类
2、	关联关系：成员变量
3、	聚合关系：成员变量，是整体与部分的关系，且部分可以离开整体而单独存在。与关联关系要考察具体逻辑
4、	组合关系：在整体类的构造方法中直接实例化成员类，是整体与部分的关系，但部分不能离开整体而单独存在。
5、	实现关系：类实现某个接口
6、	泛化关系（继承）
1.6.1	依赖关系(Dependency)
是一种使用的关系，即一个类的实现需要另一个类的协助，所以要尽量不使用双向的互相依赖。
【代码表现】：局部变量、方法的参数或者对静态方法的调用。一般表现为在局部变量中使用被依赖类的对象,以被依赖类的对象作为方法参数以及使用被依赖类的静态方法.
【箭头及指向】：带箭头的虚线，指向被使用者
 
假如有一艘宇宙飞船，需要去某个行星上补充能量，显然这种补充是临时性的，偶然性的，而又依赖与行星本身的特性，这里只提到两个相关，1、资源，2、行星的重量，因为行星越重补充完资源要摆脱行星消耗就越大。实际代码中体现的是行星变成某个补充能量方法的参数，具体实现如下：
import math

class SolarSystemPlanet:
    position = 'galaxy'

    def __init__(self, r=999, weight=888, resources=956):
        self.r = r
        self.weight = weight
        self.resources = resources

    def rotation(self):
        print('speed:', 2*math.pi*self.r)

class Spaceship:
    def __init__(self, energy):
        self.energy = energy

    def add_energy(self, star):
        self.energy = star.resources - star.weight*0.01

# 在飞行过程中遇到了planet1这颗普通的行星，普通到参数都可以使用默认值
planet1 = SolarSystemPlanet()
# 这是宇宙飞船，到这里的时候能量只有10了
ship1 = Spaceship(10)
ship1.add_energy(planet1)
print(ship1.energy)  # 947.12
1.6.1.1	依赖关系与关联关系
关联关系：某个类以成员变量的形式出现在另一个类中，体现的是两个类、或者类与接口之间语义级别的一种强依赖关系，比如我和我的朋友；这种关系比依赖更强、不存在依赖关系的偶然性、关系也不是临时性的，一般是长期性的，而且双方的关系一般是平等的。
依赖关系：某个类以局部变量的形式出现在另一个类中，类A使用到了另一个类B，而这种使用关系是具有偶然性的、临时性的、非常弱的，但是B类的变化会影响到A；比如某人要过河，需要借用一条船，此时人与船之间的关系就是依赖；表现在代码层面，为类B作为参数被类A在某个method方法中使用
1.6.2	关联关系（Association)
是一种拥有的关系，它使一个类知道另一个类的属性和方法；如：老师与学生，丈夫与妻子关联可以是双向的，也可以是单向的。双向的关联可以有两个箭头或者没有箭头，单向的关联有一个箭头。
【代码体现】：成员变量
 
关联关系的关键是找到某种联系，而这种联系将不同的实体联系在一起：比如朋友关系将朋友联系在一起，很多朋友会相互打电话一起出去玩，夫妻关系把一些男女联系在一起，而不同的联系情况应该有不同的表现，比如如果定义是同事，就不应该有过多超过朋友范围的行为。
还是用宇宙飞船做例子，假如两艘宇宙飞船是友军。下面将新增一个属性表示友军
```python
class Spaceship:
    def __init__(self, name, energy, friend):
        self.name = name
        self.friend = friend
        self.energy = energy

    def add_energy(self, name, star):
        self.energy = star.resources - star.weight*0.01


# 实例化两艘飞船
ship1 = Spaceship('Eva', 100, 30)
ship2 = Spaceship('Freedom', 200, 11)
# 绑定关联关系
ship1.friend = ship2
ship2.friend = ship1
print(ship1.name) # Eva
print(ship1.friend.name) # Freedom
不过其实一般来说比如友军是会有很多个的，我们当然可以将现在的存储一个对象改为list，从而存储多个对象，不过显然的实际友军是多对多关系（同一个人的两个朋友之间不一定还是朋友），所以可以另外新增一个对象，专门用来存储这种关系。
class Spaceship:
    def __init__(self, name, energy):
        self.name = name
        self.energy = energy

    def add_energy(self, name, star):
        self.energy = star.resources - star.weight*0.01


class Friend:
    friend_list = []

    def add_fri(self, obj1, obj2):
        # 判断关系是否存在，不存在就添加
        if [obj1, obj2] in self.friend_list or [obj2, obj1] in self.friend_list:
            return '已经存在'
        self.friend_list.append([obj1, obj2])
        return True
    
    # 获取所有友军信息
    def get_fri(self, obj):
        temp = []
        for item in self.friend_list:
            if obj in item:
              temp.append(item)
        return temp


# 实例化两艘飞船
ship1 = Spaceship('Eva', 100, 30)
ship2 = Spaceship('Fr', 200, 11)
ship3 = Spaceship('Free', 200, 11)
ship4 = Spaceship('Freedom', 200, 11)
# 实例化关系
friend = Friend()
print(friend.add_fri(ship1, ship2))  # True
print(friend.add_fri(ship2, ship1))  # 已经存在
print(friend.add_fri(ship1, ship3))  # True
print(friend.add_fri(ship2, ship3))  # True
fris = friend.get_fri(ship1)
for item in fris:
    print(item[0].name, item[1].name)
 ```
1.6.3	组合关系(Composition)
是整体与部分的关系，但部分不能离开整体而单独存在。如公司和部门是整体和部分的关系，没有公司就不存在部门。
组合关系是关联关系的一种，是比聚合关系还要强的关系，它要求普通的聚合关系中代表整体的对象负责代表部分的对象的生命周期。
【代码体现】：成员变量，组合关系在代码上体现为在整体类的构造方法中直接实例化成员类，因为类组合关系中整体与部分是共生的。
【箭头及指向】：带实心菱形的实线，菱形指向整体
 
如下构造函数就执行了部分零部件的初始化，并且假定某些部件会因为目标能量的不同，需要传入不同的值，而获得不同的材质。
class Part:
    def __init__(self, material=5):
        self.material = material


class Spaceship:
    def __init__(self, name, energy):
        self.name = name
        self.energy = energy
        self.part1 = Part()
        self.part2 = Part(energy*0.2)

    def add_energy(self, star):
        self.energy = star.resources - star.weight*0.01


new_spaceship = Spaceship('NEW', 100)
1.6.4	聚合关系（Aggregation）
是整体与部分的关系，且部分可以离开整体而单独存在。如车和轮胎是整体和部分的关系，轮胎离开车仍然可以存在。
聚合关系是关联关系的一种，是强的关联关系；关联和聚合在语法上无法区分，必须考察具体的逻辑关系。
【代码体现】：成员变量
 
1.6.5	实现关系（Realization）
是一种类与接口的关系，表示类是接口所有特征和行为的实现。
 
1.6.6	泛化关系（Generalization）（继承）
是一种继承关系，表示一般与特殊的关系，它指定了子类如何继承父类的所有特征和行为。
从某个现有的class继承，新的class称为子类（Subclass），被继承的class为基类、父类或超类（Base class、Super class）。通过继承，子类可以扩展父类的功能。
