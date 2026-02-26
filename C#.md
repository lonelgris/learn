# C#语法概述

## 一、C#基础概念

### 1.1 类与对象
#### 1.1.1 �?Classes)
类的定义是从class开始，后面跟类的名称类的主题，一般形式如下：
```csharp
<access specifier> class class_name 
{
    //成员变量
    <access specifier> <data type> variable1;

    ///成员方法
    <access specifier> <return type> method1(parameter_list) 
    {
        
    }		
}
```

特点�?
1. `<access specifier>` 指定了对类或者成员的访问规则，如果没有指定，则使用默认的访问标识符，类的默认标识符是internal 表示的是只有此命名空间可以被调用，如果是public 表示该类不止在当前命名空间可以被调用，其他命名空间也可以被调用，成员的默认访问是private
2. `<data type>` 指定了变量类�?`<return type>` 表示了返回类�?
3. 如果要访问类的成员可以用(.)运算�?
4. 形如 `myclass mc = new myclass()` 创建对象的时候，将在托管堆上面分配内存，并由GC回收
5. 类是引用类型
6. 类完全支持单一继承，不支持多重继承，但是可以通过接口实现多重继承
7. Sealed关键字修饰符可阻止其他类继承该类 形如：`sealed class B` 这个时候就没有类可以在继承B

#### 1.1.2 结构�?Structs)
结构体的关键字是从struct开始，结构体是值类型，一般形式如下：
```csharp
struct Books
{
   public string title;
   public string author;
   public string subject;
}
```

在C#结构体的特征如下�?
1. 结构体中可以带方法，字段，索引，属性，运算符方法和事件
2. 可以定义构造函数，但是不能定义析构函数，不可以定义无参构造函�?
3. 结构不能继承其他的结构或�?
4. 结构不能作为其他结构或类的基础结构
5. 结构可以实现一个或多个接口
6. 结构体成员不能指定abstract，virtual或者protected属�?
7. 当你使用new操作符来构建一个结构对象的时候，会调用合适的构造函数来构造，与类不同，结构可以不使用new操作符就可以被实例化

#### 1.1.3 类vs结构�?
1. 类是引用类型，结构是值类�?
2. 结构不支持继�?
3. 结构不能声明默认的构造函�?
4. 结构体中声明的字段无法赋予初值，类可�?
5. 结构体的构造函数，必须为结构体所有字段赋值，类的构造无此限�?

#### 1.1.4 类与结构的选择
类的对象是储存在了堆中，结构是在栈中，堆空间大，但是访问速度慢，栈空间小，但是访问速度快，所以描述一个轻量级的对象时候可以用结构，提高效率，但是假如我们是用过来传值的时候希望传递的是引用而不是对象的拷贝的时候，这个时候类合适�?

#### 1.1.5 静态类(Static classes)
主要特性：
1. 仅包含静态成�?
2. 无法实例�?
3. 静态类的本质是一个抽象密封类，所以不能被继承，也不能被实例化
4. 不能包含实例构造函�?
5. 如果一个类下面所有的成员需要被共享，可以设计成静态类

### 1.2 属性与访问�?
#### 1.2.1 属�?Properties)
1. 属性是类，结构，接口的命名成员。类或者结构体中的成员变量或者方法，称作是域Field，属性Property是域的扩展，并且可以使用相同的语法来访问，他们使用访问器Accessors让私有域的值可以被读写或者操�?
2. 访问器（Accessors）声明可包含一个get访问器，一个set访问器，或者同时包含，形如下：
```csharp
// 声明类型�?string �?Code 属�?
public string Code
{
   get
   {
      return code;
   }
   set
   {
      code = value;
   }
}
```

#### 1.2.2 抽象属�?Abstract Properties)
抽象类可拥有抽象属性，这些属性应该在派生类中被实现�?

#### 1.2.3 自动属�?Auto-Implemented properties)
自动生成属性方法，声明更简�?形如下：
```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
}
```

#### 1.2.4 属性访问控�?Getter/setter separate accessibility)
1. 通过 getter/setter 访问字段有如下好�?
Getter/setter 是函数，允许你检查处理输入输出，而public 不行
通过getter/setter 来访问字段，可以使某个字段只读或者只写，而字段不�?

#### 1.2.5 自动属性初始化表达�?
1. 形如如下代码的表�?
```csharp
public class Person
{
    public string FirstName { get; set; }
}
```

2. 属性初始化为其类型默认值以外的�?
```csharp
public class Person
{
    public string FirstName { get; set; } = string.Empty;
}
```

3. 还可以自定义存储
```csharp
public class Person
{
    public string FirstName
    {
        get { return firstName; }
        set { firstName = value; }
    }
    private string firstName;
}
```

4. 属性实现是单个表达式时，可�?getter �?setter 使用 expression-bodied 成员
```csharp
public class Person
{
    public string FirstName
    {
        get => firstName;
        set => firstName = value;
    }
    private string firstName;
}
```

#### 1.2.6 仅限init的属�?
1. init访问器定义的属性仅在构造时可以赋值，实例化之后属性就变成只读�?
2. 语法
```csharp
public int? Age { get; init; }
```
年龄属性是根据生日属性计算出来了，适合使用init访问�?

### 1.3 数据类型与变�?
#### 1.3.1 枚举类型(Enum)
1. 枚举是一组命名的整型常量，用enum关键字声�?
2. C#的枚举也是值类型，并且不能被继承和传递继�?

#### 1.3.2 隐式类型变量(Implicitly typed local variables)
用var声明的变�?

#### 1.3.3 可为空的类型(Nullable Types)
1. 因为net中类型可分为值类型和引用类型，值类型不能为空，引用类型可以为空，在这样的前提下所有的值类型都会给予一个初始值，那么在这种情况下因为数据库中对应的值类型是可以为空的，所以就会造成两者补能对应的尴尬地步，所以在c#2.0中引入了可为空的值类型，强调一点的是可空类型是对于值类型而言不是对应引用类型�?
2. 值值类型后加上？就可以定义为可为空的值类�?例如�?
Int j ? = null
3. 可空类型不是net中的新的数据类型，实际上空类型在定义的net库中式一种泛型类system.nullable<T>
4. 可空类型不是一种真正的类型，而是一个对�?

#### 1.3.4 字面�?Literals)
不通过构造函数来创建�?
1. String Literal
在字符串前加@ 则该字符串不专义，且遇到下一个时终结
在字符串中使用\u或者\x为前缀且紧�?位数字，则自动转化为相应的Unicode字符

2. Numeric literal
数字后面加L或者l 表示该数字为长整�?Int64)
数字后加F或者f 表示该数字为单精�?Single)
数字后加D或者d 表示该数字为双精�?Double)

#### 1.3.5 原义标识�?@)
@特殊字符用作原义标识符具有以下用�?
1. 使用c#关键字作为标识符,@z字符可作为代码元素的前缀，编译器将把此代码元素解析为标识符而非c#的关键字，比如for 改为@for
2. 指示将原义解释为字符�?
3. 使编译器在命名冲突的情况下区分两种属�?

#### 1.3.6 匿名类型
形如下的类型�?
```csharp
var author = new
{
  FirstName = "Joydip",
  LastName = "Kanjilal",
  Address = "Hyderabad, INDIA"
};
```

#### 1.3.7 记录类型
1. Record是引用类型，和class差不多，但是为什么还要新增呢，比如有如下的例�?
```csharp
Public class Dog
{
    Public string nickname(get;set)
    Public string age(get;set;)
}
```

这个时候如果用class来生�?
```csharp
Dog dog1 = new Dog
{
    Nickname = "泰迪1",
    Age = "12"
};

Dog dog2 = new Dog
{
    Nickname = "泰迪1",
    Age = "12"
};
```

这个时候去输出 console.Writeline(dog1 == dog2)
这个时候发现结果居然是false

这是因为class下关心的只是引用是否为同一个实例，并不关心内容是否相等

如果把class换成record
```csharp
Public record Dog
{
    Public string nickname(get;set)
    Public string age(get;set;)
}
```

在去输出 console.Writeline(dog1 == dog2)
发现结果是true

其实是record 类型让你省去了重写相等比较（重写Equals、GetHashCode 等方法或重载运算符）的逻辑�?
实际上，代码在编译后record 类型也是一个类，但自动实现了成员相等比较的逻辑。以前你要手动去折腾的事现在全交给编译器去干

2. 对象克隆
Record提供了with表达式来方便地克隆一个新的对象，所以在需要克隆的时候可以考虑使用record，另外所有原型模式的地方都可以考虑使用record来实�?

#### 1.3.8 本机大小的整�?
有符号nint和无符号nuint
例子
```csharp
nint nativeInt = 55;
Console.WriteLine(nint.MaxValue);
// �?x86 平台上， 输出�?2147483647
// �?x64 平台上， 输出�?9223372036854775807
```

优点：可以更好的兼容原生API�?
缺点：缺失平台无关性；

### 1.4 装箱和取消装�?
简单的来说装箱就是将值类型转换为引用类型，取消装箱是将引用类型转为值类�?
C#的值类型和引用类型都是继承自object类型，也就是说值类型其实也可以被当做引用类型来处理

Net中，数据类型被划分为值类型和引用类型，与此对应的内存也会被分为两种方�?一种为栈，一种为堆，此处的堆为托管堆

1. 装箱操作
首先从托管堆中为新生成的引用对象分配内存
然后将值类型的数据拷贝到刚刚新分配的内存中
返回托管堆中重新分配的对象地址
从这3步可以看出进行一次装箱操作要进行内存分配和数据拷贝这两项比较消耗性能
	
2. 拆箱操作
首先获取从托管堆中属于值类型的那部分字段的地址
将引用对象的值拷贝到线程堆栈上的值类型的实例中去
从这两部来看，可以认为同装箱是互反的操作，并不影响性能，但是这之后的拷贝数据操作还是一样影响性能

3. 为什么要装箱
因为object 可以是任意类型，所以可以以便通用处理数据

4. 装箱/拆箱的执行效�?
显然从上面的执行步骤来看。我们应该尽量避免装箱，但是万事不是绝对，比如你想改造的代码为第三方程序集，你没有法子更改那么就只能装箱�?

## 二、C#1.2

### 1.2.1 Dispose in foreach
�?IEnumerator 实现 IDisposable 时，foreach 循环中生成的代码会在 IEnumerator 上调�?Dispose�?

### 1.2.2 foreach over string specialization
foreach上的字符串特�?

## 三�?C#2.0

### 2.0.1 泛型(Generics)
1. 泛型运行你延迟编写类或者方法的编程元素的数据类型的规范，也可以这样说，泛型允许你编写一个可以和任何类型一起工作的类或者方�?
2. 泛型的委�?举例
Delegate T numberChanger<T>(T n)

3. 泛型约束条件
T :结构(类型参数必须是值类�?
T:�?类型必须是引用类型，包括任何的类，接口，委托，数组类�?
T:new()(类型参数必须具有无参数的公共构造函�?
T:<基类�?(类型参数必须是指定的基类或者派送自指定的基�?
T:<接口名称>(类型参数必须是知道的接口或实现指定的接口，可以指定多个接口约束，约束接口也可以是泛型)

4. 分部类和方法(Partial Types)
主要作用是将类，结构，接口等类型分拆到多个不同的文件当中去，以便简化开发和维护

5. 匿名方法(Anonymous Methods)
因为在c#2.0之前，声明委托的唯一方法是使用命名方法，2.0以后可以用匿名方法来处理
如果使用匿名方法，就不在需要单独的创建方法，因此减少了实例化委托所需的编码的开销
如果局部变量和参数的范围包含匿名方法声明，则局部变量和参数称为该匿名方法的外部变量或捕获变量，外部变量的生命周期一直持续到该匿名方法委托符合垃圾回收条件为�?
匿名方法不能访问外部的ref或者out参数
在匿名方法块中不能访问任何不安全的代码
不能在匿名方法快内使用跳转语句比如goto，break，conitnue

6. 迭代�?Iterators)
在c#1.0时候只能使用foreach来循环集合，自己实现迭代器也很麻烦，所以在c#2.0以后实现的迭代器可以拙步迭代集合，迭代器方法使用yield return 语句返回元素，每次返回一个到�?yield teturn 语句时候，会记住当前代码中的位置，下次在迭代的时候就可以从该位置重新开始啦

7. 可为空的类型(Nullable Types)
1. 因为net中类型可分为值类型和引用类型，值类型不能为空，引用类型可以为空，在这样的前提下所有的值类型都会给予一个初始值，那么在这种情况下因为数据库中对应的值类型是可以为空的，所以就会造成两者补能对应的尴尬地步，所以在c#2.0中引入了可为空的值类型，强调一点的是可空类型是对于值类型而言不是对应引用类型�?
2. 值值类型后加上？就可以定义为可为空的值类�?例如�?
Int j ? = null
3. 可空类型不是net中的新的数据类型，实际上空类型在定义的net库中式一种泛型类system.nullable<T>
4. 可空类型不是一种真正的类型，而是一个对�?

8. 属性访问控�?Getter/setter separate accessibility)
1. 通过 getter/setter 访问字段有如下好�?
Getter/setter 是函数，允许你检查处理输入输出，而public 不行
通过getter/setter 来访问字段，可以使某个字段只读或者只写，而字段不�?

9. 方法组转�?Method group conversions (delegates))

可以将声明委托代表成一种方法，隐式调用

10. 协变和逆变(Co- and Contra-variance for delegates and interfaces)
1. 协变
派生程度较大的类型分配或者赋值给派生程度小的，在泛型参数中使用out类型参数修饰�?

2. 逆变
派生类程度较小的分配或者赋值给派生程度较大的，在泛型参数中使用in类型参数修饰�?

11. 静态类(Static classes)
主要特�?
1. 仅包含静态成�?
2. 无法实例�?
3. 静态类的本质是一个抽象密封类，所以不能被继承，也不能被实例化
4. 不能包含实例构造函�?
5. 如果一个类下面所有的成员需要被共享，可以设计成静态类

12. 委托推断(Delegate inference)
将一个方法的地址传送给一个委托变量，编译器会自动检测委托变量的委托类型，然后根据委托类型创建委托实例，并把方法地址传送给委托的构造函数�?

## 四、C#3.0

### 3.0.1 隐式类型变量(Implicitly typed local variables)
用var声明的变�?

### 3.0.2 对象集合初始�?Object and collection initializers)
1. 对象初始�?
对象初始化器由一系列成员对象组成，其对象必须初始化，用逗号间隔，使用{}封闭

2. 集合初始�?
集合初始化器由一系列集合对象组成，用逗号间隔，使用{}封闭

### 3.0.3 自动属�?Auto-Implemented properties)
自动生成属性方法，声明更简�?形如下：
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public int Age { get; set; }
}

### 3.0.4 匿名类型
形如下的类型�?
var author = new
{
  FirstName = "Joydip",
  LastName = "Kanjilal",
  Address = "Hyderabad, INDIA"
};

### 3.0.5 扩展方法(Extension methods)
项目中有需要添加新功能，但是有不想或者不能破坏原来代码，在时候就可以用扩展方法来完成上述功能

### 3.0.6 查询表达�?Query expressions)
有点和sql语句类似的查询代�?

### 3.0.7 lambda表达�?Lambda expression)
1. 表达式作为主�?
(input-parameters) => expression
2. 语句块作为主�?
(input-parameters) => { <sequence-of-statements> }

### 3.0.8 表达式树(Expression trees)
用一种树形数据结构表示代码，其中每一个节点都是一种表达式 net中的linq to sql 就是对表达式的解�?

### 3.0.9 分部方法(Partial methods)
1. 以下条件可以用于分部方法
声明必须上下文关键字partial开�?
分部类型各部分中的签名必须匹配

2. 以下情况不需要分部方法即可实�?
没有任何可访问的修饰符
返回void
没有任何输出参�?
没有以下任何修饰符：virtual，override ，sealed，new 或extern

## 五、C#4.0

### 4.0.1 动态绑�?Dynamic binding)
1. 动态绑�?就是对类型、成员和操作的解析过程。动态绑定意味着与编译器无关，而与运行时有�?

2. 使用关键字dynamic来声�?

### 4.0.2 命名参数和可选参�?Named and optional arguments)
1. 命名参数
一种语法糖代码，可以让你不用在记住和查找形参所调动方法的形参中的顺�?

2. 可选参�?
为一个参数提供默认值就可以将其声明为可选的

### 4.0.5 泛型类型的协变和逆变(Co- and Contra-variance for generic delegates and interfaces)

1. 作用
提供更大的灵活�?

2. 协变
把子类付给父�?

3. 逆变
把父类付给子�?

### 4.0.6 类型等效性和嵌入的互操作类型(Embedded interop types ("NoPIA"))
将com类型的类型信息直接嵌入到托管程序集中，而不要求托管程序集从互操程序集中获取com类型的类型信�?

## 六、C#5.0

### 5.0.1 异步方法(Asynchronous methods)
1. 如果需要IO绑定(例如从网络请求数据，访问数据库，写入到文件系�? 则需要利用异步编�?
2. 异步变成的核心是task和task<T>对象，这两个对象对异步操作建模，他们受关键字async和await的支持，在大多数的情况下模型十分简�?
对应IO绑定代码，等待一个在async方法中返回task或者task<T>的操�?
对于cpu绑定代码.，等待一个使用task.run方法在后台线程启动的操作

### 5.0.2 调用方信息特�?Caller info attributes)
主要用于调试，跟踪，诊断的一些接口信�?

## 七、C#6.0

### 6.0.1 静态导�?
using static 指令指定一种类型，无需指定类型名称即可访问其静态成员和嵌套类型

### 6.0.2 异常筛选器
可以使用上下文关键字when在上下文中指定筛选条�?
在try/catch或者try/catch/finally块中使用
在switch语句的case标签�?
在switch表达式中

### 6.0.3 自动属性初始化表达�?
1. 形如如下代码的表�?
public class Person
{
public string FirstName { get; set; }
}

2. 属性初始化为其类型默认值以外的�?
public class Person
{
public string FirstName { get; set; } = string.Empty;
}

3. 还可以自定义存储
public class Person
{
public string FirstName
{
get { return firstName; }
set { firstName = value; }
}
private string firstName;
}

4. 属性实现是单个表达式时，可�?getter �?setter 使用 expression-bodied 成员
5. public class Person
{
    	public string FirstName
    	{
        	get => firstName;
       	 	set => firstName = value;
    	}
    	private string firstName;
    }

### 6.0.4 Expression bodied 成员
1. 语法
member => expression;

2. 例子
表达式主体定义�?
public override string ToString() => $"{fname} {lname}".Trim();

简化版�?
public override string ToString()
{
   return $"{fname} {lname}".Trim();
}
}

### 6.0.5 Null 传播�?
1. Null 条件运算�??. �??[] 
null 条件运算符才会将成员访问 ?. 或元素访�??[]运算应用于其操作数；否则，将返回 null
如�?a 的计算结果为 null，则 a?.x �?a?[x] 的结果为 null�?
如�?a 的计算结果为�?null，则 a?.x �?a?[x] 的结果将分别�?a.x �?a[x] 的结果相同�?

### 6.0.7 字符串内�?
1. $ 特殊字符将字符串文本标识为内插字符串 �?内插字符串是可能包含内插表达式的字符串文�?�?将内插字符串解析为结果字符串时，带有内插表达式的项会替换为表达式结果的字符串表示形式
2. 结构
{<interpolationExpression>[,<alignment>][:<formatString>]}

### 6.0.8 nameof 表达�?
1. nameof 表达式可生成变量、类型或成员的名称作为字符串常量
2. 实例
Console.WriteLine(nameof(System.Collections.Generic));  // output: Generic
Console.WriteLine(nameof(List<int>));  // output: List
Console.WriteLine(nameof(List<int>.Count));  // output: Count
Console.WriteLine(nameof(List<int>.Add));  // output: Add

var numbers = new List<int> { 1, 2, 3 };
Console.WriteLine(nameof(numbers));  // output: numbers
Console.WriteLine(nameof(numbers.Count));  // output: Count
Console.WriteLine(nameof(numbers.Add));  // output: Add

## 八�?.0版本

### 7.0.1 out变量
1. 现在可以在方法调用的参数列表中声明out 变量，而不需要编写单独的声明语句
if (int.TryParse(input, out int result))
    Console.WriteLine(result);
else
Console.WriteLine("Could not parse input");

2. 支持使用隐式类型的局部变�?
if (int.TryParse(input, out var answer))
    Console.WriteLine(answer);
else
    Console.WriteLine("Could not parse input");

### 7.0.2 元组和析构函�?
1. 元组
1.1 定义
元组是包含多个字段以表示数据成员的轻量级数据结构
	1.2 语法
var tuple  = (a: 5, b: 10);  
//or   var tuple  = (5,10);  
 
 (int a,int b) tuple1 = (5,10);
// or  (int,int) tuple1 = (5,10);

2. 弃元
2.1 定义 
弃元就是使用下划线_作为一个占位符，但不占存储空间
2.2 语法
(_, _, area) = city.GetCityInformation(cityName);

### 7.0.3 模式匹配
1. 定义
在c#中，is是一个关键字，可以用来检查某个数据的类型是否为特定类型，这是一个表达式，返回类型为boolean

2. 在下面这些情况返回true
表达式类型和is类型相符�?
表达式的类型为is类型的派生类�?
表达式具有一个编译时类型，它是is类型的基类，在运行时值为is类型的派生类�?
表达式实现了is类型的接�?
3. 在类型检查的基础上，直接支持类型转换
4. is 后面还可以是常量，is测试表达式的值是否为特定常量
5. 如果is后面是var 则永远为true，并把值赋予后面的变量
6. 支持模式匹配的switch
1. 定义
现在的c#支持类型模式，也就是说在case后面还可以是一个用来检测的类型

### 7.0.4 本地函数
1. 定义
本地方法是一种语法糖，允许我们在方法内定义本地方法。更加类似于函数式语言，但是，本质上还是基于面向对象实现的�?

2. 形如此的函数
public int MyFunction(int parameter)
{
    int local = 6;
    return MyLocalFunction(4);

    // Local Function
    int MyLocalFunction(int localFunctionParameter) => 42;
}

### 7.0.5 已扩�?expression bodied 成员
1. 定义
C# 6 为成员函数和只读属性引入了 expression-bodied 成员�?C# 7.0 扩展了可作为表达式实现的允许的成员�?�?C# 7.0 中，你可以在属性和索引器上实现构造函数、终结器以及 get �?set 访问器�?以下代码演示了每种情况的示例
// Expression-bodied constructor
public ExpressionMembersExample(string label) => this.Label = label;
// Expression-bodied finalizer
~ExpressionMembersExample() => Console.Error.WriteLine("Finalized!");

private string label;

// Expression-bodied get / set accessors.
public string Label
{
    get => label;
    set => this.label = value ?? "Default label";
}

### 7.0.6 Ref 局部变量和返回结果
1. 定义
	ref关键字很早就存在�?但是他只能用于参�?这次C#7.0让他不仅仅只能作为参数传�?还能作为本地变量和返回值了

## 九、C#7.1

### 7.1.1 async main 方法
1. 定义
应用程序的入口点可以含有 async 修饰符�?

2. 语法
static async Task<int> Main()
{
    return await DoAsyncWork();
}

### 7.1.2 default 文本表达�?
1. 定义
在可以推断目标类型的情况下，可在默认值表达式中使用默认文本表达式

2. 语法
Func<string, bool> whereClause = default;

### 7.1.3 推断元组元素名称
1. 定义
在许多情况下，可通过元组初始化来推断元组元素的名�?

### 7.1.4 泛型类型参数的模式匹�?
1. 定义
可以对类型为泛型类型参数的变量使用模式匹配表达式

## 十、C# 7.2

### 7.2.1 编写安全高效代码
无需固定即可访问固定的字段�?
可以重新分�?ref 本地变量�?
可以使�?stackalloc 数组上的初始值设定项�?
可以对支持模式的任何类型使�?fixed 语句�?
可以使用其他泛型约束�?
针对实参的 in 修饰符，指定形参通过引用传递，但不通过调用方法修改�?�?in 修饰符添加到参数是源兼容的更改�?
针对方法返回的 ref readonly 修饰符，指示方法通过引用返回其值，但不允许写入该对象�?如果向某个值赋予返回值，则添�?ref readonly 修饰符是源兼容的更改�?�?readonly 修饰符添加到现有�?ref 返回语句是不兼容的更改�?它要求调用方更新 ref 本地变量的声明以包含 readonly 修饰符�?
readonly struct 声明，指示结构不可变，且应作�?in 参数传递到其成员方法�?�?readonly 修饰符添加到现有的结构声明是二进制兼容的更改�?
ref struct 声明，指示结构类型直接访问托管的内存，且必须始终分配有堆栈�?�?ref 修饰符添加到现有 struct 声明是不兼容的更改�?ref struct 不能是类的成员，也不能用于可能在堆上分配的其他位置�?

### 7.2.2非尾随命名参�?
命名的参数可后接位置参�?

### 7.2.3 数值文字中的前导下划线
数值文字现可在任何打印数字前放置前导下划线，主要是增加可读�?

### 7.2.4 private protected 访问修饰�?
private protected 访问修饰符允许访问同一程序集中的派生类

### 7.2.5 条件ref表达�?
可以引用条件表达式 (?:) 的结�?

## 十一、C#7.3

### 7.3.1 无需固定即可访问固定字段
主要原因是因为gc是根标记回收方法，回收完成以后就会开始进行内存压缩，一旦压缩就会导致指针指向的位置无效或者错乱，之前c#版本是用fixed来固定变�?这个版本以后就不在需要了

### 7.3.2 可以重新分配ref本地变量

### 7.3.3 可以使用stackalloc数组上的初始值设定项
int* pArr = stackalloc int[3] {1, 2, 3};
int* pArr2 = stackalloc int[] {1, 2, 3};
Span<int> arr = stackalloc [] {1, 2, 3};
stackalloc 表达式在堆栈上分配内存块�?该方法返回时，将自动丢弃在方法执行期间创建的堆栈中分配的内存块�?不能显式释放使用 stackalloc 分配的内存�?堆栈中分配的内存块不受垃圾回收的影响，也不必通过 fixed 语句固定�?

### 7.3.4 可以对支持模式的任何类型使用fixed语句
fixed 语句支持有限的一组类型�?�?C# 7.3 开始，任何包含返回 ref T �?ref readonly T �?GetPinnableReference() 方法的类型均有可能为 fixed�?添加此功能意味着 fixed 可与 System.Span<T> 和相关类型配合使用�?

### 7.3.5 可以使用其他泛型约束
现在，可以将类型 System.Enum �?System.Delegate 指定为类型参数的基类约束�?
现在也可以使用新�?unmanaged 约束来指定类型参数必须是不可�?null �?非托管类�?�?
有关详细信息，请参阅有关 where 泛型约束和类型参数的约束的文章�?
将这些约束添加到现有类型是不兼容的更改�?封闭式泛型类型可能不再满足这些新约束的要求�?

### 7.3.6 改进了重载解�?
1. 现在可以正确的区�?Task.Run(Action) �?Task.Run(Func<Task>())�?

## 十二，C#8.0

### 8.0.1 Readonly 成员
可�?readonly 修饰符应用于结构的成员�?它指示该成员不会修改状态�?这比�?readonly 修饰符应用于 struct 声明更精�?

### 8.0.2 默认接口方法
主要是因为菱形问题，还有c#不支持多重继承，同时避免菱形问题，才引入这个方法

C#8.0之前
	interface IExample
{
    void Ex1();                                      // 允许
    void Ex2() => Console.WriteLine("IExample.Ex2"); // 不允�?C# 8 以前)
}

C#8.0以后
interface IExample
{
    void Ex1();                                      // 允许
    void Ex2() => Console.WriteLine("IExample.Ex2"); // 允许
}

### 8.0.3 模式匹配增强功能
1. Switch 表达�?
public static RGBColor FromRainbow(Rainbow colorBand) =>
    colorBand switch
    {
        Rainbow.Red    => new RGBColor(0xFF, 0x00, 0x00),
        Rainbow.Orange => new RGBColor(0xFF, 0x7F, 0x00),
        Rainbow.Yellow => new RGBColor(0xFF, 0xFF, 0x00),
        Rainbow.Green  => new RGBColor(0x00, 0xFF, 0x00),
        Rainbow.Blue   => new RGBColor(0x00, 0x00, 0xFF),
        Rainbow.Indigo => new RGBColor(0x4B, 0x00, 0x82),
        Rainbow.Violet => new RGBColor(0x94, 0x00, 0xD3),
        _              => throw new ArgumentException(message: "invalid enum value", paramName: nameof(colorBand)),
};

语法改进点：
变量位�?switch 关键字之前�?不同的顺序使得在视觉上可以很轻松地区�?switch 表达式和 switch 语句�?
将 case �?: 元素替换�?=>�?它更简洁，更直观�?
将 default 事例替换�?_ 弃元�?
正文是表达式，不是语句�?

2. 属性模�?
定�?
借助属性模式，可以匹配所检查的对象的属�?
例�?
public static decimal ComputeSalesTax(Address location, decimal salePrice) =>
    location switch
    {
        { State: "WA" } => salePrice * 0.06M,
        { State: "MN" } => salePrice * 0.075M,
        { State: "MI" } => salePrice * 0.05M,
        _ => 0M
};

3. 元组模式
public static string RockPaperScissors(string first, string second)
    => (first, second) switch
    {
        ("rock", "paper") => "rock is covered by paper. Paper wins.",
        ("rock", "scissors") => "rock breaks scissors. Rock wins.",
        ("paper", "rock") => "paper covers rock. Paper wins.",
        ("paper", "scissors") => "paper is cut by scissors. Scissors wins.",
        ("scissors", "rock") => "scissors is broken by rock. Rock wins.",
        ("scissors", "paper") => "scissors cuts paper. Scissors wins.",
        (_, _) => "tie"
};

4. 位置模式
定�?
某些类型包含 Deconstruct 方法，该方法将其属性解构为离散变量�?如果可以访问 Deconstruct 方法，就可以使用位置模式检查对象的属性并将这些属性用于模�?

例�?
public class Point
{
    public int X { get; }
    public int Y { get; }

    public Point(int x, int y) => (X, Y) = (x, y);

    public void Deconstruct(out int x, out int y) =>
        (x, y) = (X, Y);
}

### 8.0.4 using 声明
改进了using的写法，不在需要写disposed代码，就可以释放资源
例�?
static int WriteLinesToFile(IEnumerable<string> lines)
{
    using var file = new System.IO.StreamWriter("WriteLines2.txt");
    int skippedLines = 0;
    foreach (string line in lines)
    {
        if (!line.Contains("Second"))
        {
            file.WriteLine(line);
        }
        else
        {
            skippedLines++;
        }
    }
    // Notice how skippedLines is in scope here.
    return skippedLines;
    // file is disposed here
}

### 8.0.5 静态本地函�?
从C# 8 开始，本地方法就可以是静态的了�?
与其他的本地方法不同，静态的本地方法无法捕获任何本地状态量�?

### 8.0.6 可处置的 ref 结构
�?ref 修饰符声明的 struct 可能无法实现任何接口，因此无法实�?IDisposable�?因此，要能够处理 ref struct，它必须有一个可访问�?void Dispose() 方法�?此功能同样适用�?readonly ref struct 声明�?

### 8.0.7 可为空引用类�?
若要指示一个变量可能为 null，必须在类型名称后面附加 ?，以将该变量声明为可为空引用类型

### 8.0.8 异步�?
NET 引入�?async �?await 关键词让异步编程更具有可读性，但有一个遗憾，�?C# 8 之前都不能使用异步的方式处理数据流，直到 C# 8 引入�?IAsyncEnumerable<T> 才解决了这个问题�?

说到 IAsyncEnumerable<T> ，得先说一�?IEnumerable<T> ，大家都知道，它是用同步的方式来迭代 collection 集合的，而这里的 IAsyncEnumerable<T> 则是用异步方式，换句话说�?IAsyncEnumerable<T> 在迭代集合的过程中不会阻塞调用线程�?

### 8.0.9 异步可释�?
语言支持实现 System.IAsyncDisposable 接口的异步可释放类型�?可使�?await using 语句来处理异步可释放对象

### 8.9.10 索引和范�?
1. C�?.0中引入了两个新的运算符，以为您提供所需的全部功能：
�?来自结尾的索�?运算符： ^ ，它指定相对于序列结尾的索引�?�?
�?范围"运算符： .. ，它指定范围的开始和结束�?

2. 注意事项
^0索引与sequence[sequence.Length]相同�?
注意， sequence[^0] 确实会抛出IndexOutOfRangeException ，就像sequence[sequence.Length]一样�?
对于任何数字n ，索引^n与sequence.Length - n相同�?
对于范围，范围的开始是包含�?，但范围的结束是排除�?�?
范围[0..0^]代表整个序列，就像[0..sequence.Length]或[..] �?
范围不需要完全定义，
例�?
[..3] ->给我从数组开始到索引3的所有内容�?
[2..] ->给我从索�?到数组末尾的所有内容�?
[..] ->给我一�?

### 8.9.11 Null 合并赋�?
引入�?null 合并赋值运算符 ??=�?仅当左操作数计算�?null 时，才能使用运算�???= 将其右操作数的值分配给左操作数

### 8.9.12 非托管构造类�?
1. �?C# 7.3 及更低版本中，构造类型（包含至少一个类型参数的类型）不能为非托管类型�?�?C# 8.0 开始，如果构造的值类型仅包含非托管类型的字段，则该类型不受管理�?
2. 例子
Span<Coords<int>> coordinates = stackalloc[]
{
    new Coords<int> { X = 0, Y = 0 },
    new Coords<int> { X = 0, Y = 3 },
    new Coords<int> { X = 4, Y = 0 }
};

Span 是安全可操作的内存块指令

### 8.9.13 嵌套表达式中�?stackalloc
C# 8.0 开始，如果 stackalloc 表达式的结果�?System.Span<T> �?System.ReadOnlySpan<T> 类型，则可以在其他表达式中使�?stackalloc 表达式：
Span<int> numbers = stackalloc[] { 1, 2, 3, 4, 5, 6 };
var ind = numbers.IndexOfAny(stackalloc[] { 2, 4, 6, 8 });
Console.WriteLine(ind);  // output: 1

### 8.9.14 内插逐字字符串的增强功能
内插逐字字符串中 $ �?@ 标记的顺序可以任意安排：$@"..." �?@$"..." 均为有效的内插逐字字符串�?在早�?C# 版本中，$ 标记必须出现�?@ 标记之前�?

## 十三、C#9.0

### 9.0.1 记录类型
1. Recrd 是引用类型，和class差不多，但是为什么还要新增呢�?
比如有如下的例子
Public class Dog
{
	Public string nickname(get;set)
	Public string age(get;set;)
}


这个时候如果用class来生�?
Dog dog1 = new Dog
�?
	Nickname = "泰迪1"
	Age = "12"
�?

Dog dog2 = new Dog
�?
	Nickname = "泰迪1"
	Age = "12"
�?

这个时候去输出 console.Writeline(dog1 == dog2)
 这个时候发现结果居然是false

这是因为class下关心的只是引用是否为同一个实例，并不关心内容是否相等

如果把class换成record
Public record Dog
{
	Public string nickname(get;set)
	Public string age(get;set;)
}

在去输出 console.Writeline(dog1 == dog2)
发现结果是true

其实是record 类型让你省去了重写相等比较（重写Equals、GetHashCode 等方法或重载运算符）的逻辑�?
实际上，代码在编译后record 类型也是一个类，但自动实现了成员相等比较的逻辑。以前你要手动去折腾的事现在全交给编译器去干
2. 对象克隆
第一章record 提供�?with 表达式来方便的克隆一个新的对象，所以在需要克隆的时候可以考虑使用 record，另外所有原型模式的地方都可以考虑使用 record 来实�?

### 9.0.2 仅限init的资料库
1. init访问器定义的属性仅在构造时可以赋值，实例化之后属性就变成只读�?
2. 语法
public int? Age { get; init; }
年龄属性是根据生日属性计算出来了，适合使用init访问�?

### 9.0.3 顶级语句
1. 定义
将Class的定义和主函数Main的声明省略掉，只写出你的核心业务代码，就成了顶级语句

2. 遵守规则
顶级语句必须放在using语句代码后面
顶级语句必须用在任何类型或者命名空间声明的前面
顶级语句只能写在一个源代码文件里，像如今只能写一个main方法一样�?
顶级语句中定义的本地函数和变量，在顶级代码段外部的任何地方调用他们都会产生错误�?

3. 原理
1. 顶级语句最终还是在编译的时候，被作为全局命空间中Program类的Main方法体中一段代码一起自动生�?

static class Program
{
		static async Task Main(string[] args)
		{
       // 顶级语句
		}
}

### 9.0.4 模式匹配增强功能
1. 模式匹配的改�?
类型模式要求在变量是一种类型时匹配
带圆括号的模式强制或强调模式组合的优先�?
联�?and 模式要求两个模式都匹�?
析�?or 模式要求任一模式匹配
否�?not 模式要求模式不匹�?
关系模式要求输入小于、大于、小于等于或大于等于给定常数�?

### 9.0.5 性能和互操作�?
1. 本机大小的整�?
有符号 nit
无符号 nuint
例子
nint nativeInt = 55;
Console.WriteLine(nint.MaxValue);
// �?x86 平台上， 输出�?2147483647
// �?x64 平台上， 输出�?9223372036854775807

优点：可以更好的兼容原生API�?
缺点：缺失平台无关性；

2. 函数指针
使�?delegate* 可以声明函数指针

3. 禁止发出localsinit标识
在 C#9.0 中，可以使用 SkipLocalsInitAttribute 来告知编译器不要发射 (Emit) .locals init 标记�?例子
[System.Runtime.CompilerServices.SkipLocalsInit]
static unsafe void DemoLocalsInit() {
 int x;
 // 注意�?x 没有初始化， 输出结果不确定；
 Console.WriteLine(*&x);
}

### 9.0.6 调整和完成功�?
1. 目标类型的new表达�?
定�?
增加了用户定义类�?new 表达式的目标类型推导，即通过上下文左边自动推�?new 表达式的类型，从而在使用 new 构造时省略类型的指�?

例�?
// C# 9 之前
Point p = new Point(3, 5);

// C# 9
Point p = new (3, 5);

2. 静态匿名函�?
原�?
匿名方法的代价不低，因为他有委托调用方面的开销，如果你的lambda里需要补货封闭方法的局部变量或者参数，那么就会存在两种堆栈分配，一种是委托上的一种是闭包上的分配，所以为了避免不必要的内存分配，c#9.0 引入了static匿名函数

方�?
使用static +const组合在提升应用程序的性能
	
例�?
优化前 y会有内存分配
			int y = 1;
MyMethod(x => x + y);
		
优化后
const int y = 1;
MyMethod(static x => x + y);


3. 目标类型的条件表达式
条件表达式 c ? e1 :e2 定义了新的隐式条件表达式转换，允许从条件表达式到任何类型的隐式转化T，如果条件表达式在和之间既没有通用类型，也不符�?e1 e2 条件表达式转换，则是错误的�?

4. 协变返回类型
允许重写方法的时候返回比她重写的方法更派生的类型

5. 扩展GetEnumerator支持foreach循环
允�?foreach 循环识别扩展方法 GetEnumerator 方法，该方法以其他方式满�?foreach 模式，并在该表达式被视为错误时循环使�?

6. Lambda 弃元参数
允许丢弃 (用作 _ lambda 和匿名方法的参数) 。例如：
lambda�?(_, _) => 0 �?(int _, int _) => 0
匿名方法： delegate(int _, int _) { return 0; }

7. 本地函数的属�?
本地函数声明现在允许�?属性。本地函数上的参数和类型参数也允许有属�?

### 9.0.7 支持代码生成�?
1. 定义
通过使用属性修饰方法，可以将方法指定为模块初始值设定项 [ModuleInitializer] 从而保证允许库在加载时执行预先的一次性初始化，开销最小，用户无需显式调用任何内容

方法例子
using System;
namespace System.Runtime.CompilerServices
{
    [AttributeUsage(AttributeTargets.Method, AllowMultiple = false)]
    public sealed class ModuleInitializerAttribute : Attribute { }
}

属性例�?
using System.Runtime.CompilerServices;
class C
{
    [ModuleInitializer]
    internal static void M1()
    {
        // ...
    }
}

### 9.0.8 分部方法的新功能
通过使用分部方法，可以将一个类型中的操作分散在多个文件中，方便开�?

## 十三、C# 10

### 10.1 允许const内插字符�?
当用于占位符的所有表达式也是常量字符串时，可以使用字符串内插来初始化常量字符串�?换言之，每个 interpolationexpression 都必须是一个字符串，并且必须是编译时常量�?

### 10.2 记录类型可以密封ToString

### 10.3 同一解构中的赋值与宣告
C#10 之前
// Initialization:
(int x, int y) = point;
// assignment:
int x1 = 0;
int y1 = 0;
(x1, y1) = point;


C#10以后
int x = 0;
(x, int y) = point;


10.4 允许方法上的AsyncMethodBuilder属�?
在C#10中，除了为返回给定任务类类型的所有方法指定方法生成器类型之外，还可以为单个方法指定不同的异步方法生成器。这允许高级性能调优方案，在这种情况下，给定方法可能从自定义构建器中受益�?

## 十四、NET5.0

### 5.0.1 invoke
1. 委托后面�?.invoke
判断一下这个委托是不是为null，如果是就不执行委托，反之执行�?

2. Invoke 和BeginInvoke 的区�?

C#中有两种主要的Invoke/BeginInvoke:

**a. 委托(Delegate)上的Invoke/BeginInvoke:**
- 所有委托类型都具有这些方法
- 不特定于UI线程，可在任何上下文中使�?
- Invoke是同步调用委托的方法
- BeginInvoke是异步调用委托的方法，使用线程池
- 例如：`Action action = () => Console.WriteLine("Hello"); action.Invoke();`

**b. 控件(Control)上的Invoke/BeginInvoke:**
- 专门用于解决跨线程访问UI控件的问�?
- 用于确保代码在拥有控件的UI线程上执�?

Control.Invoke: 在拥有此控件基础窗口句柄的线程上同步执行指定的委�?
Control.BeginInvoke: 在创建控件的基础句柄所在的线程上异步执行指定的委托

以下内容主要针对Control.Invoke/BeginInvoke，常用于UI线程与工作线程之间的交互:

#### (1) Invoke - 同步调用:
   - 会阻塞调用线程，直到UI线程执行完委�?
   - 适用于需要立即获取结果的场景
   - 如果从UI线程调用，会直接执行，不会导致死�?

#### (2) BeginInvoke - 异步调用:
   - 不阻塞调用线程，立即返回
   - 委托会在UI线程的消息循环中排队等待执行
   - 适用�?发射后不�?的场景，不关心执行结�?

#### (3) 何时使用何种方法:
   - 使用Invoke: 当需要在继续执行前确保UI操作已完�?
   - 使用BeginInvoke: 当不需要等待UI操作完成，或避免潜在的死�?
   - 注意: 过度使用Invoke可能导致应用程序反应迟缓

#### (4) 参数详解:
   a. Invoke方法参数:
```csharp
// 常见形式
object Control.Invoke(Delegate method)
object Control.Invoke(Delegate method, params object[] args)
```
   - method: 要执行的委托(方法引用)
   - args: 传递给委托的参数数�?
      
   示例中的`(MethodInvoker) delegate { ... }`:
   - MethodInvoker�?NET内置委托类型，等同于`delegate void MethodInvoker()`
   - delegate { ... }是匿名方�?C# 2.0引入)，创建无参数无返回值的委托
   - 类型转换确保委托类型匹配Invoke要求

   b. BeginInvoke方法参数:
```csharp
// 常见形式
IAsyncResult Control.BeginInvoke(Delegate method)
IAsyncResult Control.BeginInvoke(Delegate method, params object[] args)
```
   - method: 要异步执行的委托
   - args: 传递给委托的参数数�?
   - 返回IAsyncResult: 可用于检查异步操作状态或等待完成

   c. 常用委托类型:
```csharp
// 无返回�?
this.Invoke(new Action(() => { label1.Text = "更新"; }));
      
// 有参数无返回�?
this.Invoke(new Action<string>(text => { label1.Text = text; }), "更新");
      
// 有返回�?
string result = (string)this.Invoke(new Func<string>(() => { 
    return textBox1.Text; 
}));
```

完整示例代码:

```csharp
// Invoke示例 - 从工作线程更新UI
private void BackgroundTask()
{
    // 耗时操作...
    string result = PerformLongOperation();
    
    // 需要更新UI，必须切换到UI线程
    this.Invoke((MethodInvoker) delegate {
        resultLabel.Text = result; // 安全地访问UI控件
    });
    
    // 或者使用带参数的方�?
    this.Invoke(new Action<string>(UpdateLabel), result);
}

private void UpdateLabel(string text)
{
    resultLabel.Text = text;
}

// BeginInvoke示例 - 非阻塞地更新UI
private void BackgroundTask()
{
    // 耗时操作...
    string result = PerformLongOperation();
    
    // 异步调度到UI线程，不阻塞当前线程继续执行
    this.BeginInvoke((MethodInvoker) delegate {
        resultLabel.Text = result;
    });
    
    // 可以立即继续工作，不等待UI更新完成
    ContinueProcessing();
}
```

## 委托详解

### 1. 委托的基本概�?

委托是C#中的一种引用类型，用于存储对具有特定参数列表和返回类型的方法的引用。委托可视为类型安全的函数指针，它们使得方法可以像参数一样被传递�?

委托的主要特点：
- 类型安全：编译时会检查委托类型和方法签名是否匹配
- 可序列化：支持远程调�?
- 多播特性：可以通过`+`和`-`运算符组合多个方�?
- 可封装实例方法或静态方�?
- 提供了回调机制的基础

### 2. 委托的声明和实例�?

#### 委托声明语法
```csharp
[访问修饰符] delegate [返回类型] [委托名称]([参数列表]);
```

#### 简单委托示�?
```csharp
// 声明委托类型
public delegate int CalculateDelegate(int x, int y);

// 实现符合委托签名的方�?
public int Add(int x, int y)
{
    return x + y;
}

public int Subtract(int x, int y)
{
    return x - y;
}

// 实例化委�?
CalculateDelegate calc = Add;  // �?new CalculateDelegate(Add);

// 调用委托
int result = calc(10, 5);  // 结果�?5
```

### 3. 委托多播（Multicast�?

委托可以引用多个方法，这称为多播委托。当调用多播委托时，所有引用的方法将按添加顺序被调用�?

```csharp
public delegate void NotifyDelegate(string message);

public void EmailNotify(string message)
{
    Console.WriteLine($"Email sent: {message}");
}

public void SMSNotify(string message)
{
    Console.WriteLine($"SMS sent: {message}");
}

// 创建多播委托
NotifyDelegate notifier = EmailNotify;
notifier += SMSNotify;  // 添加另一个方�?

// 调用多播委托
notifier("Hello");  // 两个方法都会被调�?

// 移除一个方�?
notifier -= EmailNotify;
```

多播委托的特殊情况：
- 对于有返回值的委托，只会返回最后一个被调用方法的返回�?
- 如果任何方法抛出未处理的异常，后续方法将不会被调�?

### 4. 匿名方法和Lambda表达�?

C# 2.0引入了匿名方法，C# 3.0引入了Lambda表达式，它们提供了更简洁的方式来实例化委托�?

#### 匿名方法
```csharp
CalculateDelegate calc = delegate(int x, int y) { return x + y; };
```

#### Lambda表达�?
```csharp
CalculateDelegate calc = (x, y) => x + y;
```

Lambda表达式的优势�?
- 更简洁的语法
- 可以捕获外部变量（闭包）
- 可以用于LINQ表达�?
- 可以被转换为表达式树

### 5. 预定义委托类�?

.NET框架提供了多种通用委托类型，减少了创建自定义委托的需要：

#### Action委托
表示无返回值的方法，可接受0�?6个参数：
```csharp
Action<string> log = message => Console.WriteLine(message);
log("Hello, World!");
```

#### Func委托
表示有返回值的方法，可接受0�?6个参数：
```csharp
Func<int, int, int> add = (x, y) => x + y;
int result = add(5, 3);  // 结果�?
```

#### Predicate委托
表示返回布尔值的方法，接受一个参数：
```csharp
Predicate<int> isEven = number => number % 2 == 0;
bool result = isEven(4);  // 结果为true
```

### 6. 委托的异步调�?

委托提供了`BeginInvoke`和`EndInvoke`方法用于异步调用。在.NET Framework中，这是异步编程的传统方式之一�?

```csharp
// 声明委托
delegate long FactorialDelegate(int number);

// 实现方法
long Factorial(int number)
{
    // 计算阶乘的代�?
    return result;
}

// 异步调用
FactorialDelegate factorialDelegate = Factorial;
IAsyncResult asyncResult = factorialDelegate.BeginInvoke(10, null, null);

// 做其他工�?..

// 获取结果
long result = factorialDelegate.EndInvoke(asyncResult);
```

>.NET Core�?NET 5+中，推荐使用Task-based异步模式(TAP)而非传统的委托异步模式�?

### 7. 委托与事�?

事件是基于委托构建的一种特殊成员，提供了发�?订阅模式的实现�?

事件与委托的区别�?
- 事件只能在声明它的类中触发（调用�?
- 外部类只能添加或移除事件处理程序，不能直接调用事�?
- 事件自动初始化为null，避免了空引用检查的必要

```csharp
// 声明委托类型
public delegate void PriceChangedEventHandler(decimal oldPrice, decimal newPrice);

public class Stock
{
    private decimal price;
    
    // 声明事件
    public event PriceChangedEventHandler PriceChanged;
    
    public decimal Price
    {
        get { return price; }
        set 
        { 
            if (price != value)
            {
                decimal oldPrice = price;
                price = value;
                // 触发事件
                PriceChanged?.Invoke(oldPrice, price);
            }
        }
    }
}

// 使用事件
Stock stock = new Stock();
stock.PriceChanged += (oldPrice, newPrice) => 
{
    Console.WriteLine($"Price changed from {oldPrice} to {newPrice}");
};
stock.Price = 30.10m;  // 触发事件
```

### 8. 委托的内部实�?

在底层，委托是派生自`System.MulticastDelegate`的密封类，它又派生自`System.Delegate`。编译器为每个委托声明生成一个对应的类�?

主要成员�?
- `System.Delegate.Target`：表示委托引用的方法所属的对象实例
- `System.Delegate.Method`：表示委托引用的方法信息
- `System.MulticastDelegate.GetInvocationList()`：获取多播委托中的所有委�?
- `Invoke()`：调用委托引用的方法

```csharp
public delegate void SimpleDelegate();

SimpleDelegate d = () => Console.WriteLine("Hello");

// 检查委托信�?
Type delegateType = d.GetType();                // 获取委托类型
MethodInfo methodInfo = d.Method;               // 获取方法信息
object target = d.Target;                       // 获取目标对象
Delegate[] delegates = d.GetInvocationList();   // 获取多播委托列表
```

### 9. 委托最佳实�?

- 尽可能使用内置委托类型（Action, Func, Predicate）而非自定义委�?
- 使用泛型委托提高重用�?
- 委托参数命名应反映其用途（例如：`onComplete`, `callback`�?
- 调用委托前检查null（使用`?.`运算符）
- 在多线程环境中小心使用多播委托，保存本地副本避免竞态条�?
- 避免在高性能场景中过度使用匿名方法和闭包，它们可能导致意外的内存分配

## 二、面向对象编程高级特�?

### 2.1 接口与继�?
#### 2.1.1 接口(Interfaces)
1. 接口定义了所有类继承接口时候应该遵循的语法规则，接口定义了语法规则是什么的部分，派生类定义了语法规则怎么做的部分
2. 接口声明和类类似，用interface关键字定义，接口默认是public权限
3. 如果一个接口继承了其他接口，那么实现类的时候，继承的其他接口也需要实�?

#### 2.1.2 默认接口方法
主要是因为菱形问题，还有c#不支持多重继承，同时避免菱形问题，才引入这个方法

C#8.0之前
```csharp
interface IExample
{
    void Ex1();                                      // 允许
    void Ex2() => Console.WriteLine("IExample.Ex2"); // 不允�?C# 8 以前)
}
```

C#8.0以后
```csharp
interface IExample
{
    void Ex1();                                      // 允许
    void Ex2() => Console.WriteLine("IExample.Ex2"); // 允许
}
```

### 2.2 分部类和分部方法
#### 2.2.1 分部类和方法(Partial Types)
主要作用是将类，结构，接口等类型分拆到多个不同的文件当中去，以便简化开发和维护

#### 2.2.2 分部方法(Partial methods)
1. 以下条件可以用于分部方法
声明必须上下文关键字partial开�?
分部类型各部分中的签名必须匹�?

2. 以下情况不需要分部方法即可实�?
没有任何可访问的修饰�?
返回void
没有任何输出参数
没有以下任何修饰符：virtual，override ，sealed，new 或extern

### 2.3 扩展方法
项目中有需要添加新功能，但是有不想或者不能破坏原来代码，在时候就可以用扩展方法来完成上述功能

### 2.4 索引�?
#### 2.4.1 索引器基础(Indexer)
1. 索引器允许一个对象像一个数组一样使用下标访�?
形式如下�?
```csharp
element-type this[int index] 
{
   // get 访问�?
   get 
   {
      // 返回 index 指定的�?
   }

   // set 访问�?
   set 
   {
      // 设置 index 指定的�?
   }
}
```

#### 2.4.2 索引器重�?
索引器可被重载，索引器声明的时候也可以带多个参数，且每个参数可以是不同的类型，没有必要让索引器必须是整形，C#允许是别的类型�?

### 2.5 协变和逆变
#### 2.5.1 基础概念
1. 协变
派生程度较大的类型分配或者赋值给派生程度小的，在泛型参数中使用out类型参数修饰�?

2. 逆变
派生类程度较小的分配或者赋值给派生程度较大的，在泛型参数中使用in类型参数修饰�?

#### 2.5.2 泛型类型的协变和逆变
1. 作用
提供更大的灵活�?

2. 协变
把子类付给父�?

3. 逆变
把父类付给子�?

#### 2.5.3 实际例子
##### 协变(Covariance)示例
协变允许使用比原始指定的类型派生程度更大的类型：

```csharp
// 协变的接口声�?- 注意out关键�?
interface IEnumerable<out T>
{
    IEnumerator<T> GetEnumerator();
}

// 协变在委托中的应�?
public delegate TResult Func<out TResult>();

// 协变使用示例
IEnumerable<string> strings = new List<string>();
IEnumerable<object> objects = strings; // 合法: string派生自object

// 函数协变
Func<string> stringFunc = () => "test";
Func<object> objectFunc = stringFunc; // 合法: 返回类型是协变的
```

##### 逆变(Contravariance)示例
逆变允许使用比原始指定的类型派生程度更小的类型：

```csharp
// 逆变的接口声�?- 注意in关键�?
interface IComparer<in T>
{
    int Compare(T x, T y);
}

// 逆变在委托中的应�?
public delegate void Action<in T>(T obj);

// 逆变使用示例
IComparer<object> objectComparer = new ObjectComparer();
IComparer<string> stringComparer = objectComparer; // 合法: string派生自object

// 逆变委托示例
Action<object> objectAction = (object obj) => Console.WriteLine(obj);
Action<string> stringAction = objectAction; // 合法: 参数类型是逆变�?
```

##### 实际应用中的意义
协变和逆变提高了泛型接口和委托的灵活性和重用性。比如，在LINQ中广泛使�?

```csharp
// 没有协变时，这样的代码是不合法的�?
IEnumerable<string> strings = new List<string>() { "one", "two", "three" };
IEnumerable<object> objects = strings;
foreach (object obj in objects)
{
    Console.WriteLine(obj); // 处理各种不同类型的序�?
}

// 使用逆变的实际例�?
void ProcessItems<T>(IEnumerable<T> items, Action<T> processor)
{
    foreach (T item in items)
    {
        processor(item);
    }
}

// 可以这样使用
IEnumerable<string> strings = new List<string>() { "one", "two", "three" };
Action<object> printObject = obj => Console.WriteLine(obj);
// 由于逆变，可以将接受object的Action传递给处理string的方�?
ProcessItems(strings, printObject);
```

### 2.6 Expression bodied成员
1. 语法
member => expression;

2. 例子
表达式主体定义：
```csharp
public override string ToString() => $"{fname} {lname}".Trim();
```

简化版�?
```csharp
public override string ToString()
{
   return $"{fname} {lname}".Trim();
}
```

### 2.7 已扩展的Expression-bodied成员
在C#中，Expression-bodied成员是一种更简洁的语法，用于定义只包含单个表达式的成员�?

#### 2.7.1 C# 6.0中的Expression-bodied成员
C# 6.0首先引入了Expression-bodied成员，但仅限于：
- 方法
- 只读属�?

语法�?`member => expression;`

例如�?
```csharp
// 方法
public string GetFullName() => $"{FirstName} {LastName}";

// 只读属�?
public string FullName => $"{FirstName} {LastName}";
```

#### 2.7.2 C# 7.0扩展的Expression-bodied成员
C# 7.0扩展了Expression-bodied成员的应用范围，增加了对以下成员的支持：
- 构造函�?
- 析构函数（终结器�?
- 属性访问器（get和set�?
- 索引器访问器

例如�?
```csharp
// 构造函�?
public Person(string name) => Name = name;

// 析构函数/终结�?
~Person() => Console.WriteLine("Finalizing Person");

// 属性访问器
private string _name;
public string Name 
{
    get => _name;
    set => _name = value ?? throw new ArgumentNullException(nameof(value));
}

// 索引�?
private string[] _items = new string[100];
public string this[int index]
{
    get => _items[index];
    set => _items[index] = value;
}
```

#### 2.7.3 Expression-bodied成员的优�?
1. **代码简洁�?*：减少了大括号和return语句，使代码更紧�?
2. **可读性提�?*：对于简单的单行实现，更容易理解
3. **功能性与常规实现相同**：它只是语法糖，不影响功能和性能
4. **适合函数式编程风�?*：鼓励使用表达式而不是语�?

#### 2.7.4 适用场景
Expression-bodied成员最适合于：
- 简单的计算或转�?
- 单行实现
- 委托到其他方法或属�?
- 条件返回值（使用条件运算符）

```csharp
// 条件逻辑
public bool IsAdult => Age >= 18;

// 简单计�?
public double GetArea() => Width * Height;

// 委托到其他方�?
public string FormatName() => FormatHelper.FormatPersonName(FirstName, LastName);

// 链式操作
public IEnumerable<string> GetFilteredNames() => Names.Where(n => n.Length > 5).Select(n => n.ToUpper());
```

### 2.9
// ... existing code ...
