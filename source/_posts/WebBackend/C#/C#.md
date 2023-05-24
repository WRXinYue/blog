---
title: C#
date: 2022-07-13 16:53:14.0
updated: 2023-04-18 15:48:54
url: /archives/c
categories: 
- C#/.NET
tags: 
- c#
---

<h1>1 .NET框架</h1>
<p>.NET框架由三部分组成：</p>
<ul>
<li>编程工具：包括Visual Studio集成开发环境，调试器，.NET兼容的编译器等</li>
<li>CLR（Common Language Runtime，公共语言运行库）：在运行时管理程序的执行，包括内存管理和垃圾收集、代码安全验证、代码执行线程管理及异常处理等</li>
<li>BCL（Base Class Library，基类库）：包括通用基础类（文件操作、字符串操作等相关的类）、集合类（列表、字典、散列表）、线程和同步类、XML类。</li>
</ul>
<p>以下图片说明了3个用不同语言编写的程序的完整编译时和运行的过程</p>
<p><a href="https://wyh317.github.io/img/1.5.jpg"><img src="https://wyh317.github.io/img/1.5.jpg" alt="NET框架" /></a></p>
<p><a href="https://wyh317.github.io/img/1.5.jpg">NET框架</a></p>
<h1>2. C#编程概述</h1>
<p>一个简单的C#程序，这段程序会输出“Hi there！”</p>
<pre><code class="language-c#">//告诉编译器这个程序使用了System命名空间的类型
using System;
//声明一个新命名空间，名称为Simple
namespace Simple{
    class Program{
        static void Main(){
            Console.WriteLine(&quot;Hi there!&quot;)
        }
    }
}
Copy</code></pre>
<p>在C#中，WirteLine相当于java中的println，Write相当于java中的print</p>
<pre><code class="language-c#">Console.WriteLine(&quot;Three integers are {1}, {0} and {1}.&quot;, 3, 6);
Copy</code></pre>
<p>以上语句将在屏幕上显示：
Three integers are 6, 3 and 6.</p>
<h2>类型存储和变量</h2>
<p>命名空间是一种把相关的类型声明分组并命名的方法。既然程序是一组相关的类型声明，那么通常会把程序声明在你创建的命名空间内部。</p>
<h2>预定义类型</h2>
<p>C#提供了16种预定义类型，包括13种简单类型和3种非简单类型</p>
<p>简单类型：
| 名称 | 含义 |
| ———– | ———– |
| int | 32位有符号整数 |
| uint | 32位无符号整数 |
| long | 64位有符号整数 |
| ulong | 62位无符号整数 |
| short | 16位有符号整数 |
| ushort | 16位无符号整数 |
| byte | 8位有符号整数 |
| sbyte | 8位无符号整数 |
| float | 单精度浮点数 |
| double | 双精度浮点数 |
|decimal|高精度小数类型|
| bool | 布尔型 |
| char | Unicode字符串 |</p>
<p>非简单类型：</p>
<ul>
<li>object：所有其他类的基类</li>
<li>string：多个Unicode字符组成的序列</li>
<li>dynamic：在使用动态语言编写的程序集时使用</li>
</ul>
<p>C#语言是静态的，但基于.NET的一些其他语言却是动态的，也就是说变量的类型直到运行时才会被解析。由于它们是.NET语言，所以C#程序需要使用这些语言编写的程序集。问题是程序集中的类型直到运行时才会被解析，而C#又要引用这样的类型并且需要在编译的时候解析类型。为了解决这个问题，有了dynamic关键字。</p>
<p>在编译时，编译器不会对dynamic类型的变量进行类型检查。相反，它将与该变量及该变量的操作有关的所有信息打包。在运行时会对这些信息进行检查，以确保它与变量所代表的实际类型保持一致性，否则将在运行时抛出异常。</p>
<h2>用户定义类型</h2>
<p>C#中有6种用户自定义类型</p>
<ul>
<li>类类型class</li>
<li>结构类型struct</li>
<li>数组类型array</li>
<li>枚举类型enum</li>
<li>委托类型delegate</li>
<li>接口类型interface</li>
</ul>
<h1>3. 方法</h1>
<h2>类型推断和var关键字</h2>
<p>var关键字不是特定类型变量的符号，它是从等号右边推断出的实际类型的速记。</p>
<pre><code class="language-c#">//在下面的第一个声明中，var是int的速记
//第二个声明中，var是MyExcellentClass的速记
static void Main(){
    var total = 15;  
    var mec = new MyExcellentClass();
}
Copy</code></pre>
<p>使用var关键字有一些重要的条件：</p>
<ul>
<li>只能用于本地变量，不能用于字段</li>
<li>只能在变量声明中包含初始化的时候使用</li>
<li>一旦编译器推断出变量的类型，它就是固定且不能更改的</li>
</ul>
<h2>本地常量</h2>
<p>用const修饰符来修饰（类似于java中的final）</p>
<p>常量和变量的语法除了以下两点外都相同：</p>
<ul>
<li>常量在类型之前增加关键字const</li>
<li>常量必须有初始化语句，也就是说初始值不能在编译期确定。因此，它不能是某个对象的引用（但可以是null的引用），因为对象的引用是在运行时决定的。</li>
</ul>
<h2>参数</h2>
<p>首先区分下<strong>形参</strong>和<strong>实参</strong>的概念：</p>
<pre><code class="language-c#">//以下函数的参数声明中，x和y均为形参
public void PrintSum(int x, float y){

}
Copy
//以下函数的调用中，5和someInt均为实参,实参的值用于初始化形参
PrintSum(5, someInt){

}
Copy</code></pre>
<h3>1.值参数</h3>
<p>Java中的参数传递类型（值传递），即：值参数是把实参的值复制给形参，二者在栈中的不同位置。</p>
<ul>
<li>在方法被调用前，用作实参的变量a2已经在栈中了</li>
<li>在方法开始时，系统在栈中为形参分配空间，并从实参复制值
<ul>
<li>因为a1是引用类型，所以a1的值（即指向对象的地址）被复制，形参和实参都指向堆中的同一个对象</li>
<li>因为a2是值类型的，所以值被复制，产生了一个独立的数据项</li>
</ul></li>
<li>在方法中，f2和对象f1的字段都被加上了5</li>
<li>方法结束后，形参从栈中弹出</li>
</ul>
<p><a href="https://wyh317.github.io/img/值参数.jpg"><img src="https://wyh317.github.io/img/%E5%80%BC%E5%8F%82%E6%95%B0.jpg" alt="值参数" /></a></p>
<p><a href="https://wyh317.github.io/img/值参数.jpg">值参数</a></p>
<h3>2.引用参数</h3>
<p>对于引用参数，系统不会在栈中为形参分配新的空间，形参的参数名将作为实参的别名，指向相同的内存位置</p>
<ul>
<li>使用引用参数时，必须在方法的声明和调用中都使用ref修饰符</li>
<li>实参必须是变量，在用作实参前必须被赋值</li>
</ul>
<pre><code>//方法声明中要使用ref修饰符
void MyMethod(ref int val){

}

int y = 1;
MyMethod(ref y)   //使用y前必须赋值
MyMethod(ref 3 + 5)   //会报错，因为引用参数作为实参必须是变量，不能是表达式
Copy</code></pre>
<ul>
<li>在方法调用前，将要被用作实参的变量a1和a2已经在栈里了</li>
<li>在方法的开始，形参名被设置为实参的别名。引用相同的内存位置</li>
<li>在方法结束后，f2和f1的对象的字段都被加上了5</li>
</ul>
<p><a href="https://wyh317.github.io/img/引用参数.jpg"><img src="https://wyh317.github.io/img/%E5%BC%95%E7%94%A8%E5%8F%82%E6%95%B0.jpg" alt="引用参数" /></a></p>
<p><a href="https://wyh317.github.io/img/引用参数.jpg">引用参数</a></p>
<p>对比将引用类型对象作为值参数和引用参数传递的两种情况：</p>
<ul>
<li>将引用类型对象作为值参数传递：如果在方法内创建一个对象并赋值给形参，将切断形参和实参之间的关联，并且在方法调用结束后，新对象将不复存在</li>
<li>将引用类型对象作为引用参数传递：如果在方法内创建一个新对象并赋值给形参，会让实参也引用该新对象，并且在方法结束后该对象仍然存在。</li>
</ul>
<h2>3.输出参数</h2>
<p>输出参数用于从方法体内把数据传出到调用代码，修饰符为out。和引用参数非常类似</p>
<p>和引用参数一样，输出参数的形参担当实参的别名，方法内对形参的任何改变在方法完成后通过实参变量都是可见的。</p>
<p>唯一和引用参数不同的是：<strong>方法内的代码在读取输出参数之前必须先对其写入</strong></p>
<pre><code class="language-c#">public void Add(out int outValue){
    //以下这句会报错，因为输出参数outValue在方法中被读取前没有被赋值
    int var1 = outValue + 2;
}
Copy</code></pre>
<h2>4.参数数组</h2>
<p>参数数组允许0个或多个实参对应一个特殊的形参,修饰符为params</p>
<pre><code class="language-c#">//形参inVals可以代表0个或多个实参
void ListInts(params int[] inVals){

}
Copy</code></pre>
<ul>
<li>在参数列表中只能有一个参数数组，并且是列表中的最后一个</li>
<li>由参数数组表示的所有参数必须具有相同的类型</li>
</ul>
<p>参数数组在方法声明中需要params修饰符，而在调用时不需要（不同于引用参数和输出参数，它们在以上两个地方都需要修饰符）</p>
<p>可以有如下两种方式为参数数组提供实参：</p>
<ol>
<li>
<p>用一个逗号分隔的该数据类型元素的列表,使用这种方法时，编译器做如下的事：</p>
<ul>
<li>
<p>接收实参列表，用它们在堆中创建并初始化一个数组</p>
</li>
<li>
<p>把数组的引用作为形参保存在栈中</p>
<pre><code class="language-c#">ListInts(10, 20, 30)
Copy</code></pre>
</li>
</ul>
</li>
<li>
<p>用数组作为实参</p>
<p>在这种情况下，编译器会直接使用传入的数组，也就是说栈中的形参指向内存中intArray的位置</p>
<pre><code class="language-c#">int[] intArray = {1, 2, 3};
ListInts(intArray);
Copy</code></pre>
<h2>5.命名参数</h2>
<p>在使用命名参数时，需要在方法调用中包含参数名。而方法的声明无需任何改变</p>
<pre><code class="language-c#">class MyClass{
   //方法中的参数声明一如平常
   public int Calc(int a, int b, int c){
       return a + b + c;
   }
   static void Main(){
       MyClass mc = new MyClass();
       int result = mc.Calc(c: 2, a: 4, b: 3);
   }
}
Copy</code></pre>
<h3>6.可选参数</h3>
<p>所谓可选参数就是在调用方法的时候可以包含这个参数，也可以忽略它。</p>
<pre><code class="language-c#">class MyClass{
   //b为可选参数，默认值为3
   public int Calc(int a, int b = 3){
       return a + b;
   }
   static void Main(){
       MyClass mc = new MyClass();
       int ro = mc.Calc(5, 6);
       int r1 = mc.Calc(5);
       Console.WriteLine("{0}, {1}", ro, r1);
   }
}
Copy</code></pre>
<p>上述代码会输出11，8</p>
</li>
</ol>
<p>只要值类型的默认值在编译的时候可以确定，就可以使用值参数作为可选参数。而只有在默认值为null的时候，引用参数才可以作为可选参数。</p>
<p>总结下来，一个方法的声明中，参数要按照必填参数、可选参数、params参数的先后顺序声明。</p>
<p>可以忽略最后一个可选参数，或者最后n个可选参数，但是不可以随机选择省略任意的可选参数，省略必须从最后开始。</p>
<p><strong>参数类型总结：</strong></p>
<table>
<thead>
<tr>
<th>参数类型</th>
<th>修饰符</th>
<th>是否在声明时使用</th>
<th>是否在调用是使用</th>
<th>执行</th>
</tr>
</thead>
<tbody>
<tr>
<td>值参数</td>
<td>无</td>
<td></td>
<td></td>
<td>系统把实参的值复制给形参，二者在栈中位置不同</td>
</tr>
<tr>
<td>引用参数</td>
<td>ref</td>
<td>是</td>
<td>是</td>
<td>形参是实参的别名，二者在栈中位置相同</td>
</tr>
<tr>
<td>输出参数</td>
<td>out</td>
<td>是</td>
<td>是</td>
<td>在读取输出参数前必须对其写入，除此之外和引用参数类似</td>
</tr>
<tr>
<td>参数数组</td>
<td>params</td>
<td>是</td>
<td>否</td>
<td>允许传递可变数目的实参到方法</td>
</tr>
</tbody>
</table>
<h2>栈帧</h2>
<p>在调用方法的时候，内存从栈的顶部开始分配，保存和方法关联的一些数据项。这块内存叫做方法的栈帧</p>
<p>栈帧保存如下的内容：</p>
<ul>
<li>
<p>返回地址</p>
</li>
<li>
<p>为参数分配的内存</p>
</li>
<li>
<p>各种和方法调用相关的其他管理数据项</p>
<p>在方法调用的时候，整个栈帧都会压入栈。在方法退出的时候，整个栈帧都会从栈上弹出。</p>
</li>
</ul>
<p><a href="https://wyh317.github.io/img/栈帧.jpg"><img src="https://wyh317.github.io/img/%E6%A0%88%E5%B8%A7.jpg" alt="栈帧" /></a></p>
<p><a href="https://wyh317.github.io/img/栈帧.jpg">栈帧</a></p>
<h1>4.类</h1>
<p>类成员包括数据成员（保存数据）和函数成员（执行代码）
其中数据成员包括：</p>
<ul>
<li>字段</li>
<li>常量（用const修饰，包括本地常量和成员常量，本地常量声明在方法内，成员常量声明在类中）</li>
</ul>
<h2>常量</h2>
<p>成员常量表现的和静态量相似，但唯一不同的是，成员常量没有自己的存储位置，而是在编译时被编译器替换。此外，不能将成员常量声明为static。与const有着相同作用的是readonly，不同的是，const字段只能在字段的声明语句中初始化，而readonly也可以在构造函数中初始化。因此const字段的值必须在编译时确定，而randonly字段的值可以在运行时决定。</p>
<p>函数成员包括：</p>
<ul>
<li>方法</li>
<li>属性</li>
<li>构造函数、析构函数</li>
<li>运算符</li>
<li>索引</li>
<li>事件</li>
</ul>
<h2>属性</h2>
<p>属性是一组称为访问器的方法（set访问器为属性赋值，get访问器从属性中获取值）。它是类中的函数成员，因此不需为属性分配内存。</p>
<p>写入和读取属性的代码和访问字段一样。属性会根据是写入还是读取，来隐式地调用适当的访问器</p>
<p>属性通常和字段关联，一种常见的方式是在类中将字段声明为private以封装字段，并声明一个public属性用get和set访问器来控制对该字段的访问。和属性关联的字段成为后备字段</p>
<pre><code class="language-c#">class C1{
    private int TheRealValue = 10;   //后备字段：分配内存
    public int MyValue{              //属性：不分配内存
        set{
            TheRealValue = value;    //设置字段的值
        } 
        get{
            return TheRealValue;     //获取字段的值
        }
    }
}

class Program{
    static void Main(){
        //对属性的读和写如同对字段的读和写
        C1 c = new C1();
        Console.WriteLine(&quot;MyValue: {0}&quot;, c.MyValue);

        c.MyValue = 20;
        Console.WriteLine(&quot;MyValue: {0}&quot;, c.MyValue);
    }
}
Copy</code></pre>
<p>此外，属性也可以只有get访问器（只读属性），或者只有set访问器（只写属性）</p>
<pre><code class="language-c#">class RightTriangle{
    public double A = 3;
    public double B = 4;
    //只读属性，计算直角三角形的第三边
    public double Hypotenuse{
        get{
            return Math.Sqrt((A * A) + (B * B));
        }
    }
}

class Program{
    static void Main(){
        RightTriangle c = new RightTriangle();
        Console.WriteLine(&quot;Hypotenuse: {0}&quot;, c.Hypotenuse);
    }
}

上述代码将输出5
Copy</code></pre>
<h2>索引器</h2>
<p>可以认为索引器是为类的多个数据成员提供get和set访问器的属性。</p>
<pre><code class="language-c#">class Class1{
    private int Temp0;
    private int Temp1;
    //和属性不同的是，索引器有参数（索引参数），并且使用this而不是名称
    //索引器声明
    public int this [int index]{    
        get{
            return (index == 0) ? Temp0 : Temp1;
        }
        set{
            if(index == 0)
                Temp0 = value;   //value为set访问器的隐式变量
            else
                Temp1 = value;
        }
    }
}

class Example{
    static void Main(){
        Class1 a = new Class1();
        //使用索引参数0或1读取数据成员
        Console.WriteLine(&quot;T0: {0}, T1 : {1}&quot;, a[0], a[1]);
        //使用索引参数0或1对数据成员进行写入
        a[0] = 15;
        a[1] = 20;
        Console.WriteLine(&quot;T0: {0}, T1 : {1}&quot;, a[0], a[1]);
    }
}

以上代码会输出：
T0: 0, T1: 0
T0: 15, T1: 20
Copy</code></pre>
<h1>5.继承</h1>
<p>如果类OtherClass继承自SomeClass，则应按如下表示</p>
<pre><code class="language-c#">class OtherClass : SomeClass{
}
Copy</code></pre>
<p>一个类只能继承自一个基类，所有的类都是Object类的派生类</p>
<h2>屏蔽基类的成员</h2>
<p>虽然派生类不能删除它继承的任何成员，但可以用与基类成员名称相同的成员来屏蔽基类成员（如果是函数成员，则要求签名相同，签名指名称和参数列表，不包括返回类型）。此外还要使用new修饰符来告诉编译器我正在故意屏蔽继承的成员。</p>
<p>另外，即使派生类屏蔽了基类的成员，也可以使用基类访问表达式访问隐藏的继承成员。</p>
<pre><code class="language-c#">class SomeClass{    //基类
    public string Field1 = &quot;Field1--In the base class&quot;;
}
class OtherClass : SomeClass{    //派生类
    //使用new修饰符隐藏基类中的Field1字段
    new public string Field1 = &quot;Field1--In the derived class&quot;;
    public void PrintField1(){
        //访问派生类中的Field1，会输出&quot;Field1--In the derived class&quot;
        Console.WriteLine(Field1);   
        //使用基类访问来访问基类中的Field1，会输出&quot;Field1--In the base class&quot; 
        Console.WriteLine(base.Field1); 
    }
}
Copy</code></pre>
<h2>使用基类的引用</h2>
<pre><code class="language-c#">MyDerivedClass derived = new MyDerivedClass();   //创建一个派生类对象
MyBaseClass mybc = (MyBaseClass)derived;        //让基类引用指向派生类对象
Copy</code></pre>
<p>对于如上代码，派生类的引用derived可以看到完整的MyDerivedClass对象，而基类引用mybc只能看到对象的MyBaseClass部分（只能看到基类成员）
<a href="https://wyh317.github.io/img/使用基类的引用.jpg"><img src="https://wyh317.github.io/img/%E4%BD%BF%E7%94%A8%E5%9F%BA%E7%B1%BB%E7%9A%84%E5%BC%95%E7%94%A8.jpg" alt="使用基类的引用" /></a></p>
<p><a href="https://wyh317.github.io/img/使用基类的引用.jpg">使用基类的引用</a></p>
<p>另外，也可以使用基类引用调用派生类的方法，但要满足如下条件：</p>
<ul>
<li>派生类的方法和基类方法有着相同的签名和返回类型</li>
<li>基类的方法用virtual标注</li>
<li>派生类的方法用override标注
在这种情况下，当使用基类引用（mybc）调用方法时，方法会被传递到派生类执行</li>
</ul>
<p>注意：</p>
<ul>
<li>覆写（override）和被覆写的方法应该有相同的访问性</li>
<li>不能覆写static方法和非虚（virtual）方法</li>
</ul>
<p>当使用对象的基类引用调用一个覆写的方法时，方法的调用被沿着派生层次上溯执行，一直到标记为override的方法的最高派生版本。
如果在更高派生级别有该方法的其他声明，但没有被标记为override，那么它们不会被调用。</p>
<h2>构造函数</h2>
<h3>构造函数初始化语句</h3>
<p>两种形式：</p>
<ul>
<li>关键字base：指明使用哪一个基类的构造函数</li>
<li>关键字this：指明使用哪一个当前类的构造函数
以下构造函数使用了构造函数初始化语句，构造函数初始化语句指明了要使用第一个参数是string，第二个参数是int型的那个基类构造函数</li>
</ul>
<p>当声明一个不带构造函数初始化语句的构造函数时，它实际上是使用了无参数的基类构造函数。</p>
<pre><code class="language-c#">public MyDerivedClass(int x, string s) : base(s, x){

}
Copy</code></pre>
<p>如下代码中的MyClass类包含一个有一个int型参数的构造函数，这个构造函数使用了同一个类中具有两个参数的构造函数，并为第二个参数提供了一个默认值</p>
<pre><code class="language-c#">public MyClass(int x) : this(x, &quot;Using Default String&quot;){

}
Copy</code></pre>
<p>如果一个类有好几个构造函数，并且它们都需要在构造对象的过程中执行一些公共代码。这时可以把公共代码提取出来作为一个构造函数，被其他所有的构造函数作为构造函数初始化语句使用。</p>
<h2>访问级别</h2>
<p>类有两种访问级别：</p>
<ul>
<li>public：可以被任何程序集中的代码访问</li>
<li>internal：默认的访问级别，仅可以被自己所在的程序集中的类看到</li>
</ul>
<p>类中的成员有5种访问级别：</p>
<ul>
<li>私有的（private）：只能被自己类中的成员访问，不能被其他的类访问，即使是继承自它的类也不行</li>
<li>公有的（public）：所有的类都可以自由访问</li>
<li>受保护的（protected）：和private类似，唯一不同的是，它允许该类的派生类来访问</li>
<li>内部的（internal）：对程序集内部的所有类可见，对程序集外部的所有类不可见</li>
<li>受保护内部的（protected internal）：相当于internal与protected的并集，即对程序集内部的类可见，也对继承自该类的类可见。</li>
</ul>
<h2>抽象成员</h2>
<p>类似于Java中的抽象方法。它使用abstract标记，并且必须是函数成员（方法、属性、事件、索引）。不能有实现代码块，抽象成员的实现用分号表示。即每一个抽象成员的声明后都要带一个分号</p>
<p>如：以下声明了两个抽象成员，一个名为PrintStuff的抽象方法和一个名为MyProperty的抽象属性</p>
<pre><code class="language-c#">abstract public void PrintStuff(string s);
abstract public int MyProperty{
    get;    //分号代替实现
    set;
}
Copy</code></pre>
<ul>
<li>抽象类：只能被继承，不能用来创建实例，用abstract修饰符标注</li>
<li>密封类：与抽象类相反，只能被用来创建实例，不能被继承。用sealed修饰符标注</li>
</ul>
<h1>语句</h1>
<h2>操作符重载</h2>
<p>如果面对一个用户自定义的类或结构，运算符就会不知道如何取处理它。运算符重载允许用户自己定义C#运算符来操作自定义类型的操作数。</p>
<ul>
<li>为类或结构重载一个运算符x，可以声明一个名称为<code>operator x</code>的方法并实现它的行为（如<code>operator +</code>和<code>operator -</code>等）。一元运算符的重载方法带有一个单独的class或struct类型的参数，二元运算符重载的方法带有两个参数，其中至少有一个是class或struct类型。</li>
<li>声明必须同时使用static和public的修饰符</li>
<li>运算符必须要是要操作的类或结构的成员</li>
</ul>
<p>如下代码声明了LimitedInt类的两个重载的运算符：一个是加运算符，另一个是取负运算符</p>
<pre><code class="language-c#">class LimitedInt Return{
    public static LimitedInt operator + (LimitedInt x, double y){
        LimitedInt li = new LimitedInt();
        li.TheValue = x.TheValue + (int)y;
        return li;
    }

    public static LimitedInt operator - (LimitedInt x){
        LimitedInt li = new LimitedInt();
        li.TheValue = 0;
        return li;
    }
}
Copy</code></pre>
<h2>标签语句</h2>
<p>标签语句由一个标识符后面跟着一个冒号再跟着一条语句组成，它有如下的形式：<code>Identifier: Statement</code>。这条语句在执行时与只有Statement的语句相同，加一个标签的目的只是为了允许程序从其他位置跳转到这个标签所在的位置。</p>
<ul>
<li>因为标签有自己的声明空间，所以标签语句中的标识符可以是任意有效的标识符（可以与本地变量名相同）。</li>
<li>标签的作用域仅在块内部</li>
</ul>
<p>goto语句可以跳到它本身所在的块中的任何标签语句，或跳出到任何它被嵌套的块内的标签语句。<code>goto Indentifier</code></p>
<h1>数组</h1>
<h2>一维数组和矩形数组</h2>
<pre><code class="language-c#">int[] intArr1 = new int[15];   //声明一维数组
int[,] intArr2 = new int[5, 10];  //声明二维数组
int var2 = intArr[2, 3];      //从二维数组中读值

int[] intArr = new int[]{10, 20, 30, 40};   //初始化一维数组
int[,] intArr2 = new int[,]{{0, 1, 2}, {10, 11, 12}}; //初始化二维数组
Copy</code></pre>
<h2>交错数组</h2>
<p>交错数组是<strong>数组的数组</strong>，与矩阵数组不同，交错数组的子数组的元素个数可以不同</p>
<pre><code class="language-c#">//实例化顶层数组，不能在声明语句中初始化顶层数组之外的数组长度
int[][] Arr = new int[3][];  
//实例化子数组
Arr[0] = new int[]{1,2,3};
Arr[1] = new int[]{4,5,6};
Arr[2] = new int[]{7,8,9};
Copy</code></pre>
<h2>foreach语句</h2>
<p>注意：迭代变量item是只读的，不能修改。</p>
<pre><code class="language-c#">int[] arr1 = new int[]{1,2,3};
foreach(int item in arr1)
    Console.WriteLine(&quot;Item Value: {0}, item&quot;);</code></pre>