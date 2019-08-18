# Java Learning Notes

> Book: 疯狂Java讲义第四版

# 1. Java 基础

## 1.1 流程控制

### 1.1.1. Switch

> 使用 switch 语句时，有两个值得注意 的地方 :第 一个地方是 switch 语句后的 expression 表达式的 数据类型只 能是 byte 、 short、 char、 int 四种整数类型 ， String (Java 7 才 支持 ) 和枚举类型;第 二个地方是如果省咯 了 case 后代码块的 break; 将引入一个陷阱。

## 1.2 控制循环结构

### 1.2.1 break

> break 语句不仅可以结束其所在的循环，还可以直接结束其外层循环。此时需要在 break 后紧跟一个标签，这个标签用于标识一个外层循环 。

```java
public class BreakTest2
{
	public static void main(String[] args)
	{
		// 外层循环，outer作为标识符
		outer:
		for (int i = 0 ; i < 5 ; i++ )
		{
			// 内层循环
			for (int j = 0; j < 3 ; j++ )
			{
				System.out.println("i的值为:" + i + "  j的值为:" + j);
				if (j == 1)
				{
					// 跳出outer标签所标识的循环。
					break outer;
				}
			}
		}
	}
}
```

### 1.2.2 continue

> 与 break 类似的是，continue 后也可以紧跟一个标签，用 于直接跳过标签所标识循环的当次循环的剩下语句，重新开始下 一次循环 。

```java
public class ContinueTest2
{
	public static void main(String[] args)
	{
		// 外层循环
		outer:
		for (int i = 0 ; i < 5 ; i++ )
		{
			// 内层循环
			for (int j = 0; j < 3 ; j++ )
			{
				System.out.println("i的值为:" + i + "  j的值为:" + j);
				if (j == 1)
				{
					// 忽略outer标签所指定的循环中本次循环所剩下语句。
					continue outer;
				}
			}
		}
	}
}
```

## 1.3 Arrays

### 1.3.1 几个常用的static方法

> int binarySearch(type口 a， type key): 使用 二分法查询 key 元素值在 a 数组中出现的索引 ;如果 a 数组不包含 key 元素值 ，则返回负数 。 调用该方法时要求数组中元素己经按升序排列 ， 这样才能得到正确结果 。
>
> int binarySearch(type[] a , int fromIndex， int tolndex , type key) : 这个方法与前一个方法类似，但它只搜索 a 数组中fromIndex 到 tolndex 索引 的元素。调用该方法时要求数组中元素己经按升序排列，这样才能得到正确结果 。
>
> type[] copyOf(type[] original, int length): 这个方法将会把 original 数组复制成一个新数组， 其中length 是新数组的长度。如果 length 小于 original 数组的长度 ，则新数组就是原数组的前面 length 个元素;如果 length 大于 original 数组的长度，则新数组的前面元素就是原数组的所有元素，后面补充 o(数值类型)、false(布尔类型)或者 null ( 引用类型) 。
>
> type[] copyOfRange(type[] original , int from , int to): 这个方法与前面方法相似，但这个方法只复制 original 数组的 from 索引到 to 索引的元素 。 
>
> boolean equals(type[] a， type[] a2): 如果 a 数组和 a2 数组的长度相等，而且 a 数组和 a2 数组的数组元素也一一相同，该方法将返回 true。 
>
> void fill(type[] a，type val): 该方法将会把 a 数组的所有元素都赋值为 val 。 
>
> void fill(type[] a, int fromIndex， int tolndex , type val): 该方法与前一个方法的作用相同，区别只是该方法仅仅将 a 数组的 fromlndex 到 tolndex 索引的数组元素赋值为 val。
>
> void sort(type[] a): 该方法对 a 数组的数组元素进行排序。
>
> void sort(type[] a , int 仕omIndex， int toIndex): 该方法与前一个方法相似 ，区别是该方法仅仅对 fromlndex 到 toIndex 索引的元素进行排序。 
>
> String toString(type[] a): 该方法将一个数组转换成一个字符串。该方法按顺序把多个数组元素连缀在一起，多个数组元素使用英文逗号(，)和空格隔开。

### 1.3.2 并行方法

> Java 8 增强了 Arrays 类的功能，为 Arrays 类增加了 一些工具方法，这些工具方法可以充分利用多 CPU 并行的能力来提高设值、排序的性能 。

> void parallelPrefix(xxx[] array, XxxBinaryOperator op): 该方法使用 op 参数指定的计算公式计算 得到的结果作为新的元素 。 op 计算公式包括 left、right 两个形参，其中 le位代表数组中前一个 索引处的元素， right 代表数组中当前索引处的元素，当计算第一个新数组元素时， left的值默认为 l 。 
>
> void paralle lP refix(xxx[] array， int fromlndex， int tolndex , XxxBinaryOperator op): 该方法与上一个方法相似，区别是该方法仅重新计算 fromlndex 到 toIndex 索引的元素 。 
>
> void setAll(xxx[] array, Int ToXxxFunction generator): 该方法使用指定的生成器 (generator) 为所有数组元素设置值，该生成器控制数组元素的值的生成算法 。 
>
> void parallelSetAll(xxx[] array, In tToXxxFunction generator): 该方法的功能与上一个方法相同，只是该方法增加了并行能力，可以利用多 CPU 并行来提高性能 。
>
> void parallelSort(xxx[] a): 该方法的功能与 Arrays 类以前就有的 sortO方法相似，只是该方法增 加了并行能力，可以利用多 CPU 并行来提高性能 。 
>
> void parallelSort(xxx[] a , int 仕omlndex， int toIndex): 该方法与上一个方法相似，区别是该方法仅对台omIndex 到 toIndex 索引的元素进行排序 。 
>
> Spliterator.OfXxxspliterator(xxx[] array): 将该数组的所有元素转换成对应的 Spliterator 对象 。 
>
> Spliterator.OfXxxspliterator(xxx[] arr陈 int startInc1usive , int endExc1usive): 该方法与上一个方法相似，区别是该方法仅转换 startlnc1usive 到 endExc1usive 索引的元素 。 
>
> XxxStream stream(xxx[] aπay): 该方法将数组转换为 Stream ， Stream 是 Java 8 新增的流式编程的 API 。
>
> XxxStream stream(xxx[] arra讥 int startln c1usive , int endExc1usive): 该方法与上一个方法相似，区别是该方法仅将 fromIndex 到 toIndex 索引的元素转换为 Stream。
>

```java
public class ArraysTest2
{
	public static void main(String[] args)
	{
		int[] arr1 = new int[]{3, -4 , 25, 16, 30, 18};
		// 对数组arr1进行并发排序
		Arrays.parallelSort(arr1);
		System.out.println(Arrays.toString(arr1));
		int[] arr2 = new int[]{3, -4 , 25, 16, 30, 18};
		Arrays.parallelPrefix(arr2, new IntBinaryOperator()
		{
			// left代表数组中前一个所索引处的元素，计算第一个元素时，left为1
			// right代表数组中当前索引处的元素
			public int applyAsInt(int left, int right)
			{
				return left * right;
			}
		});
		System.out.println(Arrays.toString(arr2));
		int[] arr3 = new int[5];
		Arrays.parallelSetAll(arr3 , new IntUnaryOperator()
		{
			// operand代表正在计算的元素索引
			public int applyAsInt(int operand)
			{
				return operand * 5;
			}
		});
		System.out.println(Arrays.toString(arr3));
	}
}
```

## 1.4 面向对象（上）

### 1.4.1 类

> Java 语言里定义类的简单语法如下:

```java
[修饰符 1] class 类名

{

零个到多个构造器定义. . . 

零个到多个成员变量.. . 

零个到多个方法. . .

}
```

> 其中，修饰符可以是 public、 final、 abstract ，或者完全省略这三个修饰符。
>
> 对一个类定义而言，可以包含三种最常见的成员 :构造器、成员变量和方法， 三种成员都可以定义 零个或多个。
>
> 类里各成员之间的定义顺序没有任何影响，各成员之间可以相互调用，但需要指出的是， static 修饰的成员不能访问没有 static 修饰的成员 。
>
> 成员变量用于定义该类或该类的实例所包含的状态数据，方法则用于定义该类或该类的实例的行为 特征或者功能实现。构造器用于构造该类的实例， Java 语言通过 new 关键字来调用构造器，从而返回 该类的实例。
>
> 构造器是一个类创建对象的根本途径，如果一个类没有构造器，这个类通常无法创建实例。因此， Java 语 言提供了一个功能 : 如果程序员没有为一个类编写构造器，则系统会为该类提供一个默认的构造器。一旦程序员为一个类提供了构造器，系统将不再为该类提供构造器 。
>

### 1.4.2 成员变量

> 定义成员变量的语法格式如下:
>

```java
[修饰符] 类型 成员变量名 [=默认值] ;
```

> 对定义成员变量语法格式的详细说明如下 ：
>
> 修饰符:修饰符可以省略，也可以是 public、 protected、 private 、 static 、自nal，其中 public 、 protected 、private 三个最多只能出现其中之一 ， 可以与 static 、 final 组合起来修饰成员变量 。 
>
> 类型 : 类型可以是 Java 语言 允许的任何数据类型，包括基本类型和现在介绍的引用类型 。 
>
> 成员变量名:成员变量名只要是一个合法的标识符即可，但这只是从语法角度来说的;如果从程序可读性角度来看，成员变量名应该由 一个或多个有意义的单词连缀而成，第 一个单词首字母小写，后面每个单词首字母大写 ， 其他字母全部小 写 ，单词与单词之间不要使用任何分隔符 。
>
> 成员变量用于描述类或对象包含的状态数据，因此成员变量名建议使用英文名词 。 
>
> 默认值:定义成员变量还可以指定 一个可边的默认值 。

### 1.4.3 方法

#### 1.4.3.1 定义方法

```java
[修饰符] 方法返回值类型 方法名(形参列表) {
  由零条到多条可执行性语句组成的方法体
}
```

> 对定义方法语法格式的详细说明如下：
>
> 修饰符:修饰符可以省略，也可以是 public、 protected、 private、 static、 final、 abstract，其中 public 、protected、 private 三个最多只能出现其中之一 ; 以 与 static 组合起来修饰方法 。final 和 abstract 最多只能出现其中之一 ，它们可以 与 static 组合起来修饰方法 。
>
> 方法返回值类型:返回值类型可以是 Java 语 言 允许的任何数据类型，包括基本类型和引用类型；如果声明了方法返回值类型，则方法体内必须有一个有效的 return 语句，该i吾句返回 一个变量 或一个表达式，这个变量或者表达式的类型必 须与此处声 明的类型匹配 。 除此之外 ， 如果一个 方法没有返回值 ，则必须使用 void 来声明没有返回值 。 
>
> 方法名:方法名的命名规则与成员变量 的命名规则基本相同，但由于方法用于描述该类或该类 的实例的行为特征或功能实现，因此通常建议方法名以英文动词开头 。 
>
> 形参列表:形参列表用于定义该方法可以接受的参数，形参列表由 零组到多组"参数类型形参 名"组合而成 ， 多组参数之间以英文逗号 （，）隔开，形参类型和形参名之间以英文空格隔开 。 一旦在定义方法时指定了形参列表，则调用该方法时必须传入对应的参数值一 谁调用方法， 谁负责为形参赋值 。

#### 1.4.3.2 方法的重载

> 方法重载 的要求就是两同一不同 :**同 一个类中方法名相同，参数列表不同**。至于方法的其他部分， 如方法返回值类型、修饰符等，与方法重载没有任何关系 。

#### 1.4.3.3 参数可变的方法

> 从 JDK 1.5 之后， Java 允许定义形参个数可变的参数，从而允许为方法指定数量不确定 的形参。如 果在定义方法时， 在最后 一个形参的类型后增加三 点( .. . ) ，则表明该形参可 以接受多个参数值，多 个 参数值被当成数组传入 。

> 形参个数可变的参数本质就是一个数组参数，也就是说，下面两个方法签名的效果 完全一样 。
>
> // 以可变个数形参来定义方法
>
> public static void test(int a, String… books ) ;
>
> // 下面采用数组形参来定义方法
>
> public static void test(int a, String[] books);
>
> **数组形式的形参可以处于形参列表的任意位置，但个数可变的形参只能处于形 参列表的最后。 也就是说， 一个方法中最多只能有一个个数可变的形参 。**

### 1.4.4 构造器

#### 1.4.4.1 构造器定义

```java
[修饰符] 构造器名 (形参列表) {
  由零条到多条可执行性语句组成的构造器执行体
} 
```

> 对定义构造器语法格式的详细说明如下 :
>
> 修饰符 : 修饰符可以省略，也可以是 public 、protected、private 其中之一；
>
> 构造器名:构造器名必须和类名相同 。
>
> 形参列表 :和定义方法形参列表的 格式完全相同 。

> 值得指出的是，**构造器既不能定义返回值类型 ，也不能使用 void 声明构造器没有返回值。**如果为 构造器定义了返回值类型，或使用 void 声明构造器没有返回值，**编译时不会出错**，但 Java 会把这个所谓的构造器**当成方法**来处理一一它就不再是构造器 。

#### 1.4.4.2 构造器重载

> 同 一个类里具有多个构造器 ， 多个构造器的形参列表不同 ，即被称为构造器重载。

### 1.4.5 this 关键字

> Java 提供了 一个 this 关键字 ， **this 关键字总是指向调用该方法的对象**。 根据 this 出现位置的不同 ，this 作为对象的默认引用有两种情形：
>
> 1. 构造器中引用该构造器正在初始化的对象 。this 引用也可以用于构造器中作为默认引用，由于构造器是直接使用 new 关键宇来调用， 而不是使用对象来调用的，所以 this 在构造器中代表该构造器正在初始化的对象。
>
> 2. 在方法中引用调用该方法的对象 。

> **Static 方法中不允许使用this。**

### 1.4.6 成员变量与局部变量

![Java-Learning-Notes-Picture-1](/Users/lotus/Notes/Java-Learning-Notes/Java-Learning-Notes-Picture-1.png)

### 1.4.7 封装 Encapsulation

> 3 个访问控制符 : private、 protected 和 public ，分别代表了 3 个访问控制级别，另外还 有一个不加任何访问控制符的访问控制级别，提供了 4 个访问控制级别 。
>
> 访问控制级别由小到大：private -> default -> protected -> public.

|            | private | default | protected | public |
| ---------- | :-----: | :-----: | :-------: | :----: |
| 同一个类中 |  mark   |  mark   |   mark    |  mark  |
| 同一个包中 |         |  mark   |   mark    |  mark  |
| 子类中     |         |         |   mark    |  mark  |
| 全局范围   |         |         |           |  mark  |

#### 1.4.7.1 使用原则

> 关于访问控制符的使用，存在如下几条基本原则:
>
> 1. 类里的绝大部分成员变量都应该使用 private 修饰，只有一些 static 修饰的、类似全局变量 的成 员变量，才可能考虑使用 public 修饰 。 除此之外，有些方法只用于辅助实现该类的其他方法，这些方法被称为工具方法 ，工具方法也应该使用 private 修饰 。
> 2. 如果某个类主要用做其他类的父类，该类里包含的大部分方法可能仅希望被其子类重写，而不 想被外界直接调用，则应该使用 protected 修饰这些方法 。
> 3. 希望暴露出来给其他类自由调用的方法应该使用 public 修饰 。 因此，类的构造器通过使用 public 修饰，从而允许在其他地方创建该类的实例 。 因为外部类通常都希望被其他类自由使用，所以 大部分外部类都使用 public 修饰 。

#### 1.4.7.2 package 、import 和 import static

> Java 允许将一组功能相关的类放在同一个 package 下，从而组成逻辑上的类库单元 。 如果希望把一 个类放在指定的包结构下，应该在 Java 源程序的第 一个非注释行放置如下格式的代码:
>
> package packageName;

> import static 导入的粒度是成员变量或方法。
>
> JDK 1. 5 以后更是增加了 一种静态导入的语法 ， 它用于导入指定类的某个静态成员变量、方法或全部的静态成员变量 、方法 。
>
> 静态导入使用 import static 语句 ， 静态导入也有两种语法，分别用于导入指定类的单个静态成员变量、方法和全部静态成员变量 、方法，其中导入指定类的单个静态成员变量 、方法的语法格式如下:
>
> import static package . subpackage.. .ClassName.fieldNamelmethodName;
>
> 星号只能代表静态成 员变量或方法名 。

> Java 的核心类都放在 Java 包以及其子包下， Java 扩展的许多类都放在 Javax 包以及其子包下 。
>
> 1. java.lang: 这个包下包含了 Java 语 言 的核心类，如 String、 Math、 System 和 Thread 类等，使用 这个包下的类无须使用 lmport 语句导入，系统会自动导入这个包下的所有类 。 
> 2. java.util: 这个包下包含了 Java 的大量工具知接口和集合框架势接口，例如Arrays 和 List、 Set 等 。 
> 3. java.net: 这个包下包含了一些 Java 网络编程相关的类/接口 。 
> 4. java.io: 这个包下包含了 一些 Java 输入/输出编程相关的类/接口 。 
> 5. java.text: 这个包下包含了 一些 Java 格式化相关的类 。 
> 6. java.sql: 这个包下包含了 Java 进行 JDBC 数据库编程的相关类/接口 。

### 1.4.8 类的继承

#### 1.4.8.1 类继承的定义

> Java 的继承通过 extends 关键字来实现.

```java
修饰符 class SubClass extends SuperClass {
 //类定义部分 
}
```

#### 1.4.8.2 重写父类的方法

> 子类包含与父类同名方法的现象被称为方法重写( Override ) ，也被称为方法覆盖。可 以说子类重写了父类的方法， 也可以说子类覆盖了父类的方法 。
>
> **方法的重写要遵循 " 两同两 小一大"规则**。
>
> "两同"即方法名相同 、 形参列表相同 ;
>
> "两小"指的 是子类方法返回值类型应比父类方法返回值类型更小或相等 ， 子类方法声明抛出的异常类应 比父类方法声 明抛出的异常类更小或相等;
>
> "一大"指的是子类方法的访 问 权限应比父类方法的访 问 权限更大或相等。 
>
> 尤其需要指出的是，覆盖方法和被覆盖方法要么都是类方法，要么都是实例方法，不能一个是类方法， 一个是实例方法 。

#### 1.4.8.3 super

> super 是 Java 提供的 一个关键字， super 用于限定该对象调用它从父类继承得到的实例变量或方法，包括构造器 。
>
> 正如 this 不能出现在 statlc 修饰的方法中 一样， **super 也不能出现在 static 修饰的方法中**。 static 修饰的方 法是属于类的，该方法的调用者可能是一个类，而不是对象，因而 super 限定也就失去了意义 。

> 如果在构造器中使用 super ，则 super 用于限定该构造器初始化的是该对象从父类继承得到的实例变量，而不是该类自己定义的实例变量 。
>
> **如果子类定义了和父类同名的实例变量**，则会发生子类实例变量隐藏父类实例变量 的情形 。 在正常情况下，子类里定义的方法直接访问该实例变量默认会访问到子类中定义的实例变量，无法访问到父类 中被隐藏的实例变量。

#### 1.4.8.4 变量的查找顺序

> 如果在某个方法中访问名为 a 的成员变量 ，但没有显式指定调用者， 则系统查找 a 的顺序为:
>
> 1. 查找该方法中是否有名为 a 的局部变量。
> 2. 查找当前类中是否包含名为 a 的成员变量。
> 3. 查找 a 的直接父类中是否包含名为 a 的成员变量，依次上溯 a 的所有父类，直到 java.lang.Object 类，如果最终不能找到名为 a 的成员变量，则系统出现编译错误 。

#### 1.4.8.5 super 调用父类构造器

> **不管是否使用 super 调用来执行父类构造器的初始化代码， 子类构造器总会调用父类构造器一次。** 
>
> 子类构造器调用父类构造器分如下几种情况：
>
> 1. 子类构造器执行体的第 一行使用 super 显式调用父类构造器，系统将根据 super 调用里传入的实 参列表调用父类对应的构造器 。 
> 2. 子类构造器执行体的第一行代码使用 this 显式调用本类中重载的构造器 ， 系统将根据 this 调用里 传入的实参列表调用本类中的另 一个构造器 。 执行本类中另 一个构造器时即会调用父类构造器 。 
> 3. 子类构造器执行体中既没有 super 调用，也没有 this 调用，系统将会在执行子类构造器之前，隐 式调用父类无参数的构造器。
>
> 不管上面哪种情况，当调用子类构造器来初始化子类对象时，**父类构造器总会在子类构造器之前执行**;不仅如此，执行父类构造器时，系统会再次上溯执行其父类构造器 …… 依此类推，创建任何 Java 对象 ， **最先执行的总是 java.lang.Object 类的构造器**。

### 1.4.9 多态 Polymorphism

#### 1.4.9.2 什么事多态

> Java 引用变量有两个类型 : 一个是编译时类型， 一个是运行时类型 。 编译时类型由声明该变量时使 用的类型决定，运行时类型由实际赋给该变量的对象决定 。 如果**编译时类型和运行时类型不一致**，就可能出现所谓的多态(Polymorphism) 。
>

> 当把一个子类对象直接赋给父类引用变量时，例如 BaseClass ploymophicBc = new SubClassO; 这个 ploymophicBc 引用变量的编译时类型是 BaseClass ，而运行时类型是 SubClass ， 当运行时调 用该引 用变量 的方法时，**其方法行为总是表现出子类方法的行为特征**，而不是父类方法的行为特征 ，这就可能出现:相同类型的变量 、 调用同一个方法时呈现出多种不同的行为特征，这就是多态 。
>

#### 1.4.9.2 instanceof 运算符

> instanceof 运算符的前一个操作数通常是一个引用类型变量 ，后一个操作数通常是一个类(也可以是接口，可以把接口理解成一种特殊的类) ，它用于判断前面的对象是否是后面的类，或者其子类、实 现类的实例 。如果是 ，则返回 true ，否则返回 false 。
>
> 在使用 instanceof 运算符时需要注意 : instanceof 运算符前面操作数的编译时类型要么与后面的类相同，要么与后面的类具有父子继承关系，否则会引起编译错误 。

### 1.4.10 继承与组合

> 继承要表达的是一种"是 ( is-a) "的关系，而组合表达的是"有 ( has-a ) "的关系 。

### 1.4.11 初始化块

#### 1.4.11.1 初始化块定义

> Java 使用构造器来对**单个对象**进行初始化操作，使用构造器先完成**整个 Java 对象的状态初始化**， 然后将 Java 对象返回给程序，从而让该 Java 对象的信息更加完整 。 与构造器作用非常类似的是初始化块，它也可以对 Java 对象进行初始化操作 。
>
> **初始化块的修饰符只能是 static ， 使用 static 修饰的初始化块被称为静态初始化块。**初始化块可以不使用修饰符。
>
> 初始化块里的代 码可以包含任何可执行性语句，包括定义局部变量、调用其他对象的方法，以及使用分支、循环语句等 。

```java
[修饰符] { 
  // 初始化块的可执行性代码
  ...
}
```

> 初始化块虽然也是 Java 类的一种成员，但它没有名字，也就没有标识，因此无法通过类 、对象来 调用初始化块 。 初始化块只在创建 Java 对象时隐式执行，而且**在执行构造器之前执行。**
>
> 虽然 Java 九许一个类里定义 2 个普通初始化块，但这**没有任何意义 **。 因为初始化块 是在创建 Java 对象时隐式执行的，而且它们总是全部执行，因此完全可以把多个普通初始化块合并成一个初始化块，从而可以让程序更加简洁，可读性史强 。
>

#### 1.4.11.2 初始化块和构造器

> 初始化块是构造器的补充，初始化块总是在构造器执行之前执行。
>
> 与构造器不同的是，初始化块是一段固定执行的代码，它不能接收任何参数 。

#### 1.4.11.3 静态初始化块

> 如果定义初始化块时使用了 stahc 修饰符，则这个初始化块就变成了静态初始化块，也被称为类初 始化块(普通初始化块负责对对象执行初始化，类初始化块则负责对类进行初始化) 。 静态初始化块是 类相关的 ， 系统将在类初始化阶段执行静态初始化块，而不是在创建对象时才执行 。 因此静态初始化块 总是比普通初始化块先执行 。
>
> 静态初始化块是类相关的 ，用 于对整个类进行初始化处理，通常用于对类变量执行初始化处理。静 态初始化块不能对实例变量进行初始化处理 。
>
> 静态初始化块也被称为类初始化块，也属于类的静态成员，同样需要遵循静态成员不 能访问非静态成员的规则，因此静态初始化块不能访问非静态成员，包括不能访问实例变量和实例方法 。

#### 1.4.11.4 初始化块、静态初始化块、构造函数的执行顺序

> 类初始化阶段，先执行最顶层父类的静态初始化块，然后依次向下，直到执行当前类的静态初始化块；
>
> 对象初始化阶段，先执行最顶层父类的初始化块、最顶层父类的构造器，然后依次向下，直到执行当前的初始化块、当前类的构造器。

![Java-Learning-Notes-Picture-2](/Users/lotus/Notes/Java-Learning-Notes/Java-Learning-Notes-Picture-2.png)

## 1.5 面向对象（下）

### 1.5.1 处理对象

#### 1.5.1.1 toString() 方法

> Java 对象都是 Object 类的实例，都可直接调用该类中定义的方法 ，这些方法提供了处理 Java 对象的通用方法 。toStringO方法是 Object 类里的 一个实例方法，所有的 Java 类都是 Object 类的子类，因此所有的 Java 对象都具有 toString() 方法 。
>
> Object 类提供的 toStringO方法总是返回该对象实现类的"类名 +@+ hashCode " 值，这个返回值并 不能真正实现"自我描述"的功能，因此如果用户需要自定义类能实现"自我描述"的功能，就必须重写 Object 类的 toStringO方法 。
>

#### 1.5.1.2 ==和 equals 方法

> Java 程序中测试两个变量是否相等有两种方式 : 一种是利用==运算符，另 一种是利用 equalsO方法 。 
>
> 当使用==来判断两个变量是否相等时，如果两个变量是基本类型变量 ，且都是数值类型(不一定要求数据类型严格相同) ，则只要两个变量的值相等，就将返回 true 。
>
> 对于两个引用类型变量，只有它们指向同一个对象时，== 判断才会返回 true。== 不可用于比较类型上没有父子关系的两个对象 。
>

#### 1.5.1.3 推荐的重写自定义类的 equals 方法

```java
// 重写equals()方法，提供自定义的相等标准
public boolean equals(Object obj)
{
  // 如果两个对象为同一个对象
  if (this == obj)
    return true;
  // 只有当obj是Person对象
  if (obj != null && obj.getClass() == Person.class)
  {
    Person personObj = (Person)obj;
    // 并且当前对象的idStr与obj对象的idStr相等才可判断两个对象相等
    if (this.getIdStr().equals(personObj.getIdStr()))
    {
      return true;
    }
  }
  return false;
}
```

### 1.5.2 类成员

> 在 Java 类里只能包含成员变量、方法、构造器、初始化块、内部类 ( 包括接口、枚举) 5 种成员。

### 1.5.3 final 修饰符

#### 1.5.3.1 final 定义

> final 修饰变量时，表示该变量一旦获得了初始值就不可被改变， fmal 既可 以修饰成员变量( 包括 类变量和 实例变量)， 也可以修饰局部变量、形参 。final 修饰的变量不可被改变， 一旦获得了 初始值 ， 该 final 变量的值就 不能被重新赋值。
>
> **Java 语 法规定 : final 修饰的成员变量必须由程序员显式地指定初始值。**
>
> final 修饰的类变量、实例变量能指定初始值的地方如下：
>
> 1. 类变量 : 必须在静态初始化块中指定初始值或声明该类变量时指定初始值，而且只能在两个地方的其中之一指定。
> 2. 实例变量 :必须在非静态初始化块、声明该实例变量或构造器中指定初始值 ， 而且只能在三个地方的其中之一指定。

#### 1.5.3.2 final Bug

> final 成员变量在显式初始化之前不能直接访问，但可以通过方法来访问，基本上可断定是 Java 设计的一个缺陷 。按照正常逻辑，final A员变量在显式初始化之前是不应该 : 允许被访问的 。因此建议开发者尽量避免在 final 变量显式初始化之前访问它 。
>

```java
public class FinalErrorTest
{
	// 定义一个final修饰的实例变量
	// 系统不会对final成员变量进行默认初始化
	final int age;
	{
		// age没有初始化，所以此处代码将引起错误。
//		System.out.println(age);
		printAge();
		age = 6;
		System.out.println(age);
	}
	public void printAge(){
		System.out.println(age);
	}
	public static void main(String[] args)
	{
		new FinalErrorTest();
	}
}
```

#### 1.5.3.3 final 局部变量

```java
public class FinalLocalVariableTest
{
	public void test(final int a)
	{
		// 不能对final修饰的形参赋值，下面语句非法
		// a = 5;
	}
	public static void main(String[] args)
	{
		// 定义final局部变量时指定默认值，则str变量无法重新赋值
		final String str = "hello";
		// 下面赋值语句非法
		// str = "Java";
		// 定义final局部变量时没有指定默认值，则d变量可被赋值一次
		final double d;
		// 第一次赋初始值，成功
		d = 5.6;
		// 对final变量重复赋值，下面语句非法
		// d = 3.4;
	}
}
```

#### 1.5.3.4 final 修饰基本类型变量和引用类型变量的区别

> 当使用 final 修饰基本类型变量时，不能对基本类型变量重新赋值，因此基本类型变量不能被改变。 但对于引用类型变量而 言 ，它保存的仅仅是一个引用， final 只保证这个引用类型变量所引用的地址不会改变 ， 即 一 直引用同 一个对象，但这个对象完全可以发生改变 。
>

### 1.5.3.5 final 方法

> final 修饰的方法不可被重写 ，如果出于某些原因，不希望子类重写父类的某个方法 ，则可以使用 final 修饰该方法 。
>
> Java 提供的 Object 类里就有一个 final 方法: getClassO ，因为 Java 不希望任何类重写这个方法，所 以使用 final 把这个方法密封起来 。

#### 1.5.3.6 final 类

> **final 修饰的类不可以有子类** ， 例如 java.1ang.Math 类就是一个 final 类 ，它不可以有子类 。

### 1.5.4 不可变类

> 不可变( immutable ) 类的意思是创建该类的实例后， 该实例 的实例变量是不可改变的 。 Java 提供 的 8 个包装类和 java.lang.String 类都是不可变类 ， 当创建它们 的实例后 ， 其实例的 实例变量不可改变 。

> 创建自定义的不可变类，需要遵守如下规则 ：
>
> 1. 使用 private 和 final 修饰符来修饰该类的成员变量。 
> 2. 提供带参数构造器，用于根据传入参数来初始化类里的成员变量 。 
> 3. 仅为该类的成员变量提供 getter 方法，不要为该类的成员变量提供 setter 方法 ，因为普通方法无法修改 final 修饰的成员变量。
> 4. 如果有必要，重写 Object 类的 hashCode()和 equal()方法。equal()方法根据关键成员变量来作为两个对象是否相等的标准，除此之外，还应该保证 两个用 equals()方法判断为相等的对象的 hashCode()也相等 。

```java
public class Address
{
	private final String detail;
	private final String postCode;
	// 在构造器里初始化两个实例变量
	public Address()
	{
		this.detail = "";
		this.postCode = "";
	}
	public Address(String detail , String postCode)
	{
		this.detail = detail;
		this.postCode = postCode;
	}
	// 仅为两个实例变量提供getter方法
	public String getDetail()
	{
		return this.detail;
	}
	public String getPostCode()
	{
		return this.postCode;
	}
	//重写equals()方法，判断两个对象是否相等。
	public boolean equals(Object obj)
	{
		if (this == obj)
		{
			return true;
		}
		if(obj != null && obj.getClass() == Address.class)
		{
			Address ad = (Address)obj;
			// 当detail和postCode相等时，可认为两个Address对象相等。
			if (this.getDetail().equals(ad.getDetail())
				&& this.getPostCode().equals(ad.getPostCode()))
			{
				return true;
			}
		}
		return false;
	}
	public int hashCode()
	{
		return detail.hashCode() + postCode.hashCode() * 31;
	}
}
```

### 1.5.5 缓存实例的不可变类

> 不可变类的实例状态不可改变，可以很方便地被多个对象所共享。如果程序经常需要使用相同的不可变类实例，则 应该考虑缓存这种不可变类的实例 。 毕竟重复创建相同的对象没有太大的 意义，而且加 大系统开销 。 如果可能，应该将已经创建的不可变类的实例进行缓存 。
>
> 缓存是软件设计中 一个非常有用的模式，缓存的实现方式有很多种，不同的实现方式可能存在较大 的性能差别，关于缓存的性能问题此处不做深入讨论 。

```java
class CacheImmutale {
	private static int MAX_SIZE = 10;
	// 使用数组来缓存已有的实例
	private static CacheImmutale[] cache
		= new CacheImmutale[MAX_SIZE];
	// 记录缓存实例在缓存中的位置,cache[pos-1]是最新缓存的实例
	private static int pos = 0;
	private final String name;
	private CacheImmutale(String name) {
		this.name = name;
	}
	public String getName() {
		return name;
	}
	public static CacheImmutale valueOf(String name) {
		// 遍历已缓存的对象，
		for (int i = 0 ; i < MAX_SIZE; i++) {
			// 如果已有相同实例，直接返回该缓存的实例
			if (cache[i] != null
				&& cache[i].getName().equals(name)) {
				return cache[i];
			}
		}
		// 如果缓存池已满
		if (pos == MAX_SIZE) {
			// 把缓存的第一个对象覆盖，即把刚刚生成的对象放在缓存池的最开始位置。
			cache[0] = new CacheImmutale(name);
			// 把pos设为1
			pos = 1;
		} else {
			// 把新创建的对象缓存起来，pos加1
			cache[pos++] = new CacheImmutale(name);
		}
		return cache[pos - 1];
	}
	public boolean equals(Object obj) {
		if(this == obj) {
			return true;
		}
		if (obj != null && obj.getClass() == CacheImmutale.class) {
			CacheImmutale ci = (CacheImmutale)obj;
			return name.equals(ci.getName());
		}
		return false;
	}
	public int hashCode() {
		return name.hashCode();
	}
}
public class CacheImmutaleTest {
	public static void main(String[] args) {
		CacheImmutale c1 = CacheImmutale.valueOf("hello");
		CacheImmutale c2 = CacheImmutale.valueOf("hello");
		// 下面代码将输出true
		System.out.println(c1 == c2);
	}
}
```

### 1.5.6 抽象类

#### 1.5.6.1 抽象方法和抽象类

> 抽象方法和抽象类的规则如下：
>
> 1. 抽象类必须使用 abstract 修饰符来修饰，抽象方法也必须使用 abstract 修饰符来修饰，抽象方法 不能有方法体 。
> 2. 抽象类不能被实例化， 无法使用 new 关键字来调用抽象类的构造器创建抽象类的实例 。 即使抽象类里不包含抽象方法，这个抽象类也不能创建实例 。 
> 3. 抽象类可以包含成员变量、方法(普通方法和抽象方法都可以)、构造器 、 初始化块、内部类(接 口、枚举) 5 种成分 。 抽象类 的构造器不能用于创建实例 ， 主要是用于被其子类调用。 
> 4. 含有抽 象方法的类 ( 包括直接定义了 一个抽 象方法 : 或继承了一个抽象父类，但没有完全实现父类包含的抽 象方法 ; 或实现了一个接口， 但没有完全实现接口包含的抽象方法三种情况)只能被定义成抽象类 。

> 定义抽象方法只需在普通方法上增加 abstract 修饰符 ，并把普通方法的方法体( 也就是方法后花括号括起来 的部分〉全部去掉 ，并在方法后增加分号即可。
>

> 定义抽象类只需在普通类上增加 abstract 修饰符即可 。 甚至一个普通类(没有包含抽象方法的类)增加 abstract 修饰符后也将变成抽象类 。 
>

> abstract 不能用于修饰成员变量，不能用于修饰局部变量，即没有抽象变量、没有抽象成员变量等说法 ， abstract 也不能用于修饰构造器，没有抽象构造器，抽象类里定义的 构造器只能是普通构造器 。
>

> 当使用 abstract 修饰类时，表明这个类只能被继承;当使用 abstract 修饰方法时 ， 表明这个方法必须由子类提供实现(即重写) 。 而 final 修饰的类不能被继承 ，自lal 修饰的方法不能被重写 。 因此 **final和 abstract 永远不能同时使用 。**
>
> 当使用 static 修饰一个方法时，表明这个方法属于该类本身，即通过类就可调用该方法，但如果该方法被定义成抽象方法，则将导致通过该类来调用该方法时出现错误(调用了一个没有方法体的方法肯定会引起错误)。因此**static 和 abstract 不能同时修饰某个方法，即没有所谓的类抽象方法。**
>
> **static 和 abstract 并不是绝对互斥的，static 和 abstract 虽然不能同时修饰某个方法，但它们可以同时修饰内部类 。**
>
> **abstract 关键字修饰的方法必须被其子类重写才有意义，否则这个方法将永远不会有 方法休，因此 abstract 方法不能定义为 private 访问权限，即 private 和 abstract 不能同时修饰方法 。**

### 1.5.7 Java 9 改进的接口

> Java 9 对接口进行了改进，允许在接口中定义默认方法和类方法， 默认方法和类方法都可以提供方法实现， Java 9 为接口增加了一种私有方法，私有方法也可提供方法实现。
>

#### 1.5.7.1 Java 9 中接口的定义

```java
[修饰符] interface 接口名 extends 父接口 1 ，父接口 2. . .
{
  零个到多个常量定义... 
  零个到多个抽象方法定义... 
  零个到多个内部类、接口、枚举定义... 
  零个到多个私有方法、默认方法或类方法定义...
}
```

> 1. 修饰符可以是 public 或者省略，如果省略了 public 访问控制符，则默认采用包权限访问控制符，即只有在相同包结构下才可以访问该接口。
> 2. 接口名应与类名采用相同的命名规则，即如果仅从语法角度来看，接口名只要是合法的标识符即可;如果要遵守 Java 可读性规范，则接口名应由多个有意义的单词连缀而成，每个单词首字母大写，单词与单词之间无须任何分隔符。接口名通常能够使用形容词。 
> 3. 一个接口可以有多个直接父接口，但接口只能继承接口，不能继承类。

> 在上面语法定义中，只有在 Java 8 以上的版本中才九许在接口中定义默认方法、类方法。

> 由于接口定义的是一种规范，因此**接口里不能包含构造器和初始化块定义**。 接口里可以包含成员变量(只能是静态常量)、方法(只能是抽象实例方法、类方法 、默认方法或私有方法)、内部类(包括内 部接口、枚举)定义。
>
> 对比接口和类的定义方式，不难发现接口的成员比类里的成员少了两种，而且接口里的成员变量只能是静态常量，接口里的方法只能是抽象方法、类方法、默认方法或私有方法。
>
> 接口里定义的是多个类共同的公共行为规范，因此接口里的常量、方法、内部类 和内部枚举**都是 public 访问权限**。定义接口成员时，可以省略访问控制修饰符，如果指定访问控制修饰 符，则只能使用 public 访问控制修饰符。

> **Java 9 为接口增加了一种新的私有方法，其实私有方法的主要作用就是作为工具方法，为接 口中的 默认方法或类方法提供支持。私有方法可以拥有方法体，但私有方法不能使用 default 修饰。私有方法 可以使用 staÌlc 修饰 ，也就是说，私有方法既可是类方法，也可是实例方法。**

> 对于接口里定义的静态常量而言，它们是接口相关的，因此系统会自动为这些成员变量增加 stahc 和 final 两个修饰符。也就是说，在接口中定义成员变量时，不管是否使用 public static final 修饰符，接 口里的成员变量总是使用这三个修饰符来修饰。而且接口里没有构造器和初始化块，因此接口里定义的 成员变量只能在定义时指定默认值 。
>
> 接口里定义成员变量采用如下两行代码的结果完全一样:

```java
//系统自动为接口里定义 的成员变量增加 public static final 修饰符
int MAX SIZE = 50;
public static final int SIZE_MAX = 50;
```

> **接口里定义的方法只能是抽象方法、类方法、默认方法或私有方法，因此如果不是定义默认方法、类方法或私有方法，系统将自动为普通方法增加 abstract 修饰符:定义接口里的普通方法时不管是否使 用 public abstract 修饰符，接口里的普通方法总是使用 public abstract 来修饰 。接口里 的普通方法不能有 方法实现(方法体);但类方法、默认方法、私有方法都必须有方法实现(方法体)。**

```java
public interface Output
{
	// 接口里定义的成员变量只能是常量
	int MAX_CACHE_LINE = 50;
	// 接口里定义的普通方法只能是public的抽象方法
	void out();
	void getData(String msg);
	// 在接口中定义默认方法，需要使用default修饰
	default void print(String... msgs)
	{
		for (String msg : msgs)
		{
			System.out.println(msg);
		}
	}
	// 在接口中定义默认方法，需要使用default修饰
	default void test()
	{
		System.out.println("默认的test()方法");
	}
	// 在接口中定义类方法，需要使用static修饰
	static String staticTest()
	{
		return "接口里的类方法";
	}
	// 定义私有方法
	private void foo()
	{
		System.out.println("foo私有方法");
	}
	// 定义私有静态方法
	private static void bar()
	{
		System.out.println("bar私有静态方法");
	}
}
```

> Java 8 允许在接口中定义默认方法，默认方法必须使用 default 修饰，该方法不能使用 static 修饰， 无论程序是否指定，默认方法总是使用 public 修饰一一如果开发者没有指定 public ， 系统会自动为默认 方法添加 public 修饰符 。 由于默认方法并没有 static 修饰，因此**不能直接使用接口来调用默认方法**，需要使用接口的实现类的实例来调用这些默认方法 。
>
> **接口的默认方法其实就是实例方法**，但由于早期 Java 的设计是:接口中的实例方法 不能有方法体; Java 8 也不能直接"推倒"以前的规则，因此只好重定义一个所谓的"默认方法"，**默认方法就是有方法体的实例方法。**
>
> **Java 8 允许在接口中定义类方法， 类方法必须使用 static 修饰 ， 该方法不能使用 default 修饰**，无论程序是否指定，类方法总是使用 public 修饰一一如果开发者没有指定 public ，系统会自动为类方法添加 public 修饰符。类方法可以直接使用接口来调用 。
>
> **Java 9 增加了带方法体的私有方法**，这也是 Java 8 埋下的伏笔: Java 8 允许在接口中定义带方法体 的默认方法和类方法一一这样势必会引发一个问题， 当两个默认方法(或类方法) 中包含一段相同的实现逻辑时，程序必然考虑将这段实现逻辑抽取成工具方法，而工具方法是应该被隐藏 的，这就是 Java 9 增加私有方法的必然性。

> 接口里的成员变量默认是使用 public static final 修饰的，因此即使另 一个类处于不同包下，也可以通过接口来访问接口里的成员变量。
>

#### 1.5.7.2 接口的继承

> 接口的继承和类继承不一样，接口完全支持多继承，即 一个接口可以有多个直接父接口。和类继承相似，子接口扩展某个父接口，将会获得父接口里定义的所有抽象方法、常量。
>
> 一个接口继承多个父接口时，多个父接口排在 extends 关键宇之后，多个父接口之间以英文逗号 (,) 隔开。

#### 1.5.7.3 使用接口

> 接口不能用于创建实例 ， 但接口可以用于声明引用类型变量 。当使用接口来声 明引用类型变量时 ， 这个引用类型变量必须引用到其实现类的对象。除此之外，接口的主要用途就是被实现类实现 。 归纳起 来，接口主要有如下用途：
>
> 1. 定义变量 ，也可用于进行强制类型转换 。
> 2. 调用接口中定义的常量 。
> 3. 被其他类实现 。

> 一个类可以实现一个或多个接口，继承使用 extends 关键字，实现则使用 implements 关键字 。 因为 一个类可以实现多个接口，这也是 Java 为单继承灵活性不足所做的补充 。

```java
[修饰符] class 类名 extends 父类 implements 接口1, 接口2...
{
  类体部分
}
```

> **一个类实现了一个或多个接口之后 ，这个类必须完全实现这些接口里所定义的全部抽象方法(也就 是重写这些抽象方法);否则，该类将保留从父接口那里继承到的抽象方法，该类也必须定义成抽象类。**

> 实现接口方法时，必须使用 public 访问控制修饰符，因为接口里的方法都是 public 的，而子类(相当于实现类)重写父类方法时访问权限只能更大或者相等，所以实现类实 现接口里的方法时只能使用 public 访问权限。
>

#### 1.5.7.4 接口和抽象类

> 相同点：
>
> 1. 接口 和抽象类都不能被实例化，它们都位于继承树的顶端 ，用于被其他类实现和继承。 
> 2. 接口和抽象类都可以包含抽象方法，实现接口或继承抽象类的普通子类都必须实现这些抽象方法 。

> 不同点：
>
> 1. **接口体现的是一种规范，标准；抽象类所体现的是一种模板式设计，能力。** 
>    1. 接口作为系统与外界交互的窗口 ， 接口体现的是一种规范 。 对于接口的实现者而 言，接口 规定了实 现者必须向外提供哪些服务(以方法的形式来提供);对于接口的调用者而 言 ， 接口规定了调用者可 以 调用哪些服务，以及如何调用这些服务(就是如何来调用方法) 。当在一个程序 中使用接口时，接口是 多个模块 间的藕合标准:当在多个应用程序之间使用接口时 ， 接口是多个程序之 间的通信标准。接口类似于整个系统的"总纲"，它制定了系统各模块应该遵循的标准，因此 一个系统中的接口不应该经常改变 。一旦接 口 被改变 ， 对整个系统甚至其他系统的影响将是辐射式的， 导致系统中大部分类都需要改写 。
>    2. 抽象类作为系统中多个子类的共同父类 ， 它所体现的是一种模板式设计。 抽 象类 作为多个子类的抽象父类，可以被当成系统实现过程中的中间 产品 ， 这个中间产品己经实现了系统 的部 分功能(那些己经提供实现的方法) ，但这个产品依然不能当成最终产品，必须有更进一步的完善 ，这 种完善可能有几种不同方式 。
> 2. 用法上不同
>    1. 接口里只能包含抽象方法、静态方法、默认方法和私有方法，不能为普通方法提供方法实现；抽象类则完全可以包含普通方法。 
>    2. 接口里只能定义静态常量 ，不能定义普通成员变量 :抽象类里则既可以定义普通成员变量 ，也可以定义静态常量。 
>    3. 接口里不包含构造器;抽象类里可以包含构造器，抽象类里的构造器并不是用于创建对象，而是让其子类调用这些构造器来完成属于抽象类的初始化操作 。 
>    4. 接口里不能包含初始化块:但抽象类则完全可以包含初始化块 。 
>    5. 一个类最多只能有一个直接父类，包括抽象类;但一个类可以直接实现多个接口，通过实现多个接口可以弥补 Java 单继承的不足。

### 1.5.8 内部类

> 大部分时候，类被定义成一个独立 的程序单元。在某些情况下， 也会**把一个类放在另一个类 的内部定义 ， 这个定义在其他类 内 部的类就被称为内部类(有的地方也叫嵌套类)**，包含内部类的类也被称为 外部类(有的地方也叫宿主类 )  Java 从 JDK l.l 开始引入内部类 ，内 部类主要有如下作用：
>
> 1. 内部类提供了更好的封装，可以把内部类隐藏在外部类之内，不允许同 一个包中的其他类访问该类 。 
>    1. 假设需要创建 Cow 类， Cow 类需要组合一个 CowLeg 对象， CowLeg 类只有在 Cow 类里 才有效，离开了 Cow 类之后没有任何意义 。 在这种情况下 ， 就可把 CowLeg 定义成 Cow 的内 部类，不允许其他类访问 CowLeg 。 
> 2. 内部类成员可以直接访问外部类的私有数据，因为内部类被当成其外部类成员，同 一个类的成 员之间可以互相访 问 。 但外部类不能访 问内 部类的实现细节 ，例如内 部类的成员变量 。 
> 3. 匿名内部类适合用于创建那些仅需要一 次使用的类 。 
>    1. 对于前面介绍的命令模式，当需要传入一个 Command 对象时，重新专门定义 PrintCommand 和 AddCommand 两个实现类可能没有太大的意义 ， 因为这两个实现类可能仅需要使用一次 。 在这种情况下 ， 使用匿名内部类将更方便。

> 内部类与外部类相比：
>
> 1. 内部类比外部类可以多使用 三个修饰符: private、 protected 、 static 一一外部类不可以使用这三个修饰符 。
>
>
> 2. 非静态内部类不能拥有静态成员。

#### 1.5.8.1 非静态内部类

> 成员内部类分为两种 : 静态内部类和非静态内部类，使用 static 修饰的成员内部类是静态内部类 ， 没有使用 static 修饰的成员内部类是非静态内部类。
>
> **非静态内部类的成员可以访问外部类的 private 成员，但反过来就不成立了。**非静态内部类的成员只在非静态内部类范围内是可知的 ， 并不能被外部类直接使用。**如果外部类需要访问非静态内部类的成 员，则必须显式创建非静态 内 部类对象来调用访问其实例成员。**

```java
public class Outer {
	private int outProp = 9;
	class Inner {
		private int inProp = 5;
		public void acessOuterProp() {
			// 非静态内部类可以直接访问外部类的private成员变量
			System.out.println("外部类的outProp值:"
				+ outProp);
		}
	}
	public void accessInnerProp() {
		// 外部类不能直接访问非静态内部类的实例变量,
		// 下面代码出现编译错误
		// System.out.println("内部类的inProp值:" + inProp);
		// 如需访问内部类的实例变量，必须显式创建内部类对象
		System.out.println("内部类的inProp值:"
			+ new Inner().inProp);
	}
	public static void main(String[] args) {
		// 执行下面代码，只创建了外部类对象，还未创建内部类对象
		Outer out = new Outer();      //①
		out.accessInnerProp();
	}
}
```

> 根据静态成员不能访问非静态成员的规则， 外部类的静态方法、静态代码块不能访 问 非静态内部类 ， 包括不能使用非静态内部类定义变量、 创建实例等。总之 ， 不允许在外部类的静态成员中直接使用非静态内部类。
>
> Java 不允许在非静态内部类里定义静态成员 。
>
> 非静态内部类里不能有静态方法、静态成员变量、静态初始化块。
>
> 非静态内部类里不可以有静态初始化块，但可以包含普通初始化块。 非静态内部类普 通初始化块的作用与外部类初始化块的作用完全相同 。

#### 1.5.8.2 静态内部类

> 如果使用 static 来修饰一个内部类，则这个内部类就属于外部类本身，而不属于外部类的某个对象。因此使用 statlc 修饰的内部类被称为类内部类，有的地方也称为静态内部类 。

> **静态内部类可以包含静态成员， 也可以包含非静态成员 。** 根据静态成员不能访问非静态成员的规则，静态内部类不能访问外部类的实例成员，只能访问外部类的类成员 。 即使是静态内部类的实例方法也不能访问外部类的实例成员，只能访问外部类的静态成员 。

> 静态内部类是外部类的 一个静态成员，因此外部类的所有方法、所有初始化块中可以使用静态内部类来定义变量、 创建对象等。 外部类依然不能直接访问静态内部类的成员，但可以使用静态内部类的类名作为调用者来访问静态 内部类的类成员，也可以使用静态内部类对象作为调用者来访问静态 内 部类的实例成员。
>

```java
public class AccessStaticInnerClass
{
	static class StaticInnerClass
	{
		private static int prop1 = 5;
		private int prop2 = 9;
	}
	public void accessInnerProp()
	{
		// System.out.println(prop1);
		// 上面代码出现错误，应改为如下形式：
		// 通过类名访问静态内部类的类成员
		System.out.println(StaticInnerClass.prop1);
		// System.out.println(prop2);
		// 上面代码出现错误，应改为如下形式：
		// 通过实例访问静态内部类的实例成员
		System.out.println(new StaticInnerClass().prop2);
	}
}
```

> Java 还允许在接口里定义内部类，接口里定义的内部类默认使用 public static 修饰 ，也 就是说 ， 接口内部类只能是静态内部类。
>
>  如果为接口内部类指定访问控制符 ，则只能指定 public 访问控制符 ; 如果定义接口内部类时省略访问控制符，则该内部类默认是 public 访问控制权限 。

#### 1.5.8.3 使用内部类

	> 定义类的主要作用就是定义变量、创建实例和作为父类被继承 。 定义内部类的主要作用也如此，但 使用内部类定义变量和创建实例则与外部类存在一些小小的差异 。 下面分三种情况讨论内部类的用法。

##### 1.5.8.3.1 在外部类内部使用内部类；

> 1. 在外部类内部使用内部类时，与平常使用普通类没有太大的区别 。一样可以 直接通过内部类类名来定义变量，通过 new 调用内部类构造器来创建实例 。
> 2. 唯一存在的一个区别是:不要在外部类的静态成员(包括静态方法和静态初始化块)中使用非静态 内部类，因为静态成员不能访问非静态成员。
> 3. 在外部类内部定义内部类的子类与平常定义子类也没有太大的区别 。

***#####*** 1.5.8.3.2 在外部类以外使用非静态内部类；

> 1. 如果希望在外部类以外的地方访问内部类(包括静态和非静态两种) ，则内部类不能使用 pnvate 访 问控制权限， private 修饰的内部类只能在外部类 内部使用 。 对于使用其他访问控制符修饰的内部类， 则能在访问控制符对应的访问权限内使用。
> 2. 省略访问控制符的内部类，只能被与外部类处于同 一个包中的其他类所访问 。 
> 3. 使用 protected 修饰的内部类，可被与外部类处于同 一 个包中的其他类和外部类的子类所访问。 
> 4. 使用 public 修饰的内部类，可以在任何地方被访问 。

> 在外部类以外的地方定义内部类(包括静态和非静态两种)变量的语法格式如下:
>
> OuterClass . InnerClass varName

> 在外部类以外的地方创建非静态内部类实例的语法如下 :
>
> OuterInstance .new InnerConstructor()

> 在外部类以外的地方创建非静态内部类实例必须使用外部类实例和 new 来调用非静态内部类的构造器。
>

```java
class Out
{
	// 定义一个内部类，不使用访问控制符，
	// 即只有同一个包中其他类可访问该内部类
	class In
	{
		public In(String msg)
		{
			System.out.println(msg);
		}
	}
}
public class CreateInnerInstance
{
	public static void main(String[] args)
	{
		Out.In in = new Out().new In("测试信息");
		/*
		上面代码可改为如下三行代码：
		使用OutterClass.InnerClass的形式定义内部类变量
		Out.In in;
		创建外部类实例，非静态内部类实例将寄存在该实例中
		Out out = new Out();
		通过外部类实例和new来调用内部类构造器创建非静态内部类实例
		in = out.new In("测试信息");
		*/
	}
}
```

> 如果需要在外部类以外的地方创建非静态内部类的子类，则尤其要注意上面的规则:非静态内部类 的构造器必须通过其外部类对象来调用 。
>
> 非静态内部类的子类 不一定是内部类， 它可以是一个外部类。 但非静态内部类的子类 实例一样需要保留一个引用，该引用指向其父类所在外部类的对象。也就是说，如果有一 个内部类子类的对象存在，则一定存在与之对应的外部类对象。

##### 1.5.8.3.3 在外部类以外使用静态内部类

> 因为静态内部类是外部类类相关的，因此创建静态内部类对象时无须创建外部类对象。在外部类以 外的地方创建静态内部类实例的语法如下 :
>
> new OuterClass. InnerConstructor ()

#### 1.5.8.4 局部内部类

> **如果把一个内部类放在方法里定义，则这个内部类就是 一个局部内部类 ，** 局部内部类仅在该方法里有效。由于局部内部类不能在外部类的方法以外的地方使用，因此局部内部类也不能使用访问控制符和static 修饰符修饰。
>
> 对于局 部成员 而言，不 管是局部变量还是局部内部类，它们的 上一级程序羊元都是方 法，而不是类，使用 static 修饰它们没有任何意义。 因此 ，所有的局部成员都不能使用 stattc 修饰 。 不仅如此 ， 因为局 部成员的作用域是所在方法，其他程序单元永远也不可能访问另 一个方法中的局部成员 ， 所以所有的局部成员都不能使用访问控制符修饰 。

> **局部内部类走一个非常 "鸡肋" 的语法，在实际开发中很少定义局部内部类 ，这是因为局部内部类的作用域太小了:只能在当前方法中使用 。 大部分时候，定义一个类之后， 当然希望多次复用这个类 ，但局部 内部类无法离开它所在的方法 ， 因此在实际开发中很少 使用局部内部类 。**

```java
public class LocalInnerClass
{
	public static void main(String[] args)
	{
		// 定义局部内部类
		class InnerBase
		{
			int a;
		}
		// 定义局部内部类的子类
		class InnerSub extends InnerBase
		{
			int b;
		}
		// 创建局部内部类的对象
		InnerSub is = new InnerSub();
		is.a = 5;
		is.b = 8;
		System.out.println("InnerSub对象的a和b实例变量是："
			+ is.a + "," + is.b);
	}
}
```

#### 1.5.8.5 Java 8 改进的匿名内部类

> 匿名内部类适合创建那种只需要一次使用的类 ，例如前面介绍命令模式时所需要的 Command 对象。匿名内部类的语法有点奇怪 ，创建匿名内部类时会立即创建一个该类的实例 ， 这个类定义立即消失 ， 匿名内部类不能重复使用 。
>
> 定义匿名内部类的格式如下 :

```java
new 实现接口() | 父类构造器(实参列表 ) 
{
  //匿名内部类的类体部分
}
```

> 匿名内部类必须继承一个父类，或实现一个接口 ， 但最多只能继承一个父类， 或实现一个接口 。 关于医名内部类还有如下两条规则。
>
> 1. 匿名内部类不能是抽象类，因为系统在创建匿名内部类时，会立即 创建匿名内部类的对象。因 此不 允许将匿名内部类定义成抽 象类。 
> 2. 匿名内部类不能定义构造器 。由于匿 名内部类没有类名，所以无法定义构造器，但匿名内部类可以定义初始化块 ，可以通过实例初始化块来完成构造器需要完成的事情。

> 最常用的创建医名内部类的方式是需要创建某个接口类型的对象，如下程序所示 。

```java
interface Product
{
	public double getPrice();
	public String getName();
}
public class AnonymousTest
{
	public void test(Product p)
	{
		System.out.println("购买了一个" + p.getName()
			+ "，花掉了" + p.getPrice());
	}
	public static void main(String[] args)
	{
		AnonymousTest ta = new AnonymousTest();
		// 调用test()方法时，需要传入一个Product参数，
		// 此处传入其匿名实现类的实例
		ta.test(new Product()
		{
			public double getPrice()
			{
				return 567.8;
			}
			public String getName()
			{
				return "AGP显卡";
			}
		});
	}
}
```

> 当通过实现接口来创建匿名内部类时 ， 匿名 内部类也不能显式创建构造器，因此医名内部类只有一 个隐式的无参数构造器，故 new 接口名后的括号里不能传入参数值 。 但如果通过继承父类来创建匿名内部类时， 匿名 内部类将拥有和父类相似的构造器。

```java
abstract class Device
{
	private String name;
	public abstract double getPrice();
	public Device(){}
	public Device(String name)
	{
		this.name = name;
	}
	// 此处省略了name的setter和getter方法
	public void setName(String name)
	{
		this.name = name;
	}
	public String getName()
	{
		return this.name;
	}
}
public class AnonymousInner
{
	public void test(Device d)
	{
		System.out.println("购买了一个" + d.getName()
			+ "，花掉了" + d.getPrice());
	}
	public static void main(String[] args)
	{
		AnonymousInner ai = new AnonymousInner();
		// 调用有参数的构造器创建Device匿名实现类的对象
		ai.test(new Device("电子示波器")
		{
			public double getPrice()
			{
				return 67.8;
			}
		});
		// 调用无参数的构造器创建Device匿名实现类的对象
		Device d = new Device()
		{
			// 初始化块
			{
				System.out.println("匿名内部类的初始化块...");
			}
			// 实现抽象方法
			public double getPrice()
			{
				return 56.2;
			}
			// 重写父类的实例方法
			public String getName()
			{
				return "键盘";
			}
		};
		ai.test(d);
	}
}
```

> 当创建匿名内部类时，必须实现接口或抽象父类里的所有抽象方法 。 如果有需要，也可以重写父类 中的普通方法。

> 在 Java 8 之前， Java 要求被局部内部类、匿名 内部类访问的局部变量必须使用 final 修饰，从 Java 8 开始这个限制被取消了， Java 8 更加智能:如果局部变量被匿名 内部类访问，那么该局部变量相当于自 动使用了 final 修饰 。

```java
interface A
{
	void test();
}
public class ATest
{
	public static void main(String[] args)
	{
		int age = 8;     // ①
		// 下面代码将会导致编译错误
		// 由于age局部变量被匿名内部类访问了，因此age相当于被final修饰了
//		age = 2;
		A a = new A()
		{
			public void test()
			{
				// 在Java 8以前下面语句将提示错误：age必须使用final修饰
				// 从Java 8开始，匿名内部类、局部内部类允许访问非final的局部变量
				System.out.println(age);
			}
		};
		a.test();
	}
}
```

### 1.5.9 Java 8 新增的 Lambda 表达式 

> **Lambda 表达式支持将代码块作为方法参数**， Lambda 表达式允许使用更简洁的代码来创建只有一个抽象方法的接口(这 种接口被称为函数式接口)的实例 。

#### 1.5.9.1 Lambda 表达式入门

> 先使用匿名内部类实现：

```java
public interface Command {
	// 接口里定义的process()方法用于封装“处理行为”
	void process(int[] target);
}

public class ProcessArray {
	public void process(int[] target , Command cmd) {
		cmd.process(target);
	}
}

public class CommandTest {
	public static void main(String[] args) {
		ProcessArray pa = new ProcessArray();
		int[] array = {3, -4, 6, 4};
		// 处理数组，具体处理行为取决于匿名内部类
		pa.process(array , new Command() {
				public void process(int[] target) {
					int sum = 0;
					for (int tmp : target ) {
						sum += tmp;
					}
					System.out.println("数组元素的总和是:" + sum);
				}
			});
	}
}
```

> Lambda 表达式完全可用于简化创建匿名内部类对象:

```java
public class CommandTest2 {
	public static void main(String[] args) {
		ProcessArray pa = new ProcessArray();
		int[] array = {3, -4, 6, 4};
		// 处理数组，具体处理行为取决于匿名内部类
		pa.process(array , (int[] target)->{
				int sum = 0;
				for (int tmp : target ) {
					sum += tmp;
				}
				System.out.println("数组元素的总和是:" + sum);
			});
	}
}
```

> 与创建匿名内部类时需要实现的 process(int[] target)方法完全相同，**lambda 表达式只是不需要 new Xx(){} 这种烦琐的代码，不需要指出重写的方法名字，也不需要给出重写的方法的返回值类型一一只要给出重写的方法括号以及括号里的形参列表即可。**
>

> 当使用 Lambda 表达式代替匿名内部类创建对象时， Lambda 表达式的代码块将会代替实现抽象方法的方法体， Lambda 表达式就相当 一个匿名方法。

> Lambda 表达式的主要作用就是代替匿名内部类的烦琐语法。它由三部分组成:
>
> 1. 形参列表 。形参列表允许省略形参类型 。如果形参列表中只有一个参数，甚至连形参列表的圆括号也可以省略 。
> 2. 箭头（-> ）。必须通过英文中画线和大于符号组成。
> 3. 代码块。如果代码块只包含一条语句 ， Lambda 表达式允许省略代码块的花括号 ，那么这条语句 就不要用花括号表示语句结束 。 Lambda 代码块只有一条 return 语句，甚至可以省略 return 关键 字。 Lambda 表达式需要返回值，而它的代码块中仅有一条省略了 retum 的语句 ， Lambda 表达式会自动返回这条语句的值。

> Lambda 表达式的几种简化写法。

```java
interface Eatable {
	void taste();
}
interface Flyable {
	void fly(String weather);
}
interface Addable {
	int add(int a , int b);
}
public class LambdaQs {
	// 调用该方法需要Eatable对象
	public void eat(Eatable e) {
		System.out.println(e);
		e.taste();
	}
	// 调用该方法需要Flyable对象
	public void drive(Flyable f) {
		System.out.println("我正在驾驶：" + f);
		f.fly("【碧空如洗的晴日】");
	}
	// 调用该方法需要Addable对象
	public void test(Addable add) {
		System.out.println("5与3的和为：" + add.add(5, 3));
	}
	public static void main(String[] args) {
		LambdaQs lq = new LambdaQs();
		// Lambda表达式的代码块只有一条语句，可以省略花括号。
		lq.eat(()-> System.out.println("苹果的味道不错！"));
		// Lambda表达式的形参列表只有一个形参，省略圆括号
		lq.drive(weather -> {
			System.out.println("今天天气是：" + weather);
			System.out.println("直升机飞行平稳");
		});
		// Lambda表达式的代码块只有一条语句，省略花括号
		// 代码块中只有一条语句，即使该表达式需要返回值，也可以省略return关键字。
		lq.test((a , b)->a + b);
	}
}
```

> 第一段粗体字代码使用 Lambda 表达式相当于不带形参的匿名方法，由于该 Lambda 表达式的代码块只有一行代码 ， 因此可以省略代码块的花括号；
>
> 第二段粗体字代码使用 Lambda 表达式相当于只带一个形参的医名方法 ，由于该 Lambda 表达式的形参列表只有一个形参，因此省略了形参列表的圆括号；
>
> 第三段粗体字代码的 Lambda 表达式 的代码块中只有一行语句，这行语句的返回值将作为该代码块的返回值 。

#### 1.5.9.2 Lambda 表达式与函数式接口

> Lambda 表达式的类型，也被称为"目标类型( target type) " , Lambda 表达式的目标类型必须是"函数式接口( functional interface ) " 。函数式接口代表只包含一个抽象方法的接口。函数式接口可以包含多个默认方法、类方法，但只能声明一个抽象方法 。
>

> 如果采用匿名内部类语法来创建函数式接口的实例，则只需要实现一个抽象方法，在这种情况下即可采用 Lambda 表达式来创建对象，该表达式创建出来的对象的目标类型就是这个函数式接口。 查询 Java 8 的 API 文档，可以发现大量的函数式接口，例如: Runnable、 ActionListener 等接口都是函数式接口 。

> Java 8 专门为函数式接口提供了 @FunctionalInterface 注解，该注解通常放在接口定义前面，该注解对程序功能没有任何作用，它用于告诉编译器执行更严格检查一一检查该接口必须是函数式接口，否则编译器就会报错 。

```java
@FunctionalInterface
interface FkTest
{
	void run();
}

public class LambdaTest
{
	public static void main(String[] args)
	{
		// Runnable接口中只包含一个无参数的方法
		// Lambda表达式代表的匿名方法实现了Runnable接口中唯一的、无参数的方法
		// 因此下面的Lambda表达式创建了一个Runnable对象
		Runnable r = () -> {
			for(int i = 0 ; i < 100 ; i ++)
			{
				System.out.println();
			}
		};
//		// 下面代码报错: 不兼容的类型: Object不是函数接口
//		Object obj = () -> {
//			for(int i = 0 ; i < 100 ; i ++)
//			{
//				System.out.println();
//			}
//		};

		Object obj1 = (Runnable)() -> {
			for(int i = 0 ; i < 100 ; i ++)
			{
				System.out.println();
			}
		};

		// 同样的Lambda表达式可以被当成不同的目标类型，唯一的要求是：
		// Lambda表达式的形参列表与函数式接口中唯一的抽象方法的形参列表相同
		Object obj2 = (FkTest)() -> {
			for(int i = 0 ; i < 100 ; i ++)
			{
				System.out.println();
			}
		};

	}
}
```

> Lambda 表达式实现的是匿名方法 -- 因此它只能实现特定函数式接口中的唯一方法。这意味着 Lambda 表达式有如下两个限制 。
>
> 1. Lambda 表达式的目标类型必须是明确的函数式接口 。 
> 2. Lambda 表达式只能为函数式接口创建对象 。 Lambda 表达式只能实现一个方法 ，只有一个抽象方法的接口(函数式接口〉创建对象 。

> Lambda 表达式的目标类型必须是明确的函数式接口。
>
> 为了保证 Lambda 表达式的目标类型是一个明确的函数式接口，可以有如下三种常见方式 。
>
> 1. 将 Lambda 表达式赋值给函数式接口类型的变量。
> 2. 将 Lambda 表达式作为函数式接口类型的参数传给某个方法。
> 3. 使用函数式接口对 Lambda 表达式进行强制类型转换。

> Java 8 在 java.util.function 包下预定义了大量函数式接口，典型地包含如下 4 类接口 。
>
> 1. XxxFunction: 这类接口中通常包含一个 applyO抽象方法，该方法对参数进行处理、转换 CapplyO 方法的处理逻辑由 Lambda 表达式来实现)，然后返回 一个新的值 。 该函数式接口通常用于对指定数据进行转换处理 。
>
> 2.  XxxConsumer: 这类接口中通常包含一个 acceptO抽象方法，该方法与 XxxFunction 接口中的 applyO方法基本相似，也负责对参数进行处理，只是该方法不会返回处理结果 。 
> 3. XxxxPredicate: 这类接口中通常包含一个 testO抽象方法，该方法通常用来对参数进行某种判断 （testO方法的判断逻辑由 Lambda 表达式来实现)，然后返回 一个 boolean 值 。 该接口通常用于判 断参数是否满足特定条件，经常用于进行筛滤数据 。 
> 4. XxxSupplier: 这类接口中通常包含一个 getAsXxxO抽象方法，该力法不需要输入参数，该力法 会按某种逻辑算法 （getAsXxx 0方法的逻辑算法由 Lambda 表达式来实现）返回 一个数据。 

> 综上所述，不难发现 Lambda 表达式的本质很简单，就是使用简洁的语法来创建函数式接口的实例 -- 这种语法避免了匿名内部类的烦琐 。

#### 1.5.9.3 方法引用与构造器引用

> 如果 Lambda 表达式的代码块只有一条代码，程序就可以省略 Lambda 表达式中代码块的花括号 。 不仅如此，**如果 Lambda 表达式的代码块只有一条代码，还可以在代码块中使用方法引用和构造器引用 。**
>
> 方法引用和构造器引用可以让 Lambda 表达式的代码块更加简洁 。 方法引用和构造器引用都需要使 用两个英文冒号 。

| 种类                     | 示例             | 说明                                                         | 对应Lambda表达式                        |
| ------------------------ | ---------------- | ------------------------------------------------------------ | --------------------------------------- |
| 引用类方法               | 类名:类方法      | 函数式接口中被实现方法的全部参数传给 该类方法作为参数        | (a, b,...) ->类名.类方法(a, b,...)      |
| 引用特定对象的实 例 方法 | 特定对象实例方法 | 函数式接口中被 实 现方法的全部参数传给 该方法作为参数        | (a, b,...)->特定对象.实例方法(a, b,...) |
| 引用某类对象的实例方法   | 类名实例方法     | 函数式接口中被实现方法的第 一 个参数作为调用 者 ，后面的参数全部传给该方法作为参数 | (a, b,...) ->a 实例方法(b,...)          |
| 引用构造器               | 类名::new        | 函数式接口中被实现方法的全部参数传给 该构造器作为参数        | (a, b,...) ->new 类名 (a, b,...)        |

```java

import javax.swing.*;

@FunctionalInterface
interface Converter {
	Integer convert(String from);
}
@FunctionalInterface
interface MyTest {
	String test(String a , int b , int c);
}
@FunctionalInterface
interface YourTest {
	JFrame win(String title);
}
public class MethodRefer {
	public static void main(String[] args) {
		// 下面代码使用Lambda表达式创建Converter对象
		Converter converter1 = from -> Integer.valueOf(from);
		// 方法引用代替Lambda表达式：引用类方法。
		// 函数式接口中被实现方法的全部参数传给该类方法作为参数。
		Converter converter1 = Integer::valueOf;
		Integer val = converter1.convert("99");
		System.out.println(val); // 输出整数99

		// 下面代码使用Lambda表达式创建Converter对象
		Converter converter2 = from -> "fkit.org".indexOf(from);
		// 方法引用代替Lambda表达式：引用特定对象的实例方法。
		// 函数式接口中被实现方法的全部参数传给该方法作为参数。
		Converter converter2 = "fkit.org"::indexOf;
		Integer value = converter2.convert("it");
		System.out.println(value); // 输出2

		// 下面代码使用Lambda表达式创建MyTest对象
		MyTest mt = (a , b , c) -> a.substring(b , c);
		// 方法引用代替Lambda表达式：引用某类对象的实例方法。
		// 函数式接口中被实现方法的第一个参数作为调用者，
		// 后面的参数全部传给该方法作为参数。
		MyTest mt = String::substring;
		String str = mt.test("Java I Love you" , 2 , 9);
		System.out.println(str); // 输出:va I Lo

		// 下面代码使用Lambda表达式创建YourTest对象
		YourTest yt = (String a) -> new JFrame(a);
		// 构造器引用代替Lambda表达式。
		// 函数式接口中被实现方法的全部参数传给该构造器作为参数。
		YourTest yt = JFrame::new;
		JFrame jf = yt.win("我的窗口");
		System.out.println(jf);
	}
}
```

#### 1.5.9.4 Lambda 表达式与匿名内部类的联系和区别

> Lambda 表达式与匿名 内 部类存在如下相同点：
>
> 1. Lambda 表达式与匿名内部类一样 ， 都可以直接访问 "effectively final" 的局部变量，以及外部 类的成员变量(包括实例变量和类变量〉 。 
> 2. Lambda 表达式创建的对象与匿名内部类生成的对象一样 ， 都可 以直接调用从接口中继承的默认方法 。

> Lambda 表达式与匿名内部类主要存在如下区别：
>
> 1. 匿名内部类可以为任意接口创建实例一一不管接口包含多少个抽象方法，只要匿名内部类实现 所有的抽象方法即可;但 Lambda 表达式只能为函数式接口创建实例 。
> 2. 匿名内部类可以为抽象类甚至普通类创建实例;但 Lambda 表达式只能为函数式接口创建实例 。
> 3. 匿名内部类实现的抽象方法的方法体允许调用接口中定义的默认方法；但 Lambda 表达式的代 码块不允许调用接口中定义的默认方法 。

#### 1.5.9.5 使用 Lambda 表达式调用 Arrays 的类方法

> Arrays 类的有些方法需要 Comparator 、XxxOperator 、XxxFunction 等接口的实例，这些接口都是函数式接口，因此可以使用 Lambda 表达式来调用 Arrays 的方法 。
>

```java
import java.util.Arrays;

public class LambdaArrays
{
	public static void main(String[] args)
	{
		String[] arr1 = new String[]{"java" , "fkava" , "fkit", "ios" , "android"};
		Arrays.parallelSort(arr1, (o1, o2) -> o1.length() - o2.length());
		System.out.println(Arrays.toString(arr1));
		int[] arr2 = new int[]{3, -4 , 25, 16, 30, 18};
		// left代表数组中前一个所索引处的元素，计算第一个元素时，left为1
		// right代表数组中当前索引处的元素
		Arrays.parallelPrefix(arr2, (left, right)-> left * right);
		System.out.println(Arrays.toString(arr2));
		long[] arr3 = new long[5];
		// operand代表正在计算的元素索引
		Arrays.parallelSetAll(arr3 , operand -> operand * 5);
		System.out.println(Arrays.toString(arr3));
	}
}
```

### 1.5.10 枚举类

> 一个类的对象是有限而且固定的，比如季节类，它只有 4 个对象:再比如行星类 ， 这种实例有限而且固定的类，在 Java 里被称为枚举类 。
>

#### 1.5.10.1 枚举类入门

> 枚举类与普通类有如下简单区别：
>
> 1. 枚举类可以实现一个或多个接口，使用 enum 定义的枚举类默认继承了 java.lang.Enum 类，而不 是默认继承 Object 类，因此**枚举类不能显式继承其他父类。**其中 java.lang.Enum 类实现了 java.1ang.Serializable 和 java.lang. Comparable 两个接口。
> 2. 使用 enum 定义、非抽象的枚举类默认会使用 final 修饰， 因此**枚举类不能派生子类。**
> 3. **枚举类的构造器只能使用 private 访问控制符**，如果省略了构造器的访问控制符，则默认使用 private 修饰 ;如果强制指定访 问 控制符 ，则 只能指定 private 修饰符 。
> 4. **枚举类的所有实例必须在枚举类的第一行显式列出**，否则这个枚举类永远都不能产生实例 。 列出这些实例时，系统会自动添加 public static final 修饰，无须程序员显式添加。
>
> 枚举类默认提供了 一个 **value()** 方法，该方法可以很方便地遍历所有的枚举值。

> 所有的枚举类都继承了 java.lang.Enum 类，所以枚举类可以直接使用 java.lang.Enum 类中所包含的方法 。 java. lang.Enum 类 中 提供了如下几个方法 。 
>
> 1. int compareTo(E 0) : 该方法用于与指定枚举对象比较顺序 ，同 一个枚举实例只能与相同类型的枚举实例进行比较。 如果该枚举对象位于指定枚举对象之后， 则返回正整数; 如果该枚举对象位于指定枚举对象之前，则返回负整数，否则返回零。 
> 2. String name(): 返回此枚举实例的名称，这个名称就是定义枚举类时列出的所有枚举值之一。 与此方法相比，大多数程序员应该优先考虑使用 toString() 方法 ， 因为 toString() 方法返回更加用户友好的名称。
> 3. int ordinal(): 返回枚举值在枚举类中的索引值 (就是枚举值在枚举声明中的位置， 第一个枚举值的索引值为零) 。 
> 4. String toString() : 返回枚举常量的名称，与 name 方法相似，但 toString() 方法更常用 。 
> 5. public static <T extends Enum<T>> T valueOf(Class<T> enumType , String name) : 这是一个静态方法，用于返回指定枚举类中指定名称的枚举值 。名称必须与在该枚举类中 声 明枚举值时所用的标识符完全匹配 ， 不允许使用额外的 空 白 字符 。

#### 1.5.10.2 枚举类的成员变量、方法和构造器

> 枚举类也是一种类，只是它是一种比较特殊的类 ，因此它一样可以定义成员变量、方法和构造器 。
>
> 枚举类通常应该设计成不可变类，也就是说，它的成员变量值不应该允许改变，这样会更安全，而且代码更加简洁。 因此建议将枚举类的成员变量都使用 private final 修饰。
>

```java
public enum Gender {
	// 此处的枚举值必须调用对应构造器来创建
	MALE("男"),FEMALE("女");
	private final String name;
	// 枚举类的构造器只能使用private修饰
	private Gender(String name) {
		this.name = name;
	}
	public String getName() {
		return this.name;
	}
}
```

#### 1.5.10.3 实现接口的枚举类

> 枚举类也可以实现一个或多个接口 。与普通类实现一个或多个接口完全一样 ， 枚举类实现一个或多个接口时，也需要实现该接口所包含的方法。
>

> 如果由枚举类来实现接口里的方法，则每个枚举值在调用该方法时都有相同的行为方式(因为方法 体完全一样) 。 如果需要每个枚举值在调用该方法时呈现出不同的行为方式，则可以**让每个枚举值分别来实现该方法，每个枚举值提供不同的实现方式，从而让不同的枚举值调用该方法时具有不同的行为方式。**
>

```java
public enum Gender implements GenderDesc {
	// 此处的枚举值必须调用对应构造器来创建
	MALE("男")
	// 花括号部分实际上是一个类体部分
	{
		public void info()
		{
			System.out.println("这个枚举值代表男性");
		}
	},
	FEMALE("女")
	{
		public void info()
		{
			System.out.println("这个枚举值代表女性");
		}
	};
	// 其他部分与codes\06\6.9\best\Gender.java中的Gender类完全相同
	private final String name;
	// 枚举类的构造器只能使用private修饰
	private Gender(String name)
	{
		this.name = name;
	}
	public String getName()
	{
		return this.name;
	}
	// 增加下面的info()方法，实现GenderDesc接口必须实现的方法
	public void info()
	{
		System.out.println(
			"这是一个用于用于定义性别的枚举类");
	}
}
```

#### 1.5.10.4 包含抽象方法的枚举类

> 枚举类里定义抽象方法时不能使用 abstract 关键宇将枚举类定义成抽象类(因为系统自动会为它添加 abstract 关键字)，但因为枚举类需要显式创建枚举值，而不是作为父类，所以定义**每个枚举值时必须为抽象方法提供实现**，否则将出现编译错误 。

```java
public enum Operation {
	PLUS
	{
		public double eval(double x , double y)
		{
			return x + y;
		}
	},
	MINUS
	{
		public double eval(double x , double y)
		{
			return x - y;
		}
	},
	TIMES
	{
		public double eval(double x , double y)
		{
			return x * y;
		}
	},
	DIVIDE
	{
		public double eval(double x , double y)
		{
			return x / y;
		}
	};
	// 为枚举类定义一个抽象方法
	// 这个抽象方法由不同的枚举值提供不同的实现
	public abstract double eval(double x, double y);
	public static void main(String[] args)
	{
		System.out.println(Operation.PLUS.eval(3, 4));
		System.out.println(Operation.MINUS.eval(5, 4));
		System.out.println(Operation.TIMES.eval(5, 4));
		System.out.println(Operation.DIVIDE.eval(5, 4));
	}
}
```

### 1.5.11 对象与垃圾回收

> 垃圾回收机制具有如下特征：
>
> 1. 垃圾回收机制只负责回收堆内存中的对象，不会回收任何物理资源(例如数据库连接、网络 IO 等资源) 。
> 2. 程序无法精确控制垃圾回收的运行，垃圾回收会在合适的时候进行。当对象永久性地失去引用后，系统就会在合适的时候回收它所占的内存 。
> 3. 在垃圾回收机制回收任何对象之前，总会先调用它的 finalize() 方法，该方法可能使该对象重新复活(让一个引用变量重新引用该对象) ，从而导致垃圾回收机制取消回收。

#### 1.5.11.1 对象在内存中的状态

> 当 一个对象在堆内存中运行时，根据它被引用变量所引用的状态，可以把它所处的状态分成如下**三种**。
>
> 1. 可达状态 : 当 一个对象被创建后，若有一个以上的引用变量引用它，则这个对象在程序中处于 可达状态，程序可通过引用变量来调用该对象的实例变量和方法。 
> 2. 可恢复状态：如果程序中某个对象不再有任何引用变量引用它 ，它就进入了可恢复状态。在这种状态下，系统的垃圾回收机制准备回收该对象所占用的内存，在回收该对象之前，系统会调用所有可恢复状态对象的 finalize() 方法进行资源清理 。 如果系统在调用 finalize() 方法时重新让 一个引用变量引用该对象，则这个对象会再次变为可达状态;否则该对象将进入不可达状态。 
> 3. 不可达状态：当对象与所有引用变量的关联都被切断，且系统已经调用所有对象的 finalize() 方法后依然没有使该对象变成可达状态，那么这个对象将永久性地失去引用，最后变成不可达状态。只有当 一个对象处于不可达状态时，系统才会真正回收该对象所占有的资源。

![Java-Learning-Notes-Picture-3](/Users/lotus/Notes/Java-Learning-Notes/Java-Learning-Notes-Picture-3.png)

#### 1.5.11.2 强制垃圾回收

> 当 一个对象失去引用后，系统何时调用它的 finalize() 方法对它进行资源清理，何时它会变成不可达 状态，系统何时回收它所占有的内存，对于程序完全透明 。
>
> 程序无法精确控制 Java 垃圾回收的 时机 ，但依然可以强制系统进行垃圾回收一一这种 强制只是通 知系统进行垃圾回收，但系统是否进行垃圾回收依然不确定 。 大部分时候，程序强制系 统垃圾回 收后总 会有一些效果 。 强制系统垃圾回收有如下两种方式 。
>
> 1. 调用 System 类的 gc() 静态方法: System.gc()。 
> 2. 调用 Runtime 对象的 gc() 实例方法: Runtime.getRuntimeO.gc()。

> 运行 Java 命令时指定-verbose:gc 选项，可以看到 每次垃坡回收后的提示信息

#### 1.5.11.3 finalize 方法

> 在垃圾回收机制回收某个对象所占用的内存之前，通常要求程序调用适当的方法来清理资源 ， 在没有明确指定清理资源的情况下， Java 提供了默认机制来清理该对象的资源 ， 这个机制就是 finalizeO方法。 该方法是定义在 Object 类里的实例方法，方法原型为 :
>
> protected void finalize() throws Throwable
>
> 当 finalize() 方法返回后，对象消失，垃圾回收机制开始执行。方法原型中 的 throws Throwable 表示 它可以抛出任何类型的异常。
>
> 任何 Java 类都可以重写 Object 类的 finalizeO方法，在该方法中清理该对象占用的资源 。 如果程序 终止之前始终没有进行垃圾回收 ，则 不会调用失去引用对象的 finalizeO方法来清理资源。垃圾回 收机制 何时调用对象的 finalizeO方法是完全透明的，只有当程序认为需要更多的额外内存时，垃圾回收机制才 会进行垃圾回收 。 因此，完全有可能出现这样一种情形:某个失去引用的对象只占用了少量内存，而且 系统没有产生严重的内存需求，因此垃圾回收机制并没有试图回收该对象所占用的资源，所以该对象的 自nalizeO方法也不会得到调用。
>
> finalize() 方法具有如下 4 个特 点。
>
> 1. 永远不要主动调用某个对象的 finalize() 方法，该方法应交给垃圾回收机制调用 。
> 2. finalize() 方法何时被调用，是否被调用具有不确定性，不要把 finalize() 方法当成一定会被执行的方法 。
> 3. 当 JVM 执行可恢复对象的 finalize() 方法时，可能使该对象或系统中其他对象重新变成可达状态。 
> 4. 当 JVM 执行 finalize() 方法时出现异常时，垃圾回收机制不会报告异常，程序继续执行 。
>
> **由于 finalizeO方法并不一定会被执行，因此如果想清理某个类里打开的资源，则不要放在 finalize() 方法中进行清理。**

#### 1.5.11.4 对象的软、弱和虚引用

> Java 语言对对象的引用有如下 4 种方式：
>
> 1. 强引用 (StrongReference)
>    1. 这是 Java 程序中最常见的引用方式 。 程序创建一个对象，并把这个对象赋给一个引用变量 ，程序通过该引用变量来操作实际的对象，前面介绍的对象和数组都采用了这种强引用的方式 。 当一个对象被一个或一个以上的引用变量所引用时，它处于可达状态，不可能被系统垃圾回收机制回收 。
>
> 2. 软引用 (SoftReference)
>    1. 软引用需要通过 SoftReference 类来实现，当一个对象只有软引用时，它有可能被垃圾回收机制回收。 对于只有软引用的对象而言 ，当系统内存空间足够时，它不会被系统回收，程序也可使用该对象; 当系统内存空间不足时，系统可能会回收它。 软引用通常用于对内存敏感的程序中 。
>
> 3. 弱引用 (WeakReference)
>    1. 弱引用通过 WeakReference 类实现，弱引用和软引用很像，但弱引用的引用级别更低。 对于只有弱引用的对象而言 ，当系统垃圾回收机制运行时，不管系统内存是否足够，总会回收该对象所占用的内存 。 当然，并不是说当一个对象只有弱引用时，它就会立即被回收一一一正如那些失去引用的对象一样，必须**等到系统垃圾回收机制运行时才会被回收**。
>
> 4. 虚引用 (PhantomReference) 
>    1. 虚引用通过 PhantomReference 类实现，虚引用完全类似于没有引用 。 虚引用对对象本身没有太大影响，对象甚至感觉不到虚引用的存在。 如果一个对象只有一个虚引用时，那么它和没有引用的效果大致相同。 **虚引用主要用于跟踪对象被垃圾回收的状态，虚引用不能单独使用，虚引用必须和引用队列 ( ReferenceQueue ) 联合使用**。
>
> 引用队列由 java.lang.ref.ReferenceQueue 类表示，它用于保存被回收后对象的引用。当联合使用软引用、弱引用和引用队列时，系统在回收被引用的对象之后，将把被回收对象对应的引用添加到关联的 引用队列中 。与软引用和弱引用不同的是 ，虚引用在对象被释放之前，将把它对应的虚引用添加到它关 联的引用队列中，这使得可以在对象被回收之前采取行动 。
>
> 软引用和弱引用可以单独使用，但虚引用不能单独使用，单独使用虚引用没有太大的意义。虚引用 的主要作用就是跟踪对象被垃圾回收的状态，程序可以通过检查与虚引用关联的引用队列中是否已经包 含了该虚引用，从而了解虚引用所引用的对象是否即将被回收 。

### 1.5.12 修饰符的适用范围

|              | 外部类/接口 | 成员属性 | 方法 | 构造器 | 初始化块 | 成员内部类 | 局部成员 |
| ------------ | ----------- | -------- | ---- | ------ | -------- | ---------- | -------- |
| public       | True        | True     | True | True   |          | True       |          |
| protected    |             | True     | True | True   |          | True       |          |
| 包访问控制符 | True        | True     | True | True   | neutral  | True       | neutral  |
| private      |             | True     | True | True   |          | True       |          |
| abstract     | True        |          | True |        |          | True       |          |
| final        | True        | True     | True |        |          | True       | True     |
| statlc       |             | True     | True |        | True     | True       |          |
| strictfp     | True        |          | True |        |          | True       |          |
| synchronized |             |          | True |        |          |            |          |
| native       |             |          | True |        |          |            |          |
| transient    |             | True     |      |        |          |            |          |
| Volatile     |             | True     |      |        |          |            |          |
| default      |             |          | True |        |          |            |          |

> strictfp 关键宇的含义是 FP-strict ，也就是精确浮点的意思。 在 Java 虚拟机进行浮点运算时 ， 如果没有指定 stnct年关键宇， Java 的编译器和运行时环境在浮点运算上不一定令人满意 。一旦使用了 strictf挣 来 修饰类、接口或者方法时，那么在所修饰的范围内 Java 的编译器和运行时环境会完全依照浮点规范 IEEE-754 来执行 。 因此，如果想让浮点运算更加精确，就可以使用 strictfp 关键字来修饰类、接口和方法。
>
> native 关键宇主要用于修饰一个方法，使用 native 修饰的方法类似于一个抽象方法 。 与抽象方法不 同的是， native 方法通常采用 C 语言来实现。如果某个方法需要利用平台相关特性，或者访问系统硬件 等，则可以使用 native 修饰该方法，再把该方法交给 C 去实现 。一旦 Java 程序中包含了 native 方法， 这个程序将失去跨平台的功能 。

# 2. Java 基础类库

> Java 程序在不同操作系统上运行时，可能需要取得平台相关的属性，或者调用平台命令来完成特定 功能。 Java 提供了 System 类和 Runtime 类来与程序的运行平台进行交互。

## 2.1 系统相关

### 2.1.1 System 类

> System 类代表当前 Java 程序的运行平台，程序不能创建 System 类的对象， System 类提供了 一些类变量和类方法，允许直接通过 System 类来调用这些类变量和类方法。System 类的 getenvO 、 getPropertiesO 、 getPropertyO等方法来访问程序所在平台 的环境变量和系统属性，程序运行的结果会输出操作系统所有的环境变量值，并输出 JAVA HOME 环 境变量，以及 oS.name 系统属性的值.
>
> System 类提供了代表标准输入、标准输出和错误输出的类变量 ，并提供了 一些静态方法用于访问 环境变量 、系统属性的方法，还提供了加载文件和动态链接库的方法 。

> 加载文件和动态链接库主要对 natIve 方法有用，对于一些特殊的功能(如访问操作系统底层硬件设备等) Java 程序无法实现，必须借助 C 语言来完成，此时需要使用 C 语言为 Java 方法提供实现。其实现步骤如下:
>
> 1. Java 程序中声明 native 修饰的方法，类似于 abstract 方法，只有方法签名，没有实现。编译该 Java 程序，生成一个 class 文件 。 
> 2. 用 javah 编译第 1 步生成的 class 文件，将产生一个 .h 文件 。 
> 3. 写一个.cpp 文件实现 native 方法，这一步需要包含第 2 步产生的 .h 文件(这个 .h 文件中又包含了 JDK 带的 jni.h 文件)。 
> 4. 将第 3 步的 .cpp 文件编译成动态链接库文件 。 
> 5. 在 Java 中用 System 类的 loadLibrary..() 方法或 Runtime 类的 loadLibrary() 方法加载第 4 步产生的动态链接库文件， Java 程序中就可以调用这个 native 方法了 。

> System 类还有两个获取系统当前时间的方法 : currentTimeMillisO和 nanoTimeO ，它们都返回一个 long 型整数 。实 际上它们都返回 当前时间与 UTC 1970 年 l 月 1 日午夜的时间差，前者以毫秒作为单位， 后者以纳秒作为单位 。 必须指出的是，这两个方法返回的时间粒度取决于底层操作系统 ，可能所在的操 作系统根本不 支持以毫秒 、 纳秒作为计时单位 。

> **System 类还提供了 一个 identityHashCode(Object x)方法**， 该方法返回指定对象的精确 hashCode 值 ， 也就是根据该对象的地址计算得到的 hashCode 值 。 当某个类的 hashCodeO方法被重写后，该类实例的 hashCodeO方法就不能唯一地标识该对象 : 但通过 identityHashCodeO方法返回的 hashCode 值，依然是 根据该对象的地址计算得到的 hashCode 值。所以，如果两个对象的 identityHashCode 值相同 ，则 两个 对象绝对是同 一个对象 。

### 2.1.2 Runtime 类与 Java 9 的 ProcessHandle

> Runtime 类代表 Java 程序的运行时环境，每个 Java 程序都有 一个与之对应的 Runtime 实例，应用 程序通过该对象与其运行时环境相连。应用程序不能创建自己的 Runtime 实例，但可以通过 getRuntimeO 方法获取与之关联的 Runtime 对象。
>
> 与 System 类似的是， Runtime 类也提供了 gcO方法和 runFinalizationO 方法来通知系统进行垃圾回收、 清理系统资源，并提供了 load(String filename)和 loadLibrary(String libname)方法来加载文件和动态链接库。
>
> Runtime 类代表 Java 程序的运行时环境，可以访问阿M 的相关信息，如处理器数量、内存信息等。

> 通过 exec 启动平台上的命令之后，它就变成了 一个进程， Java 使用 Process 来代表进程 。 **Java 9 还 新增了一个 ProcessHandle 接口，通过该接口可获取进程的 ID、父进程和后代进程;通过该接口的 onExitO 方法可在进程结束时完成某些行为。**

```java
public class ExecTest
{
	public static void main(String[] args)
		throws Exception
	{
		Runtime rt = Runtime.getRuntime();
		// 运行记事本程序
		rt.exec("notepad.exe");
	}
}
```

> **ProcessHandle 还提供了 一个 ProcessHandle.Info 类，用于获取进程的命令、参数、启动时间、累计 运行时间、用户等信息。**

```java
public class ProcessHandleTest
{
	public static void main(String[] args)
		throws Exception
	{
		Runtime rt = Runtime.getRuntime();
		// 运行记事本程序
		Process p = rt.exec("notepad.exe");
		ProcessHandle ph = p.toHandle();
		System.out.println("进程是否运行: " + ph.isAlive());
		System.out.println("进程ID: " + ph.pid());
		System.out.println("父进程: " + ph.parent());
		// 获取ProcessHandle.Info信息
		ProcessHandle.Info info = ph.info();
		// 通过ProcessHandle.Info信息获取进程相关信息
		System.out.println("进程命令: " + info.command());
		System.out.println("进程参数: " + info.arguments());
		System.out.println("进程启动时间: " + info.startInstant());
		System.out.println("进程累计运行时间: " + info.totalCpuDuration());
		// 通过CompletableFuture在进程结束时运行某个任务
		CompletableFuture<ProcessHandle> cf = ph.onExit();
		cf.thenRunAsync(()->{
			System.out.println("程序退出");
		});
		Thread.sleep(5000);
	}
}
```

## 2.2 常用类

### 2.2.1 Object 类

> Object 类是所有类、数组、枚举类的父类，也就是说， Java 允许把任何类型的对象赋给 Object 类 型的变量 。当 定义一个类时没有使用 extends 关键字为它显式指定父类，则该类默认继承 Object 父类。
>
> Object 类提供了如下几个常用方法 。 
>
> 1. boolean equals(Object obj): 判断指定对象与该对象是否相等。此处相等的标准是，两个对象是 同一个对象，因此该 equalsO方法通常没有太大的实用价值 。 
> 2. protected void fmalizeO: 当系统中没有引用变量引用到该对象时，垃圾回收器调用此方法来清理 该对象的资源 。 
> 3. Class<? > getClassO: 返回该对象的运行时类；
> 4. int hashCodeO: 返回该对象的 hashCode 值 。 在默认情况下， Object 类的 hashCodeO方法根据该 对象的地址来计算(即与 System.identityHashCode(Object x)方法的计算结果相同) 。 但很多类都重写了 Object 类的 hashCodeO方法，不再根据地址来计算其 hashCodeO方法值 。 
> 5. String toStringO: 返回该对象的字符串表示，当程序使用 System.out.printlnO方法输出 一个对象， 或者把某个对象和字符串进行连接运算时，系统会自动调用该对象的 toStringO方法返回该对象 的字符串表示 。 Object 类的 toStringO方法返回"运行时类名@十六进制 hashCode 值"格式的字 符串，但很多类都重写了 Object 类的 toStringO方法，用于返回可以表述该对象信息的字符串 。
> 6. **Object 类还提供了 waitO 、 notify()、 notifyAllO几个方法，通过这几个方法可以控制线程 的暂停和运行。**

> **Java 还提供了一个 protected 修饰的 clone() 方法，该方法用于帮助其他对象来实现"自我克隆"，所谓"自我克隆"就是得到一个当前对象的副本，而且二者之间完全隔离 。 由于 Object 类提供的 clone() 方法使用了 protected 修饰，因此该方法只能被子类重写或调用。**
>
> 自定义类实现"克隆"的步骤如下 。
>
> 1. 自定义类实现 Cloneable 接口。这是一个标记性的接口，实现该接口的对象可以实现"自我克 隆"，接口里没有定义任何方法 。 
> 2. 自定义类实现自己的 clone() 方法 。
> 3. 实现 cloneO方法时通过 super.clone() ;调用 Object 实现的 clone()方法来得到该对象的副本，并返回该副本。

```java
class Address
{
	String detail;
	public Address(String detail)
	{
		this.detail = detail;
	}
}
// 实现Cloneable接口
class User implements Cloneable
{
	int age;
	Address address;
	public User(int age)
	{
		this.age = age;
		address = new Address("广州天河");
	}
	// 通过调用super.clone()来实现clone()方法
	public User clone()
		throws CloneNotSupportedException
	{
		return (User)super.clone();
	}
}
public class CloneTest
{
	public static void main(String[] args)
		throws CloneNotSupportedException
	{
		User u1 = new User(29);
		// clone得到u1对象的副本。
		User u2 = u1.clone();
		// 判断u1、u2是否相同
		System.out.println(u1 == u2);      //①
		// 判断u1、u2的address是否相同
		System.out.println(u1.address == u2.address);     //②
	}
}
```

### 2.2.2 Java 7 新增的 Objects 类

> Java 7 新增了 一个 Objects 工具类 ， 它提供了 一些工具方法来操作对象，这些工具方法大多是"空 指针"安全的。 比如你不能确定一个引用变量是否为 null，如果贸然地调用该变量 的 toStringO方法 ，则 可能引发 NullPointerExcetpion 异常 ; 但如果使用 Objects 类提供的 toString(Object 0)方法 ， 就不会引发 空指针异常，当 o 为 null 时，程序将返回 一个"null" 字符串。

```java
public class ObjectsTest {
	//定义一个 obj 变量，它 的默认值是 null

	static ObjectsTest obj; 
	public static void main(String[] args) {
		// 输出 一个 null 对象的 hashCode 值，输出 O
		System.out.println(Objects.hashCode(obj));
		// 输出 一个 null 对象的 toStr ing，输出 null
		System.out.println(Objects.toString(obj));
		// 要求 obj 不能为 null ，如果 obj 为 null 则引发异常
		System.out.println(Objects.requireNonNull(obj, "obj 参数不能是 null ! ")) ;
	}
}
```

### 2.2.3 Java 9 改进的 String 、 StringBuffer 和 StringBuilder 类

> 字符串就是一连串的字符序列， Java 提供 了 String、 StringBuffer 和 StringBuilder 三个类来封装宇符串，并提供了一系列方法来操作字符串对象。**它们都实现了 CharSequence 接口，CharSequence 可以认为是一个字符串的协议接口。**
>
> String 类是不可变类 ，即 一旦一个 String 对象被创建以后，包含在这个对象中的字符序列是不可改 变的 ， 直至这个对象被销毁。
>
> StringBuffer 对象则代表一个字符序列可变的字符串 ，当一个 StringBuffer 被创建以后，通过 StringBuffer 提供的 appendO 、 insertO 、 reverseO 、 setCharAtO 、 setLengthO等方法可以改变这个字符串对 象的宇符序列。 一旦通过 StringBuffer 生成了 最终想要的字符串，就可以调用它的 toStringO方法将其转 换为一个 String 对象 。
>
> StringBuilder 类是 JDK 1.5 新增的类 ， 它 也代表可变字符串对象 。 实际上， StringBuilder 和 StringBuffer 基本相似，两个类的构造器和方法也基本相同。不同的是，**StringBuffer 是线程安全的，而 StringBuilder 则没有实现线程安全功能 ，所以性能略高。因此在通常情况下，如果需要创建一个内容可变的字符串对象， 则应该优先考虑使用 StringBuilder 类。**

> Java 9 改进了字符串( 包括 String、 StringBuffer、 StringBuilder) 的实现 。 **在 Java 9 以前字符串采用 char[] 数组来保存字符 ，因此字符串 的每个字符占 2 字节；而 Java 9 的字符串采用 byte[]数组再加一个 encoding-flag 宇段来保存字符 ，因此字符串 的每个字符只占 1 宇节。所以 Java 9 的字符串更加节省空间，但字符串的功能方法没有受到任何影响。**

> String 类提供了大量构造器来**创建 String 对象**：
>
> 1. StringO: 创建一个包含 0 个宇符串序列的 String 对象(并不是返回 null ) 。 
> 2. String(byte[] bytes, Charset charset): 使用指定的字符集将指定的 byte[]数组解码成一个新的 String 对象 。
> 3. String(byte[] bytes, int offset, int length): 使用平台的默认字符集将指定的 byte[]数组从 offset 开始、长度为 length 的子数组解码成一个新的 String 对象。
> 4. String(byte[] bytes, int offset, int length, String charsetName): 使用指定的字符集将指定的 byte[]数 组从 offset 开始、长度为 length 的子数组解码成一个新的 String 对象 。 
> 5. String(byte[] bytes, String charsetName): 使用指定的字符集将指定的 byte[]数组解码成一个新的 String 对象。
> 6. String(char[] value, int offset, int count): 将指定的宇符数组从 offset 开始、长度为 count 的字符元素连缀成字符串。 
> 7. String(String original): 根据宇符串直接量来创建一个 String 对象 。也就是说，新创建的 String 对象是该参数字符串 的副本。 
> 8. String(StringBuffer buffer): 根据 StringBuffer 对象来创建对应的 String 对象。 
> 9. String(StringBuilder builder): 根据 StringBuilder 对象来创建对应的 String 对象。 

> String 类也提供了大量方法来**操作字符串对象**， 下面详细介绍这些常用方法。 
>
> 1. char charAt(int index): 获取字符串中指定位置的字符。其中 ， 参数 index 指 的是字符串的序数，字符串的序数从 0 开始到 length() - 1。
> 2. int compareTo(String anotherString)：比较两个宇符串的大小 。 如果两个字符串的字符序列相等， 则返回 0 ; 不相等时 ，从两个字符串第 0 个字符开始比较 ， 返回第一个不相等的字符差 。 另 一 种情况，较长字符串的前面部分恰巧是较短的字符串，则返回它们的长度差。
> 3. String concat(String s的:将该 String 对象与由连接在一起。 与 Java 提供的字符串连接运算符" +" 的功能相同 。 
> 4. boolean contentEquals(StringBuffer sb): 将该 String 对象与 StringBuffer 对象 sb 进行比较，当它们包含的字符序列相同时返回 true。 
> 5. static String copyValueOf(char[] data)：将字符数组连缀成字符串，与 String( char[] content)构造器的功能相同 。
> 6. static String copyValueOf(char[] data, int offset, int count): 将 char 数组的子数组中的元素连缀成字符串，与 String( char[] value, int offset, int count)构造器的功能相同 。
> 7. boolean endsWith(String suffix)：返回该 String 对象是否以 suffix 结尾 。
> 8. boolean equals(Object anObject)：将该字符串与指定对象比较，如果二者包含的字符序列相等，则返回 true；否则返回 false 。
> 9. boolean equalsIgnoreCase(String s的:与前一个方法基本相似，只是忽略字符的大小写 。 
> 10. byte[] getBytesO: 将该 String 对象转换成 byte 数组 。 
> 11. void getChars(int srcBegin, int srcEnd, char[] dst, int dstBegin): 该方法将字符串中从 srcBegin 开始，到 srcEnd 结束的字符复制到 dst 字符数组中，其中 dstBegin 为目标字符数组的起始复制位置 。
> 12. int indexOf(int ch): 找出 ch 字符在该字符串中第一次出现的位置 。 
> 13. int indexOf(int ch, int 仕omIndex): 找出 ch 字符在该字符串中从企omIndex 开始后第一次出现的位置。 
> 14. int indexOf(String str:找出 s位子字符串在该宇符串中第一次出现的位置 。 
> 15. int indexOf(String str， int fromIndex): 找出 s位 子字符串在该字符串中从 fromIndex 开始后第一次出现的位置。
> 16. int lastIndexOf(int ch): 找出 ch 字符在该字符串中最后一次出现的位置。 
> 17. int lastIndexOf(int ch , int fromIndex): 找出 ch 字符在该字符串 中从 fromIndex 开始后最后一次出 现的位置 。 
> 18. int lastIndexOf(String str): 找出 str 子字符串在 该字符串中最后一次出现的位置。
> 19. int lastIndexOf(String str， int fromIndex): 找出 str 子字符串在该字符串中从 fromlndex 开始后最后一次出现的位置 。
> 20. int length(): 返回当前字符串长度。
> 21. String replace(char oldChar, char newChar): 将字符串中的第一个 oldChar 替换成 newChar。
> 22. boolean startsWith(String prefix): 该 String 对象是否以 prefix 开始。
> 23. boolean startsWith(String prefix， int toffset): 该 String 对象从 toffset 位置算起，是否以 prefix 开始。
> 24. String substring(int beginlndex): 获取从 beginlndex 位置开始到结束的子字符串。 
> 25. String substring(int beginlndex , int endIndex): 获取从 beginIndex 位置开始到 endlndex 位置的子字符串。
> 26. char[] toCharArrayO: 将该 String 对象转换成 char 数组。 
> 27. String toLowerCaseO: 将宇符串转换成小写。 
> 28. String toUpperCaseO: 将字符串转换成大写。
> 29. static String valueOf(X x): 一系列用于将基本类型值转换为 String 对象的方法 。
>

> **String 类是不可变的， String 的 实例 一旦生成就不会再改变了。因为 String 是不可变的，所以会额外产生很多临时变量，使用 StringBuffer 或 StringBuilder 就可以 避免这个问题。**
>
> StringBuilder 提供了 一 系列插入、追加、改变该字符串里包含 的 字符序 列的方法 。而 StringBuffer 与其用法完全相同，只是 StringBuffer 是线程安全的 。
>
> StringBuilder、 StringBuffer 有两个属性 : length 和 capacity ，其中 length 属性表示其包含的字符序列的长度。与 String 对象的 length 不同的是 ， StringBuilder、 StringBuffer 的 length 是可以改变的 ， 可以通过 lengthO、 setLength(int len) 方法来访问和修改其字符序列的长度。 Capacity 可属性表示 StringBuilder 的容量， capacity 通常比 length 大，程序通常无须关心 capacity 属性。

### 2.2.4 Java 7 的 ThreadLocalRandom 与 Random

> Random 类专门用于生成一个伪随机数，它有两个构造器: 一个构造器使用默认的种子(以当前时 间作为种子) ，另 一个构造器需要程序员显式传入一个 long 型整数的种子 。
>
> ThreadLocalRandom 类是 Java 7 新增的 一个类 ，它是 Random 的增强版 。 **在并发访问的环境下，使用 ThreadLocalRandom 来代替 Random 可以减少 多线程资源竞争，最终保证系统具有更好的线程安全性 。**
>
> ThreadLocalRandom 类的用法与 Random 类 的用法基本相似，它提供了 一个静态的 current() 方法来获取 ThreadLocalRandom 对象 ， 获取该对象之后 即可调用 各种 nextXxxO方法来获取伪随机数了 。
>
> ThreadLocalRandom 与 Random 都比 Math 的 random() 方法提供了更多的方式来生成各种伪随机数， 可以生成浮点类型的伪随机数，也可以生成整数类型的伪随机数，还可以指定生成随机数的范围 。
>
> **Random 使用一个 48 位的种子 ，如果这个类的两个实例是用同 一个种子创建的，对它们以同样的顺序调用方法，则它们会产生相同的数字序列 。** 为了避免两个 Random 对象产生相同的数字序列，通常推荐使用当前时间作为 Random 对象的种子. Random rand = new Random(System.currentTimeMillis());

## 2.3 日期、时间类

> Java 8 吸 取了 Joda-Time 库( 一个被广泛使用的日期、 时间库)的经验 ， 提供了一套全新的日期时间库 。

### 2.3.1 Date 类

> Date 对象既包含日期 ，也包含时间 。Date 类提供了 6 个构造器 ， 其中 4 个己经 Deprecated，剩下的两个构造器如下 。
>
> 1. DateO: 生成一个代表当前日期时间的 Date 对象 。 该构造器在底层调用 System.currentTimeMillisO 获得 long 整数作为日期参数。 
> 2. Date (l ong date): 根据指定的 long 型整数来生成一个 Date 对象 。该构造器的参数表示创建的 Date 对象和 GMT 1970 年 1 月 1 日 00:00:00 之间的时间 差 ，以毫秒作为计时单位 。
>
> Date 类从 JDK 1.0 起就开始存在了，但正因为它历史悠久，所以它的大部分构造器、方法都己经过时，不再推荐使用了。

### 2.3.2 Calendar 类

> 为了统一计时 ，全世界通常选择最 普及 、 最通用的日历 : Gregorian Calendar ，也就是日常介绍年份时 常用 的 "公元几几年 " 。
>
> Calendar 类是一个抽象类，所 以 不能使用构造器来创建 Calendar 对象 。 但它提供了 几 个静态 getInstanceO方法来获取 Calendar 对象，这些方法根据 TimeZone ， Locale 类来获取特定的 Calendar ，如 果不指定 TimeZone、 Locale ， 则使用默认 的 TimeZone 、 Locale 来创建 Calendar。

### 2.3.3 Java 8 新增的日期、时间包

> Java 8 开始专 门 新增了 一个 java.time 包 ，该包下包含了 如下常用的类 。
>
> 1. Clock: 该类用于获取指定时区的当前 日 期、 时 间 。该类可取代 System 类的 currentTimeMillisO 方法，而且提供了更多方法来获取当前日期、时间 。 该类提供了大量静态方法来获取 Clock 对 象。 
> 2. Duration: 该类代表持续时间 。 该类可 以非常方便地获取一段时间。
> 3. Instant: 代表一个具体的时刻 ，可以精确到纳秒。该类提供了静态 的 nowO方法来获取当前时刻， 也提供了静态的 now(Clock clock)方法来获取 clock 对应的时刻 。 除此之外，它还提供了 一系列 minusXxxO方法在当前时刻基础上减去一段时间 ， 也提供了 plusXxxO方法在当前时刻基础上加 上一段时间。
> 4. LocalDate : 该类代表不带时区的日期 ，例 如 2007-12-03 。该类提供了静态的 nowO方法来获取当前日期，也提供了静态的 now(Clock clock)方法来获取 clock 对应的日期 。除此之外 ， 它还提供了 minusXxxO方法在当前年份基础上减去几年、几月、几周或几日等，也提供了 plusXxxO 方法在当前年份基础上加上几年 、几月 、几周或几日 等。 
> 5. LocalTime: 该类代表不带时 区 的时间，例如 10:15 :30 。 该类提供了静态的 nowO方法来获取当 前 时间，也提供了静态的 now(Clock clock)方法来获取 clock 对应的时间 。 除此之外，它还提供 了 minusXxxO方法在当前年份基础上减去几小 时、几分、几秒等，也提供了 plusXxxO方法在当 前年份基础上加上几小 时 、 几分、 几秒等。 
> 6. LocalDateTime: 该类代表不带时区 的 日期 、 时间 ， 例如 2007-12-03Tl 0: 15 :30 。 该类提供了静态 的 nowO方法来获取当前日期、 时 间 ，也提供了静态的 now(Clock clock)方法来获取 clock 对应 的日期、 时 间 。 除此之外，它还提供了 minusXxxO方法在当前年份基础上减去几年、 几月 、几 日、几小时 、 几分、几秒等， 也提供了 plusXxxO方法在当前年份基础上加上几年、几月 、 几日 、 几小时 、 几分、 几秒等。
> 7. MonthDay: 该类仅代表月日 ，例如一04-12 。 该类提供了静态的 nowO方法来获取当前月日 ，也 提供了静态的 now(Clock clock)方法来获取 clock 对应的月日 。 
> 8. Year: 该类仅代表年，例如 2014 。 该类提供了静态的 nowO方法来获取当前年份 ，也提供了静 态的 now(Clock clock)方法来获取 clock 对应的年份 。 除此之外，它还提供了 minusYearsO方法 在当前年份基础上减去几年 ，也提供了 plusYearsO方法在当前年份基础上加上几年 。 
> 9. YearMonth: 该类仅代表年月 ， 例如 2014-04 。该类提供了静态的 nowO方法来获取当前年月， 也 提供了静态的 now(Clock clock)方法来获取 clock 对应的年月 。 除此之外，它还提 供 了 minusXxxO方法在当前年月基础上减去几年 、几月 ，也提供了 plusXxxO方法在当前年月基础上加上几年、几月 。
> 10. ZonedDateTime : 该类代表一个时 区化 的日期 、时 间 。 
> 11. Zoneld: 该类代表一个时区 。 
> 12. DayOtweek: 这是一个枚举类 ， 定义 了周日到周六的枚举值 。 
> 13. Month: 这也是一个枚举类 ， 定义了 一月到十二月的枚举值 。

```java

import java.time.*;

public class NewDatePackageTest
{
	public static void main(String[] args)
	{
		// -----下面是关于Clock的用法-----
		// 获取当前Clock
		Clock clock = Clock.systemUTC();
		// 通过Clock获取当前时刻
		System.out.println("当前时刻为：" + clock.instant());
		// 获取clock对应的毫秒数，与System.currentTimeMillis()输出相同
		System.out.println(clock.millis());
		System.out.println(System.currentTimeMillis());
		// -----下面是关于Duration的用法-----
		Duration d = Duration.ofSeconds(6000);
		System.out.println("6000秒相当于" + d.toMinutes() + "分");
		System.out.println("6000秒相当于" + d.toHours() + "小时");
		System.out.println("6000秒相当于" + d.toDays() + "天");
		// 在clock基础上增加6000秒，返回新的Clock
		Clock clock2 = Clock.offset(clock, d);
		// 可看到clock2与clock1相差1小时40分
		System.out.println("当前时刻加6000秒为：" +clock2.instant());
		// -----下面是关于Instant的用法-----
		// 获取当前时间
		Instant instant = Instant.now();
		System.out.println(instant);
		// instant添加6000秒（即100分钟），返回新的Instant
		Instant instant2 = instant.plusSeconds(6000);
		System.out.println(instant2);
		// 根据字符串中解析Instant对象
		Instant instant3 = Instant.parse("2014-02-23T10:12:35.342Z");
		System.out.println(instant3);
		// 在instant3的基础上添加5小时4分钟
		Instant instant4 = instant3.plus(Duration
			.ofHours(5).plusMinutes(4));
		System.out.println(instant4);
		// 获取instant4的5天以前的时刻
		Instant instant5 = instant4.minus(Duration.ofDays(5));
		System.out.println(instant5);
		// -----下面是关于LocalDate的用法-----
		LocalDate localDate = LocalDate.now();
		System.out.println(localDate);
		// 获得2014年的第146天
		localDate = LocalDate.ofYearDay(2014, 146);
		System.out.println(localDate); // 2014-05-26
		// 设置为2014年5月21日
		localDate = LocalDate.of(2014, Month.MAY, 21);
		System.out.println(localDate); // 2014-05-21
		// -----下面是关于LocalTime的用法-----
		// 获取当前时间
		LocalTime localTime = LocalTime.now();
		// 设置为22点33分
		localTime = LocalTime.of(22, 33);
		System.out.println(localTime); // 22:33
		// 返回一天中的第5503秒
		localTime = LocalTime.ofSecondOfDay(5503);
		System.out.println(localTime); // 01:31:43
		// -----下面是关于localDateTime的用法-----
		// 获取当前日期、时间
		LocalDateTime localDateTime = LocalDateTime.now();
		// 当前日期、时间加上25小时３分钟
		LocalDateTime future = localDateTime.plusHours(25).plusMinutes(3);
		System.out.println("当前日期、时间的25小时3分之后：" + future);
		// 下面是关于Year、YearMonth、MonthDay的用法示例-----
		Year year = Year.now(); // 获取当前的年份
		System.out.println("当前年份：" + year); // 输出当前年份
		year = year.plusYears(5); // 当前年份再加5年
		System.out.println("当前年份再过5年：" + year);
		// 根据指定月份获取YearMonth
		YearMonth ym = year.atMonth(10);
		System.out.println("year年10月：" + ym); // 输出XXXX-10，XXXX代表当前年份
		// 当前年月再加5年，减3个月
		ym = ym.plusYears(5).minusMonths(3);
		System.out.println("year年10月再加5年、减3个月：" + ym);
		MonthDay md = MonthDay.now();
		System.out.println("当前月日：" + md); // 输出--XX-XX，代表几月几日
		// 设置为5月23日
		MonthDay md2 = md.with(Month.MAY).withDayOfMonth(23);
		System.out.println("5月23日为：" + md2); // 输出--05-23
	}
}
```



## 2.3 正则表达式

> 正则表达式是一个强大的字符串 处理工具 ，可以对字符串进行查找、提取、分割 、 替换等操作 。String 类里也提供了如下几个特殊的方法 。
>
> 1. boolean matches(String regex): 判断该宇符串是否匹配指定的正则表达式 。 
> 2. String replaceAll(String regex , String replacement): 将该宇符串中所有匹配 regex 的子串替换成 replacement。
> 3. String replaceFirst(String regex , String replacement): 将该字符串中第一个匹配 regex 的子串替换 成 replacement。 
> 4. String[] split(String regex): 以 regex 作为分隔符，把该字符串分割成多个子串 。 上面这些特殊的方法都依赖于 Java 提供的正则表达式支持，除此之外， Java 还提供了 Pattem 和 Matcher 两个类专门用于提供正则表达式支持。

### 2.3.1 创建正则表达式

#### 2.3.1.1 合法字符

> 正则表达式所支持的合法字符如表 7.1 所示 。

![Java-Learning-Notes-Picture-4](/Users/lotus/Notes/Java-Learning-Notes/Java-Learning-Notes-Picture-4.png)

#### 2.3.1.2 特殊字符

> 正则表达式中有一些**特殊字符**，这些特殊字符在正则表达式中有其特殊的用途。如果需要匹配这些特殊字符，就必须首先将这些宇符转义，也就是在前面添加一 个反斜线 （\）。正则表达式中的特殊字符如表 7.2 所示。

![Java-Learning-Notes-Picture-5](/Users/lotus/Notes/Java-Learning-Notes/Java-Learning-Notes-Picture-5.png)

#### 2.3.1.3 通配符

> **"通配符"** 是可以匹配多个字符 的特殊字符。正则表达式中 的"通配符"远远超出了普通通配符的功能，它被称为 预定义字符，正则 表达式支持如表 7.3 所示的预定义字符 。

![Java-Learning-Notes-Picture-6](/Users/lotus/Notes/Java-Learning-Notes/Java-Learning-Notes-Picture-6.png)

> 上面的 7 个预定义字符其 实很容易记忆一- d 是 digit 的 意思，代表数字；s 是 space 的 意思， 代表空白， W 是 word 的意思， 代表单词 。 d、 s、 w 的大写形式恰好匹配与之相反的字符 。
>

#### 2.3.1.4 方括号表达式

> 在一些特殊情况下，例如，若只想、 匹配 a~ f 的字母 ，或者匹配除 ab 之外的所有小 写字母，或者匹 配中文字符，上面这些预定义字符就无能为力了，此时就需要使用**方括号表达式**，方括号表达式有如表 7.4 所示的几种形式 。
>
> **匹配的是一个字符，除非后面添加了数量符号**

![Java-Learning-Notes-Picture-7](/Users/lotus/Notes/Java-Learning-Notes/Java-Learning-Notes-Picture-7.png)

> 方括号表达式比前面的预定义字符灵活多了，几乎可以匹配任何字符 。例如 ，若需要匹 配所有的 中文字符 ，就可以利用 [\\u0041-\\u0056]形式一一因为 所有中文字符的 Unicode 值是连续的 ， 只要找出所有 中文字符 中最小 、最大的 Unicode 值，就可以利用上面形式来匹配所有的中文字符。
>

#### 2.3.1.5 圆括号表达式

> 正则表示还支持圆括号表达式 ，用于将**多个表达式组成一个子表达式**，圆括号中可 以使用或运算符 (|)。 例如， 正则表达式 "((public )1(P rotected)l (p rivate ))" 用于匹配 Java 的三个访问控制符其中之一 。 除此之外， Java 正则表达式还支持如表 7.5 所示的几个边界匹配符 。
>

![Java-Learning-Notes-Picture-8](/Users/lotus/Notes/Java-Learning-Notes/Java-Learning-Notes-Picture-8.png)

#### 2.3.1.6 数量表示符

> 正则表达式还提供了数量标识符，正则表达式支持的数量标 识符有如下几种模式 。 
>
> 1. Greedy (贪婪模式):数量表示符默认采用贪婪模式，除非另有表示 。贪婪模式的表达式会一直 匹配下去， 直到无法匹配为止 。 如果你发现表达式匹配的结果与预期的不符 ， 很有可能是因为 一一你以为表达式只会匹配前面几个宇符，而实 际上它是贪婪模式，所以会一直 匹配下去 。
> 2. Reluctant (勉强模式):用问号后缀(?)表示，它只会匹配最少的字符。 也称为最小匹配模式 。 
> 3. Possessive (占有模式) : 用加号后缀(+)表示 ，目前只 有 Java 支持占有模式 ， 通常比较少用 。 三种模式的数量表示符如表 7.6 所示 。

![Java-Learning-Notes-Picture-9](/Users/lotus/Notes/Java-Learning-Notes/Java-Learning-Notes-Picture-9.png)

> 关于贪婪模式和勉强模式的对比 ，看如下代码 :
>
> Stri ng str = " hello , java !" ;
>
> // 贪婪模式的正则表达式
>
> System.out . println(str . replaceFirst( " \ \w*", " ." )) ; / / 输出 . , java!
>
> / /勉强模式的正则表达式
>
> System . out . pri n tl口 (str . replaceFirst( " \\w*? "，" ." ) ) ; //输出 . hello , java!
>

> 当从"hello ， java! " 字符串中查找匹配" \\w刷子串时，因为" \w*" 使用了贪婪模式 ， 数量表示符( * )会一直匹配 下去 ， 所以该字符串前面的所有单词字符都被它匹配到 ， 直到遇到空格，所 以 替换后的效果是 " ., java! " ; 如果使用勉强模式 ， 数量表示符(*)会尽量匹配最少字符， 即 匹配 0 个字符 ， 所 以 替换后 的结果是 " .hello ， java ! " 。
>

### 2.3.2 使用正则表达式

> 一旦在程序中定义了正则表达式，就可 以使用 Pattem 和 Matcher 来使用正则表达式 。 
>
> Pattem 对象是正则表达式编译后在 内 存中的表示形式，因此 ， 正则表达式宇符串 必须先被编译为 Pattem 对象 ， 然后再利用该 Pattem 对象创建对应的 Matcher 对象 。 执行匹配所涉及 的状态保留在 Matcher 对象中 ， 多个 Matcher 对象可共享同 一个 Pattem 对象 。
>
> 因此， 典型的调用顺序如下 :

```java
// 将一个字符串编译成 Pattern 对象 
Pattern p = Pattern .compil e( "a*b" ) ; // 使用 Pattern 对象创建 Matcher 对象
Matcher m = p .matcher( " aaaaab" ) ; 
boolean b = m.matches( ); // 返回 true
```

> 上面定义的 Pattem 对象可以多次重复使用 。如果某个正 则 表达式仅需一次使用，则可直接使用 Pattem 类的静态 matches() 方法，此方法自动把指定字符串编译成匿名的 Pattem 对象，并执行匹配，如下所示 。
>

```java
boolean b = Pattern .matches( " a*b" , " aaaaab" ); // 返回 true
```

> 上面语句等效于前面的三条语句 。 但采用这种语句每次都需要重新编译新的 Pattem 对象，不能重复利用己编译的 Pattem 对象 ， 所以效率不高 。
>
> **Pattem 是不可变类 ， 可供多个并发线程安全使用 。**
>
> Matcher 类提供了如下几个常用方法 。 
>
> 1. find(): 返回目标字符串中是否包含与 Pattem 匹配的子串 。 
> 2. group(): 返回上一次与 Pattem 匹配的子串 。 
> 3. start(): 返回上一 次与 Pattem 匹配的子串在目标字符串中的开始位置 。 
> 4. endO: 返回上一次与 Pattem 匹配的子串在目标字符串中的结束位置加 1 。 
> 5. lookingAtO : 返回目标字符串前面部分与 Pattem 是否匹配 。 
> 6. matchesO : 返回整个 目标字符串与 Pattem 是否匹配 。 
> 7. resetO: 将现有 的 Matcher 对象应用 于一个新的字符序列 。

> 在 Pattem、 Matcher 类 的 介绍中 经常会看到一个 CharSequence 接 口 ，该接 口代表一个字符序列，其 中 CharBuffer、 String、 StringBuffi町、 StringBuilder 都是它 的 实现类 。 简 单地说，CharSequence 代表一个各种表示形 式的字符串 。
>
> 通过 Matcher 类 的 find() 和 group() 方法可 以从目标字符串中依次取出特定子串(匹配正则 表达式 的 子串) ，例如互联网的网络爬虫， 它们可以自动从网页中识别出所有的电话号码 。 下面程序示范了如何从大段的宇符串中 找 出电话号码 。

```java
public class FindGroup
{
	public static void main(String[] args)
	{
		// 使用字符串模拟从网络上得到的网页源码
		String str = "我想求购一本《疯狂Java讲义》，尽快联系我13500006666"
			+ "交朋友，电话号码是13611125565"
			+ "出售二手电脑，联系方式15899903312";
		// 创建一个Pattern对象，并用它建立一个Matcher对象
		// 该正则表达式只抓取13X和15X段的手机号，
		// 实际要抓取哪些电话号码，只要修改正则表达式即可。
		Matcher m = Pattern.compile("((13\\d)|(15\\d))\\d{8}")
			.matcher(str);
		// 将所有符合正则表达式的子串（电话号码）全部输出
		while(m.find())
		{
			System.out.println(m.group());
		}
	}
}
```

> findO方法还可以传入一个 int 类型的参数，带 int 参数的 findO方法将从该 int 索引处向下搜索 。
>
> startO和 endO方法主要用于确定子串在目标字符串中的位置，如下程序所示。

```java
public class StartEnd
{
	public static void main(String[] args)
	{
		// 创建一个Pattern对象，并用它建立一个Matcher对象
		String regStr = "Java is very easy!";
		System.out.println("目标字符串是：" + regStr);
		Matcher m = Pattern.compile("\\w+")
			.matcher(regStr);
		while(m.find())
		{
			System.out.println(m.group() + "子串的起始位置："
				+ m.start() + "，其结束位置：" + m.end());
		}
	}
}
```

> matchesO和 lookingAtO方法有点相似，只是 matchesO方法要求整个字符串和 Pattem 完全匹配时才返回 true ，而 lookingAtO只 要字符串以 Pattem 开头就会返回 true 应用于新的字符序列。resetO方法可将现有的 Matcher 对象。看如下例子程序。

```java
public class MatchesTest
{
	public static void main(String[] args)
	{
		String[] mails =
		{
			"kongyeeku@163.com" ,
			"kongyeeku@gmail.com",
			"ligang@crazyit.org",
			"wawa@abc.xx"
		};
		String mailRegEx = "\\w{3,20}@\\w+\\.(com|org|cn|net|gov)";
		Pattern mailPattern = Pattern.compile(mailRegEx);
		Matcher matcher = null;
		for (String mail : mails)
		{
			if (matcher == null)
			{
				matcher = mailPattern.matcher(mail);
			}
			else
			{
				matcher.reset(mail);
			}
			String result = mail + (matcher.matches() ? "是" : "不是")
				+ "一个有效的邮件地址！";
			System.out.println(result);
		}
	}
}
```

> 上面程序创建了 一个邮件地址的 Pattem ，接着用这个 Pattem 与多个邮件地址进行匹配。当程序中 的 Matcher 为 null 时 ，程序调用 matcherO方法来创建一个 Matcher 对象， 一旦 Matcher 对象被创建，程 序就调用 Matcher 的 resetO方法将该 Matcher 应用于新的字符序列 。
>
> 从某个角度来看， Matcher 的 matchesO 、 lookingAtO和 String 类的 equalsO 、 startsWithO有点相似 。 区别是 String 类的 equalsO和 startsWithO都是与字符串进行 比较，而 Matcher 的 matchesO和 lookingAtO 则是与正则表达式进行匹配 。
>
> 事实上， String 类里也提供了 matchesO方法，该方法返回 该字符串是否匹配指定的正则表达式。

> 还可以利用正则表达式对目标字符串进行分割、查找、替换等操作.

```java
public class ReplaceTest
{
	public static void main(String[] args)
	{
		String[] msgs =
		{
			"Java has regular expressions in 1.4",
			"regular expressions now expressing in Java",
			"Java represses oracular expressions"
		};
		Pattern p = Pattern.compile("re\\w*");
		Matcher matcher = null;
		for (int i = 0 ; i < msgs.length ; i++)
		{
			if (matcher == null)
			{
				matcher = p.matcher(msgs[i]);
			}
			else
			{
				matcher.reset(msgs[i]);
			}
			System.out.println(matcher.replaceAll("込込:)"));
		}
	}
}
```

> 上面程序使用了 Matcher 类提供的 replaceAllO把字符串中所有与正则表达式匹配的子串替换成" 哈 哈:)" ，实际上， Matcher 类还提供了 一个 replaceFirstO ， 该方法只替换第 一个匹配的子串 。 运行上面程 序，会看到字符串中所有以" re " 开头的单词都会被替换成"哈哈:) "。
>
> 实际上 ， String 类中也提供了 replaceAllO 、 replaceFirstO 、 splitO等方法 。 下面的例子程序直接使用 String 类提供的正则表达式功能来进行替换和分割。

```java
public class StringReg
{
	public static void main(String[] args)
	{
		String[] msgs =
		{
			"Java has regular expressions in 1.4",
			"regular expressions now expressing in Java",
			"Java represses oracular expressions"
		};
		for (String msg : msgs)
		{
			System.out.println(msg.replaceFirst("re\\w*" , "込込:)"));
			System.out.println(Arrays.toString(msg.split(" ")));
		}
	}
}
```

## 2.4  变量处理和方法处理

> Java 9 引入了一个新的 VarHandle 类，井增强了原有的 MethodHandle 类 。 通过这两个类，允许 Java 像动态语言 一样引用变量、引用方法，并调用它们。
>

### 2.4.1 Java 9 增强的 MethodHandle

> MethodHandle 为 Java 增加了方法引用 的功能， 方法引用的概念有点类似于 C 的"函数指针 " 。这 种方法引用是一种轻量级的引用方式 ， 它不会检查方法的访问权限 ，也不管方法所属的类、实例方法或 静态方法 ， MethodHandle 就是简单代表特定的方法，井可通过 MethodHandle 来调用方法 。 
>
> 为了使用 MethodHandle ，还涉及如下几个类 。 
>
> 1. MethodHandles: MethodHandle 的工厂类 ， 它提供了 一系列静态方法用于获取 MethodHandle。 
> 2. MethodHandles.Lookup: Lookup 静态内部类也是 MethodHandle、 VarHandle 的工厂类，专 门用 于获取 MethodHandle 和 VarHandle。 
> 3. MethodType: 代表一个方法类型。 MethodType 根据方法的形参、返回值类型来确定方法类型 。

```java
public class MethodHandleTest
{
	// 定义一个private的类方法
	private static void hello()
	{
		System.out.println("Hello world!");
	}
	// 定义一个private的实例方法
	private String hello(String name)
	{
		System.out.println("执行带参数的hello" + name);
		return name + ",您好";
	}
	public static void main(String[] args) throws Throwable
	{
		// 定义一个返回值为void、不带形参的方法类型
		MethodType type = MethodType.methodType(void.class);
		// 使用MethodHandles.Lookup的findStatic获取类方法
		MethodHandle mtd = MethodHandles.lookup()
			.findStatic(MethodHandleTest.class, "hello", type);
		// 通过MethodHandle执行方法
		mtd.invoke();
		// 使用MethodHandles.Lookup的findVirtual获取实例方法
		MethodHandle mtd2 = MethodHandles.lookup()
			.findVirtual(MethodHandleTest.class, "hello",
			// 指定获取返回值为String, 形参为String的方法类型
			MethodType.methodType(String.class, String.class));
		// 通过MethodHandle执行方法，传入主调对象和参数
		System.out.println(mtd2.invoke(new MethodHandleTest(), "孙悟空"));
	}
}
```

> 从上面三行粗体字代码可以看出，程序使用 MethodHandles.Lookup 对象根据类、方法名、方法类型来获取 MethodHandle 对象。由于此处的方法名只是一个字符串，而该字符串可以来自于变量、配置 文件等，这意味着通过 MethodHandle 可以让 Java 动态调用某个方法。
>

### 2.4.2 Java 9 增加的 VarHandle

> VarHandle 主要用于动态操作数组的元素或对象的成员 变量。 VarHandle 与 MethodHandle 非常相似， 它也需要通过 MethodHandles 来获取实例，接下来调用 VarHandle 的方法即可动态操作指定数组的元素 或指定对象的成员变量 。

```java
class User
{
	String name;
	static int MAX_AGE;
}
public class VarHandleTest
{
	public static void main(String[] args)throws Throwable
	{
		String[] sa = new String[]{"Java", "Kotlin", "Go"};
		// 获取一个String[]数组的VarHandle对象
		VarHandle avh = MethodHandles.arrayElementVarHandle(String[].class);
		// 比较并设置：如果第三个元素是Go，则该元素被设为Lua
		boolean r = avh.compareAndSet(sa, 2, "Go", "Lua");
		// 输出比较结果
		System.out.println(r); // 输出true
		// 看到第三个元素被替换成Lua
		System.out.println(Arrays.toString(sa));
		// 获取sa数组的第二个元素
		System.out.println(avh.get(sa, 1)); // 输出Kotlin
		// 获取并设置：返回第三个元素，并将第三个元素设为Swift
		System.out.println(avh.getAndSet(sa, 2, "Swift"));
		// 看到第三个元素被替换成Swift
		System.out.println(Arrays.toString(sa));

		// 用findVarHandle方法获取User类中名为name，
		// 类型为String的实例变量
		VarHandle vh1 = MethodHandles.lookup().findVarHandle(User.class,
			"name", String.class);
		User user = new User();
		// 通过VarHandle获取实例变量的值，需要传入对象作为调用者
		System.out.println(vh1.get(user)); // 输出null
		// 通过VarHandle设置指定实例变量的值
		vh1.set(user, "孙悟空");
		// 输出user的name实例变量的值
		System.out.println(user.name); // 输出孙悟空
		// 用findVarHandle方法获取User类中名为MAX_AGE，
		// 类型为Integer的类变量
		VarHandle vh2 = MethodHandles.lookup().findStaticVarHandle(User.class,
			"MAX_AGE", int.class);
		// 通过VarHandle获取指定类变量的值
		System.out.println(vh2.get()); // 输出0
		// 通过VarHandle设置指定类变量的值
		vh2.set(100);
		// 输出User的MAX_AGE类变量
		System.out.println(User.MAX_AGE); // 输出100
	}
}
```

> 从上面前 两行粗体字 代码可 以 看 出，程序调用 MethodHandles 类的静态方法可获取操作数组的 VarHandle 对象，接下来程序可通过 VarHandle 对象来操作数组的方法，包括比较并设置数组元素、获 取并设置数组元素等 ， VarHandle 具体支持哪些方法则可参考 API 文档。
>
> 上面程序中后面三行粗体字代码则示范了使用 VarHandle 操作 实例变量 的情形，由于实例变量需要使用对象来访问， 因此使用 VarHandle 操作实例变量时需要传入一个 User 对象 。 VarHandle 既可设置实例变量 的值 ，也可获取实例变量 的值 。当然 VarHandle 也提供了更多的方法来操作实例变量，具体可参考 API 文挡。 
>
> 使用 VarHandle 操作类变量与操作实例变量差 别不大，区别只是类变量不需要对象，因此使用 VarHandle 操作类变量时无须传入对象作为参数 。
>
> VarHandle 与 MethodHandle 一样，它也是一种动态调用机制，当程序通过 MethodHandles.Lookup 来获取成员变量时，可根据字符串名称来获取成员变量，这个字符串名称同样可以是动态改变的，因此 非常灵活。

## 2.5 Java 9 改进的国际化与格式化

> 国际化 的英文单词是 Intemationalization ， 因为这个单词太长了，有时也简称 I1 8N ，其中 I 是这个单词的第一 个字母， 1 8 表示中间省略的 字母个数，而 N 代表这个单词的最后 一个字母 。
>
> Localization， 即本地化。类似于国际化可以称为I1 8N ，本地化也可以称为 L10N 。

### 2.5.1 Java 国际化的思路

> Java 程序的国际化思路是将程序中的标签、提示等信 息放在资源文件中 ， 程序需要支持哪些国家、语 言 环境， 就对应提供相应的资源文件 。 资源文件是 key-value 对， 每个资源文件中的 key 是不变的，但 value 则 随不同的国 家、语言而改变。图 7.7 显示了 Java 程序国际化的思路 。 
>
> Java 程序的国际化主要通过如下三个类完成 。 
>
> 1. java.util.ResourceBundle: 用于加载国家、语 言资 源包 。 
> 2. java.util.Locale: 用于封装特定的国家/区域、语言 环境。 
> 3. java.text.MessageFormat: 用 于格式化带占位符的字符串 。 

> 为了实现程序的国际化 ，必须先提供程序所需要的资源文件。资源文件的内容是很多 key-value 对 ， 其中 key 是程序使用的部分，而 value 则 是程序界面的显示字符串 。
>
> 资源文件的命名可 以有如下三种形式 。
>
> 1. baseN ame_language_ country. properties 
> 2. baseN ame_language. properties
> 3. baseName.properties
>
> 其中 baseName 是资源文件的基本名 ，用户可随意指定:而 language 和 county 都不可随意变化，必须是 Java 所支持的语言和国家 。
>

### 2.5.2 Java 支持的国家和语言

```java
public class LocaleList
{
	public static void main(String[] args)
	{
		// 返回Java所支持的全部国家和语言的数组
		Locale[] localeList = Locale.getAvailableLocales();
		// 遍历数组的每个元素，依次获取所支持的国家和语言
		for (int i = 0; i < localeList.length ; i++ )
		{
			// 输出出所支持的国家和语言
			System.out.println(localeList[i].getDisplayCountry()
				+ "=" + localeList[i].getCountry()+ " "
				+ localeList[i].getDisplayLanguage()
				+ "=" + localeList[i].getLanguage());
		}
	}
}
```

### 2.5.3 完成程序国际化

> 为上面程序提供如 下两个文件。
>
> 第一个文件 : mess _zh_ CN .properties ， 该文件的内 容为:

```java
# 资源文件的内 容是 key -value 对 
hello=你好!
```

> 第二个文件 : mess_en_US.properties ，该文件的内 容为 :

```java
# 资源文件 的内 容是 key-value 对
hello=Welcome!
```

> Java 9 支持使用 UTF-8 字符集来保存属 性文件，这样在属性文件中 就可 以直接包含非西欧字符，因 此属 性文件也不 再需要使用 native2ascii 工具进行处理 。 唯一要注意 的是，属性文件必须 显式保存为 UTF-8 字符集。
>
> Windows 是一个有些怪的操作系统 ， 它保存文件;默认采用 GBK 字符集 。 因此，在 Windows 平台上执行 javac 命令默认也用 GBK 字符集读取 Java 源文件 。 但实际开发项 目 时采用 GBK 字符集会引起很多 乱码问题 ， 所以通常推荐源代码都使用 UTF-8 字符集保存 。 但如果使用 UTF-8 字符集保存 Java 源代码，在命令行编译源程序 时需要为 javac 显式指 定-encoding utf-8 选项 ， 用于告诉 Javac 命令使用 UTF-8 字符集读取 Java 源文件 。 本 书出 于降低学习 难度的考 虑 ，开 始 没有介绍该选项 ， 所以用平台 默认的字符集 ( GBK ) 来保 存 Java 源文件 。

```java
public class Hello
{
	public static void main(String[] args)
	{
		// 取得系统默认的国家/语言环境
		Locale myLocale = Locale.getDefault(Locale.Category.FORMAT);
		// 根据指定国家/语言环境加载资源文件
		ResourceBundle bundle = ResourceBundle
			.getBundle("mess" , myLocale);
		// 打印从资源文件中取得的消息
		System.out.println(bundle.getString("hello"));
	}
}
```

> 从上面程序可以看出，如果希望程序完成国际化，只 需 要将不同的国家/语 言 CLocale) 的提示信息 分别以不同的文件存放即可 。 例如，简体中文的语言 资源文件就是 Xxx _ zh_ CN. properties 文件，而美国 英语的语言 资源文件就是 Xxx_ en_US.properties 文件 。

> Java 程序国际化的关键类是 ResourceBundle ，它有一个静态方法: getB undle(String baseName , Lo cale locale) ，该方法将根据 Locale 加载资源文件，而 Locale 封装了 一个国家、语言 ，例如，简体中文环境可以用简体中文的 Locale 代表，美国英语环境可以用 美 国英语的 Locale 代表 。通过如下代码来加载资源文件 。
>

```java
// 根据指定的国家 / 语言环境加载资源文件
ResourceBundle bundle = ResourceBundle.getBundle( 川ness" , myLocale);
```

> 上面代码将会加载 baseName 为 mess 的系列资源文件之一 ，到底加载其中的哪个资源文件，则取 决于 myLocale: 对于简体中文的 Locale ，则加载 mess _ zh_ CN .properties 文件 。
>
> 一旦加载了该文件后，该资源文件的内容就是多个 key-value 对，程序就根据 key 来获取指定的信 息，例如获取 key 为 hello 的消息，该消息是啃好!"一一这就是 Java 程序国际化的过程 。
>
> 如果对于美国英语的 Locale ，则加载 mess_ en_US.properties 文件，该文件中 key 为 hello 的消息是 "Welcome! " 。
>
> Java 程序国际化的关键类是 ResourceBundle 和 Locale ， ResourceBundle 根据不同的 Locale 加载语 言资源文件，再根据指定的 key 取得己加载语言 资源文件中的字符串 。

### 2.5.4 使用 MessageFormat 处理包含占位符的字符串

> 可以使用带占位符的消息 。 例如，提供一个 myMess_ en_ US.properties 文件，该文件的内 容如下 :
>

```java
msg=Hello , {O}!Today is {1}.
```

> 提供一个 myMess _ zh _ CN.properties 文件，该文件的内容如下:
>

```java
msg=你好，{O}!今天是 { 1 }。
```

> 上 面的两个资源文件必须用 UTF-8 字符集保存。

> 使用 MessageFormat 类，该类包含一个有用的静态方法 。 
>
> 1. format(String 阴阳m ， Objec t... values) : 返回后面的多个参数值填充前面的 阴阳m 字符串，其中 pattem 字符串不是正则表达式，而是一个带占位符的字符串 。

```java
public class HelloArg
{
	public static void main(String[] args)
	{
		// 定义一个Locale变量
		Locale currentLocale = null;
		// 如果运行程序的指定了两个参数
		if (args.length == 2)
		{
			// 使用运行程序的两个参数构造Locale实例
			currentLocale = new Locale(args[0] , args[1]);
		}
		else
		{
			// 否则直接使用系统默认的Locale
			currentLocale = Locale.getDefault(Locale.Category.FORMAT);
		}
		// 根据Locale加载语言资源
		ResourceBundle bundle = ResourceBundle
			.getBundle("myMess" , currentLocale);
		// 取得已加载的语言资源文件中msg对应消息
		String msg = bundle.getString("msg");
		// 使用MessageFormat为带占位符的字符串传入参数
		System.out.println(MessageFormat.format(msg
			, "yeeku" , new Date()));
	}
}
```

> 对于带占位符的消息字符串，只需要使用 MessageFormat 类的 formatO 方法为消息中的占位符指定参数即可 。

### 2.5.6 使用类文件代替资源文件

> 除使用属性文件作为资源文件外，Java 也 允许使用类文件代替资源文件，即将所有的 key-value 对存入 class 文件，而不是属性文件 。
>
> 使用类文件来代替资源文件必须满足如下条件 。
>
> 1. 该类的类名必须是 baseName_language_country，这与属性文件的命名相似 。
> 2. 该类必须继承 ListResourceBundle ， 并重写 getContentsO方法，该方法返回 Object 数组，该数组 的每一项都是 key-value 对 。 
>
> 下面的类文件可以代替 上面的属性文件 。

```java
public class myMess_zh_CN extends ListResourceBundle
{
	// 定义资源
	private final Object myData[][]=
	{
		{"msg","{0}，你好！今天的日期是{1}"}
	};
	// 重写方法getContents()
	public Object[][] getContents()
	{
		// 该方法返回资源的key-value对
		return myData;
	}
}
```

> 上面文件是一个简体中文语言环境的资源文件， 该文件可以代替 myMess_zh_ CN. properties 文件; 如果需要代替美国英语语言环境的资源文件，则还应该提供一个 myMess_ en_ US 类。
>
> 如果系统同时存在资源文件、类文件，系统将以类文件为主 ，而不会调用资源文件 。对于简体中文 的 Locale ， ResourceBundle 搜索资源文件的顺序是:
>
> 1. baseName zh CN.class 
> 2. baseN ame_ zh_ CN. properties
> 3. baseName zh.class
> 4. baseN ame_zh.properties 
> 5. baseName.class 
> 6. baseName.properties
>
> 系统按上面的顺序搜索资源文件，如果前面的 文件不存在 ，才会使用下 一个文件 。 如果 一直找不到 对应的文件，系统将抛出异常 。

### 2.5.7 Java 9 新增的日志 API

> Java 9 强化了原有的日志 API.这套日志 API 只是定义了记录消息的最小 API.开发者可将这些 日 志消息路由到各种主流的日志框架(如 SLF4J、 Log4J 等) ，否则默认使用 Java 传统的 java.util.logging 日在、 API。
>
> 这套日志 API 的用法非常简单，只要两步即可 。 
>
> 1. 调用 System 类的 getLogger(String name)方法获取 System.Logger 对象。 
> 2. 调用 System.Logger 对象的 logO方法输出日志 。该方法 的第一个参数用 于指定日志级别 。 
>
> 为了与传统 java.util.logging 日志级别、主流日志框架的级别兼容 ， Java 9 定义 了 如表 7 .7 所示的日志级别 。

![Java-Learning-Notes-Picture-10](/Users/lotus/Notes/Java-Learning-Notes/Java-Learning-Notes-Picture-10.png)

> 该日志级别是 一个非常有用的东西 :在开发阶段调试程序 时，可能 需要大量输出调试信 息:在发布软件时，又希望关掉这些调试信息 。 此时就可通过日志来实现，只 要将系 统日志级别调 高 ，所有低于该 级别的日志信息就都会被自动关闭，如果将日志级别设为 OFF ，那么所有 日 志信息都会被关 闭 。
>

```java
public class LoggerTest
{
	public static void main(String[] args)throws Exception
	{
		// 获取System.Logger对象
		System.Logger logger = System.getLogger("fkjava");
		// 设置系统日志级别（FINE对应DEBUG）
		Logger.getLogger("fkjava").setLevel(Level.INFO);
		// 设置使用a.xml保存日志记录
		Logger.getLogger("fkjava").addHandler(new FileHandler("a.xml"));
		logger.log(System.Logger.Level.DEBUG, "debug信息");
		logger.log(System.Logger.Level.INFO, "info信息");
		logger.log(System.Logger.Level.ERROR, "error信息");
	}
}
```

> 上面程序中第一行粗体字代码获取 Java 9 提供的日志 API.由于此处并未使用第三方日志框架，因此系统默认使用 java.util.logging 日志作为实现，因此第二行代码使用 java.util. logging.Logger 来设置日 志级别。程序将系统日志级别设为 F卧mC 等同于 DEBUG) ，这意味着高于或等于 DEBUG 级别的日志 信息都会被输出到 a.刀nl 文件。运行上面程序，将可以看到在该文件所在目录下生成了一个 a.xml 文件， 该文件中包含三条日志记录，分别对应于上面三行代码调用 logO方法输出的日志记录 。
>
> 如果将上面第 二行粗体字代码的日志级别改为 SEVERE C 等同于 ERROR) ，这意味着高于或等于 ERROR 级别的日志信息都会被输出到 a.xml 文件。再次运行该程序，将会看到该程序生成的 a.xml 文 件仅包含一条日志记录，这意味着 DEBUG 、 INFO 级别的日志信息都被自动关闭了。

> Java 9 的日志 API 也支持国际化一-System 类除使用简单的 getLogger(String name) 方法获取 System.Logger 对象之外，还可使用 getLogger(String name , ResourceBundle bundle)方法来获取 该对象，该方法需要传入一个国际化语 言资源包，这样该 Logger 对象即可根据 key 来输出国际化的日 志信息。

> 先为美式英语环境提供一个 logMess_ en_ US.properties 文件，该文件的内容如下 :
>

```java
debug=Debug Message 
info=Plain Message 
error=Error Message
```

> 再为简体中文环境提供一个 logMess_ zh_CN .properties 文件，该文件的内容如下:
>

```java
debug=调试信息 
info=普通信息 
error=错误信息
```

> 接下来程序可使用 ResourceBundle 先加载该国际化语 言资源包 ，然后就可通过 Java 9 的日志 API 来输出国际化的日志信息了 。

```java
public class LoggerI18N
{
	public static void main(String[] args)throws Exception
	{
		// 加载国际化资源包
		ResourceBundle rb =	ResourceBundle.getBundle("logMess",
			Locale.getDefault(Locale.Category.FORMAT));
		// 获取System.Logger对象
		System.Logger logger = System.getLogger("fkjava", rb);
		// 设置系统日志级别（FINE对应DEBUG）
		Logger.getLogger("fkjava").setLevel(Level.INFO);
		// 设置使用a.xml保存日志记录
		Logger.getLogger("fkjava").addHandler(new FileHandler("a.xml"));
		// 下面3个方法的第二个参数是国际化消息的key
		logger.log(System.Logger.Level.DEBUG, "debug");
		logger.log(System.Logger.Level.INFO, "info");
		logger.log(System.Logger.Level.ERROR, "error");
	}
}
```

### 2.5.8 使用 NumberFormat 格式化数字

> MessageFormat 是抽象类 Format 的子类， Format 抽 象 类还有两个子类: NumberFormat 和 DateFormat ，它们分 别用以实现数值、日期的格式化 。 NumberFormat 、 DateFormat 可以将数值、日期转换成宇符串，也可以将字 符串转换成数值、日期。
>
> NumberFormat 和 DateFormat 都包含了 formatO 和 parseO方法，其中 formatO用于将数值、日期格式化成字符 串， parseO用于将字符串解析成数值、日期 。 
>
> NumberFormat 也是一个抽象基类，所以无法通过它的 构造器来创建 NumberFormat 对象，它提供了如下几个类方法来得到 NumberFormat 对象 。
>
> 1. getCurrencylnstanceO: 返回默认 Locale 的货币格式器 。 也可以在调用该方法时传入指定的 Locale ， 则获取指定 Locale 的货币格式器 。 
> 2. getlntegerInstanceO: 返回默认 Locale 的整数格式器 。 也可以在调用该方法时传入指定的 Locale ， 则获取指定 Locale 的整数格式器 。 
> 3. getNumberInstanceO: 返回默认 Locale 的通用 数值格式器。也可以在调用该方法时传入指定的 Locale ，则获取指定 Locale 的通用数值格式器 。 
> 4. getPercentlnstanceO: 返回默认 Locale 的百分数格式器 。 也可以在调用该方法时传入指定的 Locale ，则获取指定 Locale 的百分数格式器 。

![Java-Learning-Notes-Picture-11](/Users/lotus/Notes/Java-Learning-Notes/Java-Learning-Notes-Picture-11.png)

```java
public class NumberFormatTest
{
	public static void main(String[] args)
	{
		// 需要被格式化的数字
		double db = 1234000.567;
		// 创建四个Locale，分别代表中国、日本、德国、美国
		Locale[] locales = {Locale.CHINA, Locale.JAPAN
			, Locale.GERMAN,  Locale.US};
		NumberFormat[] nf = new NumberFormat[12];
		// 为上面四个Locale创建12个NumberFormat对象
		// 每个Locale分别有通用数值格式器、百分比格式器、货币格式器
		for (int i = 0 ; i < locales.length ; i++)
		{
			nf[i * 3] = NumberFormat.getNumberInstance(locales[i]);
			nf[i * 3 + 1] = NumberFormat.getPercentInstance(locales[i]);
			nf[i * 3 + 2] = NumberFormat.getCurrencyInstance(locales[i]);
		}
		for (int i = 0 ; i < locales.length ; i++)
		{
			String tip = i == 0 ? "----中国的格式----" :
				i == 1 ? "----日本的格式----" :
				i == 2 ? "----德国的格式----" :"----美国的格式----";
			System.out.println(tip);
			System.out.println("通用数值格式："
				+ nf[i * 3].format(db));
			System.out.println("百分比数值格式："
				+ nf[i * 3 + 1].format(db));
			System.out.println("货币数值格式："
				+ nf[i * 3 + 2].format(db));
		}
	}
}
```

### 2.5.9 使用 DateFormat 格式化日期、时间

> 与 NumberFormat 相似的 是 ，DateFormat 也是一个抽 象类 ，它 也提供了 如下几个类方法用于获 DateFormat 对象 。
>
> 1. getDateInstanceO: 返回 一个日期格式器 ， 它格式化后 的 字符 串 只 有 日期 ， 没有时间 。 该方法可 以传入多 个参数 ， 用于 指定日期样式和 Locale 等参数 :如果不指定这些参数 ，则使用默认参数 。 
> 2. getTimeInstanceO: 返回 一个时间格式器， 它格式化后的字符 串只有时间，没有日期 。该方法可 以传入多个参数 ，用 于指定时 间样式和 Locale 等参数: 如果不指定这些参数，则使用 默认参数 。 
> 3. getDateTimeInstanceO: 返回 一个 日 期、时间 格式器 ， 它格式化后 的字符串既有 日期，也有 时间 。 店方法可 以传入多个参数 ， 用于指定日 期样式 、时间样式和 Locale 等参数 ;如果不指定这些参数 ，则使用默认参数 。 
>
> 上面三个方法可 以指定日期样式、时间 样式参数 ，它们 是 DateFormat 的 4 个静态常量 : FULL、 LONG、 MED町M 和 SHORT ， 通过这 4 个样式参数可 以控制 生成的格式化宇符串 。 看如下例子程序 。

```java
public class DateFormatTest
{
	public static void main(String[] args)
		throws ParseException
	{
		// 需要被格式化的时间
		Date dt = new Date();
		// 创建两个Locale，分别代表中国、美国
		Locale[] locales = {Locale.CHINA, Locale.US};
		DateFormat[] df = new DateFormat[16];
		// 为上面两个Locale创建16个DateFormat对象
		for (int i = 0 ; i < locales.length ; i++)
		{
			df[i * 8] = DateFormat.getDateInstance(SHORT, locales[i]);
			df[i * 8 + 1] = DateFormat.getDateInstance(MEDIUM, locales[i]);
			df[i * 8 + 2] = DateFormat.getDateInstance(LONG, locales[i]);
			df[i * 8 + 3] = DateFormat.getDateInstance(FULL, locales[i]);
			df[i * 8 + 4] = DateFormat.getTimeInstance(SHORT, locales[i]);
			df[i * 8 + 5] = DateFormat.getTimeInstance(MEDIUM , locales[i]);
			df[i * 8 + 6] = DateFormat.getTimeInstance(LONG , locales[i]);
			df[i * 8 + 7] = DateFormat.getTimeInstance(FULL , locales[i]);
		}
		for (int i = 0 ; i < locales.length ; i++)
		{
			String tip = i == 0 ? "----中国日期格式----":"----美国日期格式----";
			System.out.println(tip);
			System.out.println("SHORT格式的日期格式："
				+ df[i * 8].format(dt));
			System.out.println("MEDIUM格式的日期格式："
				+ df[i * 8 + 1].format(dt));
			System.out.println("LONG格式的日期格式："
				+ df[i * 8 + 2].format(dt));
			System.out.println("FULL格式的日期格式："
				+ df[i * 8 + 3].format(dt));
			System.out.println("SHORT格式的时间格式："
				+ df[i * 8 + 4].format(dt));
			System.out.println("MEDIUM格式的时间格式："
				+ df[i * 8 + 5].format(dt));
			System.out.println("LONG格式的时间格式："
				+ df[i * 8 + 6].format(dt));
			System.out.println("FULL格式的时间格式："
				+ df[i * 8 + 7].format(dt));
		}


		String str1 = "2017/10/07";
		String str2 = "2017年10月07日";
		// 下面输出 Sat Oct 07 00:00:00 CST 2017
		System.out.println(DateFormat.getDateInstance().parse(str2));
		// 下面输出 Sat Oct 07 00:00:00 CST 2017
		System.out.println(DateFormat.getDateInstance(SHORT).parse(str1));
		// 下面抛出 ParseException异常
		System.out.println(DateFormat.getDateInstance().parse(str1));
	}
}
```

> 获得了 DateFormat 之后，还可以调用它 的 setLenient(boolean lenient)方法来设置该格 式器是否采用严格语法 。
>
> DateFormat 的 parseO方法可以把一个宇 符串解析成 Date 对象，但它要求被解析的宇 符串必须符合日期字符串的要求，否则可能抛出 ParseException 异常 。

### 2.5.10 使用 SimpleDateFormat 格式化日期

> 前面介绍的 DateFormat 的 parseO方法可以把字符串解析成 Date 对象，但实际上 DateFormat 的 parseO 方法不够灵活一一它要求被解析的字符串必须满足特定的格式!为了更好地格式化日期、解析日期字符 串， Java 提供 了 SimpleDateFormat 类 。
>
> SimpleDateFormat 是 DateFormat 的子类，正如它的名字所暗示的，它是"简单"的日期格式器。 很多读者对"简单"的日期格式器不屑一顾，**实际上 SimpleDateFormat 比 DateFormat 更简单，功能更 强大。**

```java
public class SimpleDateFormatTest
{
	public static void main(String[] args)
		throws ParseException
	{
		Date d = new Date();
		// 创建一个SimpleDateFormat对象
		SimpleDateFormat sdf1 = new SimpleDateFormat("Gyyyy年中第D天");
		// 将d格式化成日期，输出：公元2017年中第282天
		String dateStr = sdf1.format(d);
		System.out.println(dateStr);
		// 一个非常特殊的日期字符串
		String str = "14###3月##21";
		SimpleDateFormat sdf2 = new SimpleDateFormat("y###MMM##d");
		// 将日期字符串解析成日期，输出：Fri Mar 21 00:00:00 CST 2014
		System.out.println(sdf2.parse(str));
	}
}
```

## 2.6 Java 8 新增的日期、时间格式器

> Java 8 新增的日期 、时间 API 里不仅包括了 Instant、 LocalDate 、 LocalDateTime、 LocalTime 等代表 日期、时间的类，而且在 java.time.format 包下提供了一个 DateTimeFormatter 格式器类，该类相当于前面介绍的 DateFormat 和 SimpleDateFormat 的 合体，功能非常强大 。 
>
> 与 DateFormat、 SimpleDateFormat 类似， DateTimeFormatter 不仅可以将日期、时间对象格式化成字 符串，也可以将特定格式的字符串解析成日期、时间对象 。 
>
> 为了使用 DateTimeFormatter 进行格式化或解析，必须先获取 DateTimeFormatter 对象，获取 DateTimeFormatter 对象有如下三种 常见的方式。
>
> 1. 直接使用静态常量创建 DateTimeFormatter 格式器 。 DateTimeFormatter 类中包含了大量形如 ISO LOCAL DATE 、 ISO LOCAL TIME 、 ISO LOCAL DATE TIME 等静态常量，这些静态常 量本身就是 DateTimeFormatter 实例 。
> 2. 使用代表不同风格的枚举值来创建 DateTimeFormatter 格式器 。 在 FormatStyle 枚举类中定义了 FULL、 LONG 、 MEDIUM、 SHORT 四 个枚举值，它们代表日期、时间的不同风格 。
> 3. 根据模式字符串来创建 DateTimeFormatter 格式器 。 类似于 SimpleDateFormat ， 可以采用模式字 符串来创建 DateTimeFormatter，如果需要了解 DateTimeFormatter 支持哪些模式宇符串 ，则 需要 参辛苦该类的 API 文档 。

### 2.6.1 使用 Date Ti meF ormatter 完成格式化

> 使用 DateTimeFormatter 将日期、时间（LocalDate、LocalDateTime、LocalTime 等实例）格式化为字符串 ， 可通过如下两种方式 。 
>
> 1. 调用 DateTimeFormatter 的 format(TemporalAccessor temporal)方法执行格式化 ，其中 LocalDate、LocalDateTime、 LocalTime 等类都是 TemporalAccessor 接口的实现类。
> 2. 调用 Local，Date 、 LocalDateTime 、 LocalTime 等 日 期、时间对象的 format(DateTimeFormatter formatter)方法执行格式化 。

```java
public class NewFormatterTest
{
	public static void main(String[] args)
	{
		DateTimeFormatter[] formatters = new DateTimeFormatter[]{
			// 直接使用常量创建DateTimeFormatter格式器
			DateTimeFormatter.ISO_LOCAL_DATE,
			DateTimeFormatter.ISO_LOCAL_TIME,
			DateTimeFormatter.ISO_LOCAL_DATE_TIME,
			// 使用本地化的不同风格来创建DateTimeFormatter格式器
			DateTimeFormatter.ofLocalizedDateTime(FormatStyle.FULL, FormatStyle.MEDIUM),
			DateTimeFormatter.ofLocalizedDate(FormatStyle.LONG),
			// 根据模式字符串来创建DateTimeFormatter格式器
			DateTimeFormatter.ofPattern("Gyyyy%%MMM%%dd HH:mm:ss")
		};
		LocalDateTime date = LocalDateTime.now();
		// 依次使用不同的格式器对LocalDateTime进行格式化
		for(int i = 0 ; i < formatters.length ; i++)
		{
			// 下面两行代码的作用相同
			System.out.println(date.format(formatters[i]));
			System.out.println(formatters[i].format(date));
		}
	}
}
```

> 使用 Date TimeF ormatter 进行格式化时不仅可按系统预置的格式对日期、时间进行格式化，也可使用模式字符串对日期、时间进行自定义格式化，由此可见， 功能完全覆盖了传统 的 DateFormat、 SimpleDateFormate 的功能 。
>
> 有些时候 ，读者可能还需要使用传统的 DateFormat 来执行格式化 ， DateTimeFormatter 则提供了一个 toFormat() 方法，该方法可以获取 DateTimeFormat阳对应的 Format 对象。
>

### 2.6.2 使用 DateTimeFormatter 解析字符串

> 为了使用 DateTimeFormatter 将指定格式 的字符串解析成日期、时间对象 (LocalDate 、 LocalDateTime 、 LocalTime 等实例) ，可通过日期、时间对象提供的 parse(CharSequence text , D ateTimeFormatter formatter) 方法进行解析 。

```java
public class NewFormatterParse
{
	public static void main(String[] args)
	{
		// 定义一个任意格式的日期时间字符串
		String str1 = "2014==04==12 01时06分09秒";
		// 根据需要解析的日期、时间字符串定义解析所用的格式器
		DateTimeFormatter fomatter1 = DateTimeFormatter
			.ofPattern("yyyy==MM==dd HH时mm分ss秒");
		// 执行解析
		LocalDateTime dt1 = LocalDateTime.parse(str1, fomatter1);
		System.out.println(dt1); // 输出 2014-04-12T01:06:09
		// ---下面代码再次解析另一个字符串---
        String str2 = "2014$$$4月$$$13 20小时";
        DateTimeFormatter fomatter2 = DateTimeFormatter
            .ofPattern("yyy$$$MMM$$$dd HH小时");
        LocalDateTime dt2 = LocalDateTime.parse(str2, fomatter2);
        System.out.println(dt2); // 输出 2014-04-13T20:00

	}
}
```

