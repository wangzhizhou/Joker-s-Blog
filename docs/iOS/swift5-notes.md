# 第五次学习 Swift {-_-}

## 基础

全局的代码被认为是程序的入口, 不需要写main函数，行末也不需要写分号

`let` 声明常量，具体值不需要在编译时确定，只要保证赋值一次就可以

`var` 声明变量

声明多个常量或者声明变量都可以在一行中进行。一行声明多个量时，类型写在最后一个量的后面。

变量名可以是几乎任务Unicode, 除了： 空白字符、数学符号、箭头、Uncode字面量表示、行/块绘制字符。变量名也不能以数字开头。如果变量名和保留关键字冲突，可以使用"`keyword`"来区别。尽量避免使用关键字来命名变量。

swift不会进行隐式类型转换，类型转换时必须显示指定，但提供自动类型推断，在给常/变量赋值时，可自动推断值类型，
如果无法自动判断类型，也可以手动指定类型

字符串使用`"string"`声明，可以使用`\()`进行字符串格式化

可以使用三引号`”“”`来定义多行文本，每一行文本缩进和结束符不一致的部分会被去掉。结束符必须单独写在一行上，用来控制缩进生效的位置


使用`[]`来创建`数组`和`字典`，同样使用`[]`加`下标/键值`来访问数组元素和字典值，最后一个元素可加可不加逗号，定义空数组和空字典语法: `[ElemType]()`/`[KeyType: ValueType]()`
, 如果类型可以推断出来也可以不写类型

## 控制语法

使用`if`和`switch`来进行条件判断，使用`for-in`、`while`和`repeat-while`来进行循环语句，条件可以的小括号可`()`以省略，但语句块的花括号`{}`不能省略。条件语句必须是布尔表达式，不能进行隐式条件判断。

`Optional`表示值可有可无的类型，有值时为具体类型值，无值时为`nil`。可以配合`if-let`使用，没有值被认为是条件语句不成立，不会执行if语句体，如果有值会被解包到let定义的变量，并且在if语句体内有效。声明`Optional`类型的变量时，只要在其它正常类型后面加一个`?`就可以了。

使用`??`可以给`Optional`类型提供默认值。如果`Optional`类型没有值，则使用`??`定义的默认值。

`switch`支持任意类型的数据和多种比较运算符, 可以配合`let/var`以及多种语句完成模式匹配等高级操作，不局限于整型数据和判断是否相等这种简单操作。`case`语句默认不会连续执行，不需要在case块结尾加`break`语句。

`for-in`循环语句遍历数组和字典。`while`来循环执行语句块直到条件改变，条件语句可以在头部也可以在尾部，在尾部时配合`repeat`使用，可以保证循环体语句块至少执行一次。

`..<`可以用来生成半开区间范围，不包含上边界，`...`可以用来生成闭区间范围


## 函数和闭包

使用`func`声明函数，`->`后面接返回值类型，函数的参数标签和参数名是两个不同的东西，默认情况下参数标签和参数名称是一样的，也可以分开指定，或者使用`_`来忽略参数标签的定义。

`tuple`是一种复合类型，它可包含多个值的组合，可以通过名称或者下标数字来访问具体的元素值，函数的返回值如果是多个，可以使用tuple来组合返回

函数是可以嵌套的，嵌套的函数可以访问外层函数的变量，函数是一级类型，函数返回值也可以是其它函数，函数的参数也可以是其它函数

函数是一种特殊类型的闭包，闭包是一段代码块，可以被延迟调用，闭包可以访问它在创建时所在环境的其它变量、函数。闭包也可以看作是一种匿名的函数，在花括号内，使用`in`这个关键字来分割参数返回区和代码区。闭包也可简写，当参数和返回值类型都是已知时，类型定义都可以省略，对于单语句代码块的闭包来说，可以不用写`return`，此时默认把单语句的值当作闭包的返回值。闭包的参数也可以通过数字($0, $1, ...)来访问，这在简写闭包时是很酷的。闭包参数如果是函数的最后一个参数时，可以在调用时写在函数的最末尾处，如果一个函数的参数只有闭包一个时，调用时完全可以不用写参数和小括号，直接把闭包写在函数名的后面。


## 对象和类

类定义使用`class`后接类名称进行，类成员的定义与一般的常量变量定义和函数定义一样，只是把它们的定义放在了class的环境中进行。 创建类实例只是在类名后面接一对小括号`()`，使用`.`来访问类实例成员。实例通过`init`方法创建，释放前会调用`deinit`方法做一些清理工作。类可以声明自己的父类，在类名后面加`:`跟上父类名就行，但类不强制继承父类，所以一个类在定义时没有父类也是可以的。

子类要覆盖父类的同名成员方法需要加关键字`override`, 编译器可以确保不会发生意料之外的方法覆盖问题，编译器对声明要覆盖父类方法但实际上父类并没有对应可被覆盖的方法这种情况也会提示出来。

实例属性可以拥有`getter`和`setter`, 在变量读写时进行相关操作提供了方便。`setter`的默认参数名为`newValue`, 也可以在`setter`的参数中显式的指定参数名称。

类的初始化器里面分为三个部分： 

1. 设置子类自己的属性值
2. 调用父类的初始化器
3. 设置父类的属性值，以及做一些其它的初始化配置工作

实例属性还可以设置`willSet`和`didSet`代码块，这些代码可以成员变量初始化之后任何时候被改变时被调用。

在`Optional`类型实例上调用成员或者方法时可以配合`?`一起使用，如果当前`Optional`实例没有值，则`?`后面的所有操作都不执行，并且整个表达式的值为`nil`, 如果当前`Optional`实例有值，它会被解包后访问其具体的成员变量或者成员方法，这两种情况下，整个表达式结束的值类型都是`Optional`类型


## 枚举和结构体

使用`enum`来定义枚举，枚举类型也可以有自己的方法。默认枚举项的值从`0`开始，按步长`1`递增，也以指定枚举项的值。枚举项的值类型可以是整型、字符串或者浮点型，使用`rawValue`来访问枚举项的实际值。可能通过实际值来生成枚举项，不过这种方式创建的枚举项是`Optional`类型的枚举值，因为如果实际值不包含在已经定义的枚举项范围内时是不能生成有效枚举的。如果在定义枚举项时，枚举项不需要具体的实际值，完全可以不写赋值的部分。

定义枚举项时可以为枚举项设置附加值，附加值在生成枚举实例时指定，每个实例的同一个枚举项的附加值可以不同。

## 协议和扩展

使用protocol声明协议，类、枚举、结构体都可以继承协议。类方法总是可修改这个类的成员，但是结构体不一样，结构体的方法修改结构体要用`mutating`标识.

扩展可以给现有的类型添加新的功能，使用extension定义。扩展可以为现有类型添加计算属性和方法、继承新协议或其它类型。可以把协议当作类型来使用，这种情况下，协议类型的实例不能调用协议定义之外的方法和属性。

## 错误处理

处理错误的类型都可以继承协议`Error`，使用`throw`来抛出错误，使用`throws`来标识一个函数会抛出错误给调用都来处理。

有多种方法处理错误，`do-catch`在do代码块中可以在抛出错误的代码前加上try关键字，catch
代码块中捕获到错误会默认命名为error，除非手动指定其它名称。也可以写多个catch语句块来处理特定类型的错误，catch后面也可以使用像case模式匹配的方式。

使用`try?`前缀会抛出错误的代码，如果代码抛出错误，那么抛出的错误被丢弃，整个语句的结果为nil。如果语句没有抛出错误，语句的结果为包含执行结果的`Optional`类型

`defer`指定的代码块会在函数执行`return`前一刻被调用， 不管函数有没有抛出错误，也不管defer语句块写函数内的哪个位置


## 范型

类、枚举、结构体、函数都可以定义为范型，使用尖括号`<GenericType>`，定义的范型类型还可以和`where`语名配合来限制范型类型需要满足的约束条件。`<T: Equatable>` 和 `<T> where T: Equatable`意思一样



