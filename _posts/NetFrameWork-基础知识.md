---
title: NetFrameWork-基础知识
date: 2020-03-23 23:25:23
tags: 
- .NET FrameWork基础知识
categories: .NET
description: 
---

## 平台介绍

我们先介绍下.NetFrameWork

![](1.png)

最下层蓝色部分是.NET Framework的基础，也是所有应用软件的基础。.NET Framework不是凭空出来的，实际上API，COM+，和一些相关驱动依然是它的基石。.NET Framework只不过是对这些前辈们进行了系统的封装和扩充，在这个过程中，吸取了Java框架的很多经验。

黄色部分就是.Net给我们封装好的可以调用的API了.如可以做桌面的、WEB的、连接数据的等等.

下面我们一步步引入CLS、CTS、CLR的概念。

.NetFrameWork是基于通用语言基础架构(Common Language Infrastructure，CLI),它是由Microsoft开发的开放规范(技术标准)，由ISO和Ecma标准化，它描述了可执行代码和运行时环境，该环境允许多种高级语言在不同的计算机平台上使用，而不必为特定的体系结构重写。这意味着它是平台无关的。.NetFrameWork(未跨平台)、.NetCore、Mono等是CLI的实现。

CLI规范主要描述了以下三个方面:
1. Common Type System (CTS),所有遵循cts的编程语言共享的一组数据类型和操作。
2. Common Language Specification (CLS),一组基本规则，任何针对CLI的语言都应该遵循这些规则，以便与其他兼容cls的语言进行互操作。CLS规则定义了公共类型系统的一个子集。
3. Virtual Execution System (VES),加载并执行与clic兼容的程序，使用元数据在运行时合并单独生成的代码片段。

所有兼容的语言都编译成通用中间语言(CIL)，这是一种从平台硬件中抽象出来的中间语言。当执行代码时，特定于平台的VES将根据特定的硬件和操作系统将CIL编译成机器语言。

![](2.png)

CLR:微软的CLI的实现被称之为CLR;

CLR中包含的CTS、CLS、CIL、VES等都是为了实现CLI

## 数据类型

### 数值型

8位:8bit,1byte就是8bit.如:255转换位2进制就是``1111 1111``
- byte 无符号8位(指的转换为二进制的位数)整型,0-255
- sbyte 有符号8位整型 -128-127
- short 16位
- ushort 无符号16位
- int 32位
- uint 无符号32位
- ulong 无符号64位
- long 有符号64位

### 浮点型

- float 单精度
- double 双精度
- decimal 专用于货币




## 专题介绍

### Generic(泛型)

泛型（generic）是C#语言2.0和通用语言运行时（CLR）的一个新特性。泛型为.NET框架引入了类型参数（type parameters）的概念。类型参数使得设计类和方法时，不必确定一个或多个具体参数，具体参数可延迟到客户代码中声明、实现。这意味着使用泛型的类型参数T，写一个类``MyList<T>``，客户代码可以这样调用：``MyList<int>``， ``MyList<string>``或 ``MyList<MyClass>``。这避免了运行时类型转换或装箱操作的代价和风险。

**泛型的好处**:
1. 复用性:如,干同一件事的方法,因为类型不同可以用泛型进行封装.
2. 类型安全:如,通过泛型申明的方法,类型不匹配,编译器就会报错.
3. 高效率:泛型方法和普通方法效率基本一致.不存在装箱和拆箱的操作.

**泛型的原理**:泛型不是一个简单的语法糖，是框架升级支持的.编译器在编译代码的时候会用占位符**`**表达类型参数
`·1`或`·2`表示有几个类型参数,运行的时候,类型是确定的.然后再把占位符替换掉.


1. 泛型方法
为了一个方法满足不同的类型的需求,一个方法完成多实体的查询,一个方法完成不同的类型的数据展示.
```c#
int iValue = 123;
string sValue = "456";
DateTime dtValue = DateTime.Now;
object oValue = "678";

Console.WriteLine("***********************Common***********************");
CommonMethod.ShowInt(iValue);
CommonMethod.ShowString(sValue);
CommonMethod.ShowDateTime(dtValue);

Console.WriteLine("***********************Object***********************");
CommonMethod.ShowObject(oValue);
CommonMethod.ShowObject(iValue);
CommonMethod.ShowObject(sValue);
CommonMethod.ShowObject(dtValue);

Console.WriteLine("***********************Generic***********************");
CommonMethod.Show<int>(iValue);
CommonMethod.Show<string>(sValue);
CommonMethod.Show<DateTime>(dtValue);
CommonMethod.Show<object>(oValue);

//泛型方法的声明
public static void Show<T>(T tParameter)
{
    Console.WriteLine("This is {0},parameter={1},type={2}",
        typeof(CommonMethod), tParameter.GetType().Name, tParameter);
}
```
2. 泛型类
一个类，满足不同类型的需求
```c#
public class GenericClass<T>
{

}
```
3. 泛型接口

一个接口，满足不同类型的需求

```c#
public interface GenericInterface<S>
{

}
```
4. 泛型委托

一个委托，满足不同类型的需求
```c#
public delegate void Do<T>();
```

5. 泛型约束
一个约束类型是一种基类约束，它通知编译器，只有这个类型的对象或从这个类型派生的对象，可被用作类型参数
```c#
public class GenericClass<T> where T : ISports
{

}

public T GetT<T, S>()
    //where T : class//引用类型约束
    //where T : struct//值类型
    where T : new()//无参数构造函数
    where S : class
{
    //return null;
    //return default(T);//default是个关键字，会根据T的类型去获得一个默认值
    return new T();
}
```

6. 协变、逆变
所谓协变逆变，都是跟泛型相关，只能放在接口或者委托的泛型参数前面,out 协变covariant,修饰返回值;in 逆变contravariant 修饰传入参数 

协变：就是让右边可以用子类，让泛型用起来更方便

逆变:就是让右边可以用父类，让泛型用起来更方便

```c#
IMyList<Sparrow, Bird> myList1 = new MyList<Sparrow, Bird>();
IMyList<Sparrow, Bird> myList2 = new MyList<Sparrow, Sparrow>();//协变
IMyList<Sparrow, Bird> myList3 = new MyList<Bird, Bird>();//逆变
IMyList<Sparrow, Bird> myList4 = new MyList<Bird, Sparrow>();//协变+逆变


public interface IMyList<in inT, out outT>
{
    void Show(inT t);
    outT Get();
    outT Do(inT t);

    ////out 只能是返回值   in只能是参数
    //void Show1(outT t);
    //inT Get1();

}


public class MyList<T1, T2> : IMyList<T1, T2>
{

    public void Show(T1 t)
    {
        Console.WriteLine(t.GetType().Name);
    }

    public T2 Get()
    {
        Console.WriteLine(typeof(T2).Name);
        return default(T2);
    }

    public T2 Do(T1 t)
    {
        Console.WriteLine(t.GetType().Name);
        Console.WriteLine(typeof(T2).Name);
        return default(T2);
    }
}


```
7. 泛型缓存

```c#
/// <summary>
/// 每个不同的T，都会生成一份不同的副本
/// 适合不同类型，需要缓存一份数据的场景，效率高
/// </summary>
/// <typeparam name="T"></typeparam>
public class GenericCache<T>
{
    static GenericCache()
    {
        Console.WriteLine("This is GenericCache 静态构造函数");
        _TypeTime = string.Format("{0}_{1}", typeof(T).FullName, DateTime.Now.ToString("yyyyMMddHHmmss.fff"));
    }

    private static string _TypeTime = "";

    public static string GetCache()
    {
        return _TypeTime;
    }
    //common<int>(1)
}
```



### Reflection(反射)

![](3.png)
反射Reflection:System.Reflection，是.Net Framework提供的一个帮助类库，可以读取并使用metadata

1. 反射加载dll
```c#
Assembly assembly = Assembly.Load("Ruanmou.DB.MySql");
//1 动态加载 一个完整dll名称不需要后缀  从exe所在的路径进行查找
Assembly assembly1 = Assembly.LoadFile(@"D:\ruanmou\online12\20181212Advanced12Course2Reflection\MyReflection\MyReflection\bin\Debug\Ruanmou.DB.MySql.dll");//完整路径
Assembly assembly2 = Assembly.LoadFrom("Ruanmou.DB.MySql.dll");//当前路径
Assembly assembly3 = Assembly.LoadFrom(@"D:\ruanmou\online12\20181212Advanced12Course2Reflection\MyReflection\MyReflection\bin\Debug\Ruanmou.DB.MySql.dll");//当前路径

foreach (var type in assembly.GetTypes())
{
    //type.IsGenericType
    Console.WriteLine(type.Name);
    foreach (var method in type.GetMethods())
    {
        Console.WriteLine(method.Name);
    }
}

```
2. 反射创建对象
```c#
Assembly assembly = Assembly.Load("Ruanmou.DB.MySql");//1 动态加载
Type type = assembly.GetType("Ruanmou.DB.MySql.MySqlHelper");//2 获取类型 完整类型名称
dynamic dDBHelper= Activator.CreateInstance(type);
dDBHelper.Query();//dynamic编译器不检查，，运行时才检查       
```

3. 调用构造函数

```c#
Assembly assembly = Assembly.Load("Ruanmou.DB.SqlServer");
Type type = assembly.GetType("Ruanmou.DB.SqlServer.ReflectionTest");
foreach (ConstructorInfo ctor in type.GetConstructors())
{
    Console.WriteLine(ctor.Name);
    foreach (var parameter in ctor.GetParameters())
    {
        Console.WriteLine(parameter.ParameterType);
    }
}
object oTest1 = Activator.CreateInstance(type);
object oTest2 = Activator.CreateInstance(type, new object[] { 123 });
object oTest3 = Activator.CreateInstance(type, new object[] { "陌殇" });
```
4. 破坏单例

```c#
//反射破坏单例---就是发射调用私有构造函数
Assembly assembly = Assembly.Load("Ruanmou.DB.SqlServer");
Type type = assembly.GetType("Ruanmou.DB.SqlServer.Singleton");
Singleton singletonA = (Singleton)Activator.CreateInstance(type, true);
Singleton singletonB = (Singleton)Activator.CreateInstance(type, true);
Singleton singletonC = (Singleton)Activator.CreateInstance(type, true);
Singleton singletonD = (Singleton)Activator.CreateInstance(type, true);
Console.WriteLine($"{object.ReferenceEquals(singletonA, singletonD)}");
```

5. 反射创建泛型类
```c#
Assembly assembly = Assembly.Load("Ruanmou.DB.SqlServer");
Type type = assembly.GetType("Ruanmou.DB.SqlServer.GenericClass`3");
//GenericClass<string, int, DateTime> genericClass = new GenericClass<string, int, DateTime>();
//object oGeneric = Activator.CreateInstance(type);
Type typeMake = type.MakeGenericType(new Type[] { typeof(string), typeof(int), typeof(DateTime) });
object oGeneric = Activator.CreateInstance(typeMake);
```

6. 反射调用方法
```c#
Console.WriteLine("&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&");
Assembly assembly = Assembly.Load("Ruanmou.DB.SqlServer");
Type type = assembly.GetType("Ruanmou.DB.SqlServer.ReflectionTest");
object oTest = Activator.CreateInstance(type);
{
    MethodInfo method = type.GetMethod("Show1");
    //if()
    method.Invoke(oTest, null);
}
```

7. 反射调用私有方法
```c#
{
    //调用私有方法
    Console.WriteLine("&&&&&&&&&&&&&&&&&&&&私有方法&&&&&&&&&&&&&&&&&&&");
    Assembly assembly = Assembly.Load("Ruanmou.DB.SqlServer");
    Type type = assembly.GetType("Ruanmou.DB.SqlServer.ReflectionTest");
    object oTest = Activator.CreateInstance(type);
    var method = type.GetMethod("Show4", BindingFlags.Instance | BindingFlags.NonPublic);
    method.Invoke(oTest, new object[] { "我是老王" });
}
```

8. 反射调用泛型方法

```c#
{
    Console.WriteLine("********************GenericMethod********************");
    Assembly assembly = Assembly.Load("Ruanmou.DB.SqlServer");
    Type type = assembly.GetType("Ruanmou.DB.SqlServer.GenericMethod");
    object oGeneric = Activator.CreateInstance(type);
    //foreach (var item in type.GetMethods())
    //{
    //    Console.WriteLine(item.Name);
    //}
    MethodInfo method = type.GetMethod("Show");
    var methodNew = method.MakeGenericMethod(new Type[] { typeof(int), typeof(string), typeof(DateTime) });
    object oReturn = methodNew.Invoke(oGeneric, new object[] { 123, "董小姐", DateTime.Now });
}
```

9. 反射获取(设置)字段和属性

sql的动态生成案例

```c#
Type type = typeof(People);
object oPeople = Activator.CreateInstance(type);
foreach (var prop in type.GetProperties())
{
    Console.WriteLine($"{type.Name}.{prop.Name}={prop.GetValue(oPeople)}");
    if (prop.Name.Equals("Id"))
    {
        prop.SetValue(oPeople, 234);
    }
    else if (prop.Name.Equals("Name"))
    {
        prop.SetValue(oPeople, "饿了么");
    }
    Console.WriteLine($"{type.Name}.{prop.Name}={prop.GetValue(oPeople)}");
}
foreach (var field in type.GetFields())
{
    Console.WriteLine($"{type.Name}.{field.Name}={field.GetValue(oPeople)}");
    if (field.Name.Equals("Description"))
    {
        field.SetValue(oPeople, "并不是外卖，也不是真的饿了");
    }
    Console.WriteLine($"{type.Name}.{field.Name}={field.GetValue(oPeople)}");
}
```

10. 性能测试

启动加载好,后面运行就很快了,不要在循环中去反射,最好初始化反射好.



11.  反射的优点
动态  
1.  反射的缺点
   1. 使用麻烦
   2. 避开编译器检查
   3. 性能问题！！！(启动加载好,后面运行就很快了)


### 面向对象编程

1. 继承
可以通过接口、类、抽象类的方式实现继承.
 1. 抽象方法只可以在抽象类中.
 2. 基类中可以有普通方法、抽象方法、虚方法.
 3. 普通方法由编译时决定，虚方法和抽象方法由运行时决定.
 4. 实例化子类时候,会先调用父类的构造函数,然后在调用子类的构造函数
 5. sealed类不可以被继承,sealed抽象方法,后续无法实现.
 6. 私有成员无法继承

1. 多态

通过继承，一个类可以用作多种类型：可以用作它自己的类型、任何基类型，或者在实现接口时用作任何接口类型。这称为多态性。C# 中的每种类型都是多态的。类型可用作它们自己的类型或用作 Object 实例，因为任何类型都自动将 Object 当作基类型。

3. 接口和抽象类
   1. 接口是包含一组虚方法的抽象类型，其中每一种方法都有其名称、参数和返回值。接口方法不能包含任何实现.
   2. 抽象类提供多个派生类共享基类的公共定义，它既可以提供抽象方法，也可以提供非抽象方法。抽象类不能实例化，必须通过继承由派生类实现其抽象方法，因此对抽象类不能使用new关键字，也不能被密封。
   3. 抽象类的出发点应该是代码重用，是为了当父类   is  a
   4. 接口纯粹为了约束，告诉别人一定有什么功能    can  do
   5. 接口放的是不确定的东西，确定的不可以放，比如字段.

### 