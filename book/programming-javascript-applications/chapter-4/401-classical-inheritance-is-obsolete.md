# [译] [PJA] [401] 传统的继承已经过时了

> * Original: [Classical Inheritance is Obsolete - Chapter 4. Objects - Programming JavaScript Applications](http://chimera.labs.oreilly.com/books/1234000000262/ch04.html#chcss2i1z00025eilzn6ki8ds)
> * Translated by: [cssmagic](https://github.com/cssmagic)

## Classical Inheritance is Obsolete

> "Those who are unaware they are walking in darkness will never seek the light."

> \-- Bruce Lee
> 
> 不知道自己正在走在黑暗中的人是永远不会去搜寻光明的。
> 
> ——李小龙

In "Design Patterns: Elements of Reusable Object Oriented Software", the Gang of Four opened the book with two foundational principles of object oriented design:

在《设计模式：可复用面向对象软件的基础》一书的开头，“四人帮”就推出了面向对象设计的两大基本原则：（译注：该书由四位作者合著，均为国际公认的面向对象软件领域的专家。）

1. Program to an interface, not an implementation.

2. _Favor object composition over class inheritance._

1. 面向接口编程，而非面向实现编程。

2. *优先使用对象组合，而非继承。*

In a sense, the second principle could follow from the first, because inheritance exposes the parent class to all child classes. The child classes are all programming to an implementation, not an interface. Classical inheritance breaks the principle of encapsulation, and tightly couples the child class to its ancestors.

从某种意义上说，第二条规则可由第一条推导出来，因为继承把父类暴躁给了所有子类。子类都是面向实现编程，而非面向接口。传统的继承打破了封装的原则，而且把子类和它的祖先紧密地耦合起来了。

Think of it this way: _Classical inheritance is like Ikea furniture_. You have a bunch of pieces that are designed to fit together in a very specific way. If everything goes exactly according to plan, chances are high that you'll come out with a usable piece of furniture, but if anything at all goes wrong or deviates from the preplanned specification, there is little room for adjustment or flexibility. Here's where the analogy (and the furniture, and the software) breaks down: The design is in a constant state of change.

不妨从这个角度来想：*传统的继承类似于宜家的家具。*你有一堆零件，设计为以一种非常特定的方式来组装到一起。如果每个零件都严格按照计划进行，会有很高的机会你会拿出一个有用的家具零件；但如果任何零件装错了，或偏离了预定计划的说明书，那就没有多少空间可以调整或机动了。这就是这个比喻（家具或是软件）崩溃的原因：这种设计处在一种变化的恒定状态。

_Composition is more like Lego blocks_. The various pieces aren't designed to fit with any specific piece. Instead, they are all designed to fit together with any other piece, with few exceptions.

*而组合更像是乐高积木块*。不同的零件被设计为可以和任何特定的零件组合。与上面所述不同的是，每一块积木都被设计为可以任意其它零件组合，几乎没有例外。

When you design for classical inheritance, you design a child class to inherit from a specific parent class. The specific parent class name is usually hard coded right in the child class, with no mechanism to override it. Right from the start, you're boxing yourself in -- limiting the ways that you can reuse your code without rethinking its design at a fundamental level.

当你在设计传统的继承时，你设计一个子类来继承自一个特定的父类。这个特定的父类的名称通常在子类写死了，而没有任何机制可以覆盖掉它。而从一开始，你就在跟自己搏斗——限制了你重用你的代码的方法，而没有在一个基本原则的层面去重新思考它的设计。

When you design for composition, the sky is the limit. As long as you can successfully avoid colliding with properties from other source objects, objects can be composed and reused virtually any way you see fit. Once you get the hang of it, composition affords a tremendous amount of freedom compared to classical inheritance. For people who have been immersed in classical inheritance for years, and learn how to take real advantage of composition (specifically using prototypal techniques), it is literally like walking out of a dark tunnel into the light and seeing a whole new world of possibilities open up for you.

当你在设计组合方式的时候，那就是一片海阔天空。只要你可以成功地避免其它对象引入的属性冲突，对象实际上就可以以任何你认为合适的方式进行组合和重用。一旦你掌握到其中的技巧，相对于类的继承，组合将赋予你极大的自由。对于那些在类继承中已经沉浸多年而且学着如何真正领悟组合的好处（尤其是使用原型方面的技巧）的人来说，就像是真正地走出一条黑暗的地道，步入光明，发现一个全新的世界向你敞开无限可能的大门。

Back to "Design Patterns". Why is the seminal work on Object Oriented design so distinctly anti-inheritance? Because inheritance causes several problems:

回到“设计模式”。为什么这项在面向对象方面意义深远的著作会如此旗帜鲜明地反对继承？因为继承会导致以下问题：

  1. _Tight coupling._ Inheritance is the tightest coupling available in OO design. Descendant classes have an intimate knowledge of their ancestor classes.

强耦合。在 OO 设计中，继承是所能找到的最强的耦合方式。所有后代类都对它们的祖先类十分了解。

  2. _Inflexible hierarchies._ Single parent hierarchies are rarely capable of describing all possible use cases. Eventually, all hierarchies are "wrong" for new uses -- a problem that necessitates code duplication.

不灵活的等级制度。单个父类的等级很少有能力可以描述所有用例的可能性。最终，所有等级对新用法来说都是“错误”的——有一个问题就是代码复制变得必要。

  3. _Multiple inheritance is complicated._ It's often desirable to inherit from more than one parent. That process is inordinately complex and its implementation is inconsistent with the process for single inheritance, which makes it harder to read and understand.

多重继承十分复杂。从多于一个父类继承有时会很诱人。这种方法非常复杂，并且它的实现与单继承的方式不一致，这将导致它难于阅读和理解。

  4. _Brittle architecture._ Because of tight coupling, it's often difficult to refactor a class with the "wrong" design, because much existing functionality depends on the existing design.

脆弱的架构。由于强耦合的存在，在“错误”的设计下重构一个类变得非常困难，因为太多已存在的功能依赖这种已存在的设计。

  5. _The Gorilla / Banana problem._ Often there are parts of the parent that you don't want to inherit. Subclassing allows you to override properties from the parent, but it doesn't allow you to select which properties you want to inherit.

大猩猩与香蕉问题。父类总会有某些部分是你不想继承的。子类允许你从父类中覆盖属性，但它不允许你选择哪些属性是你想继承的。

These problems are summed up nicely by Joe Armstrong in "Coders at Work", by Peter Siebel:

这些问题都已经被  很好地总结在了《》一书中，该书由  联合执笔。

> “The problem with object-oriented languages is they've got all this implicit environment that they carry around with them. You wanted a banana but what you got was a gorilla holding the banana and the entire jungle.”

> \-- Joe Armstrong

> 面向对象语言与生俱来的问题是它们与生俱来的这个暗示环境。你想要一根香蕉，但你得到的是一头手里握着香蕉的大猩猩，甚至整个丛林。

Inheritance works beautifully for a short time, but eventually the app architecture becomes arthritic. When you've built up your entire app on a foundation of classical inheritance, the dependencies on ancestors run so deep that even reusing or changing trivial amounts of code can turn into a gigantic refactor. Deep inheritance trees are brittle, inflexible, and difficult to extend.

在短时间内，继承会工作得很完美，但最终应用架构会变得僵硬迟缓。当你已经在一个类继承体系上建立起你的整个应用之后，对祖先的依赖关系如此之深，以致于甚至重用或改变一些细节末节的代码都将一场大规格的重构。深度继承树是脆弱的、不灵活的、难于扩展。

More often than not, what you wind up with in a mature classical OO application is a range of possible ancestors to inherit from, all with slightly different but often similar configurations. Figuring out which to use is not straightforward, and you soon have a haphazard collection of similar objects with unexpectedly divergent properties. Around this time, people start throwing around the word "rewrite" as if it's an easier undertaking than refactoring the current mess.

多半时候，你在一个成熟的类 OO 应用程序中搅和进去的东西，是一堆可以用来继承的祖先类，它们都有着细微的差别，但又常常具有相似的配置。分辨出哪个可用并不是那么简单，而且你很快有一个关于相似对象的无意识的集合，伴随着意想不到的分裂属性。

Many of the patterns in the GoF book were designed specifically to address these well-known problems. In many ways, the book itself can be read as a critique of the shortcomings of most classical OO languages, along with the accompanying lengthy work-arounds. In short, patterns point out deficiencies in the language. You can reproduce all of the GoF patterns in JavaScript, but before you start using them as blueprints for your JavaScript code, you'll want to get a good handle on JavaScript's prototypal and functional capabilities.

四人帮的书里的很多模式都被特别设计成讲解这些著名的问题。这本书自身可以当作对大多数面向对象语言的缺陷的批判来读，同时书中也提供了冗长的变通解决方案。简单来说，设计模式指出了语言中的短板。你可以用 js 重现书中的所有模式，但在你开始将它们当作你的 js 代码的蓝图之前，你会想好好地掌握一下 javas 的原型化和函数式能力。

For a long time, many people were confused about whether JavaScript is truly object oriented, because they felt that it lacked features from other OO languages. Setting aside the fact that JavaScript handles classical inheritance with less code than most class-based languages, coming to JavaScript and asking how to do classical inheritance is like picking up a touch screen mobile phone and asking where the rotary dial is. Of course people will be amused when the next thing out of your mouth is, "if it doesn't have a rotary dial, it's not a telephone!"

在很长一段时间内，很多人都对 js 是否是一门真正的 OO 语言感到疑惑，因为他们感觉它缺少其它 OO 语言的一些特性。暂不提 js 只用更少的代码相比大多数基于类的语言就可以搞定类继承，刚接触 js 就问如何实现类继承就好像捡起一部触屏手机然后问别人它的拨号转盘在什么地方。当然人们也会被逗乐，当你说下面这句话的时候：“它没有拨号转盘，它不是电话机”。

JavaScript can do most of the OO things you're accustomed to in other languages, such as inheritance, data privacy, polymorphism, and so on. However, JavaScript has many native capabilities that make some classical OO features and patterns obsolete. It's better to stop asking "how do I do classical inheritance in JavaScript?", and start asking, "what cool new things does JavaScript enable me to do?"

js 可以做几乎所有你在其它语言中所做的 OO 事情，比如继承、数据私有化、多态等等。然而，js 有很多原生能力可以让一些经典的 OO 特性和模块变得过时。最好别再问“怎样在 js 中实现传统的继承”这种问题。

I wish I could tell you that you'll never have to deal with classical inheritance in JavaScript. Unfortunately, because classical inheritance is easy to mimic in JavaScript, and many people come from class-based programming backgrounds, there are several popular libraries which feature classical inheritance prominently, including Backbone.js, which you'll have a chance to explore soon. When you do encounter situations in which you're forced to subclass by other programmers, keep in mind that inheritance hierarchies should be kept as small as possible. Avoid subclassing subclasses, remember that you can mix and match different code, reuse styles, and things will go more smoothly.

我希望我可以告诉你你永远不需要在 js 中处理传统的继承。不幸的是，由于传统继承在 js 中很容易模似，很人具有基于类的程序背景，很一些流行的类库特别引入了传统继承特性，包括 bb.js，我们很快会有机会支探索它。当你确实要遇到了不得不使用其它程序员的子类的情况时，请牢记继承层级应该保持得尽量少。避免创建子类的子类，记住你可以混合和匹配不同的代码，重用样式，然后事情会变得更加顺利。

***

&copy; Creative Commons BY-NC-ND 3.0 &nbsp; | &nbsp; [我要订阅](http://www.cssmagic.net/blog/subscribe) &nbsp; | &nbsp; [我要捐助](http://www.cssmagic.net/blog/donate)

&nbsp;
> * [参与评论](https://github.com/cssmagic/blog/issues/XXXXXXXXXX)
> * [查看更多文章](https://github.com/cssmagic/blog/issues?state=open)
