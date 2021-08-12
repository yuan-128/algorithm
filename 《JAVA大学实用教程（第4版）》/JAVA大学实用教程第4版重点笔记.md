笔记的内容：原则上每一个点下面都应该跟一个例子；

## 第一章

### 第一节

## 第二章

### 2.3基本数据类型的转换

1. 整型和字符型的相互转换：

   int = char+/-char（结果会出现<0 >65536的情况）

   int = （byte、short、int）op（byte、short、int）（同上）

   ```
   char c='呀';
   System.out.println(c);
   System.out.println(c+' ');//'呀'的ASCII和' '的ASCII值的和为21600
   //把两个char类型的变量相加减结果时int类型的，因为可能出现负数。
   int m=100;
   System.out.println(m);
   System.out.println(m+' ');
   
   结果：
   呀
   21600
   100
   132
   ```

2. 查看字符的ASCII：(int)'字符'

   查看数字对应的字符：(char)数字

3. 浮点类型的相互转换：

   double转ffloat无精度损失：（高转低无精度损失）

   ```
           double q=1.314;
           float w=(float)q;
   //        System.out.printf("%.10f",q);//只要截断，必然是四舍五入，结果相同
   //        System.out.println();
           System.out.println(q);
   //        System.out.printf("%.10f",w);
   //        System.out.println();
           System.out.println(w);
           结果：
           1.314
           1.314
   ```

   float转double有精度损失：（低转高有精度损失）

   ```
           float q=1.314f;
           double w=q;
   //        System.out.printf("%.10f",q);//只要截断，必然是四舍五入，结果相同
   //        System.out.println();
           System.out.println(q);
   //        System.out.printf("%.10f",w);
   //        System.out.println();
           System.out.println(w);
   结果：
   1.314
   1.3140000104904175
   ```

4. 

### 2.5 数组

1. 输出数组的引用：

   ```
   package Package2;
   class P2Class1{
       public static void main(String[] args) {
           char[] a=new char[26];
           int i;
           for (i=0;i<26;i++)
               a[i]=(char)(i+97);
           System.out.println(a+"");
   
       }
   }
   结果：
   [C@1b6d3586
   ```

2. 

## 第3章 运算符、表达式和语句

### 3.5 移位运算符

　　对于byte或short类型数据，a<<n的运算结果是int类型，当进行a<<2运算时，计算系统先将a升级为int类型数据（对于正数将高位用0填充，负数用1填充），再进行移位

### 3.8 instanceof运算符

　　instanceof 严格来说是Java中的一个双目运算符，用来测试一个对象是否为一个类的实例，用法为：

```
boolean result = obj instanceof Class
```

　　其中 obj 为一个对象，Class 表示一个类或者一个接口，当 obj 为 Class 的对象，或者是其直接或间接子类，或者是其接口的实现类，结果result 都返回 true，否则返回false。

　　注意：

1. 编译器会检查 obj 是否能转换成右边的class类型，**如果不能转换则直接报错**，如果不能确定类型，则通过编译，具体看运行时定。
2. 如果 obj 为 null，那么将返回 false。

## 第四章

### 4.6 成员变量

1. 类变量和实例变量

   ```
   //用法举例
   
   ```

2. 常量

   - final修饰
   - 大写
   - 不占内存，声明时必须初始化
   - 不可更改（和static的区别。static表示所有对象共同拥有可以更改，final表示一人一个，不可更改。）

   ```
   //用法举例
   class Tom{
       final int MAX=100;
       static final int MIN=20; //通过类名访问，不可更改
   }
   ```

   总结：访问权限最靠前，final最靠近；

   - 成员变量声明：**[访问权限]　　[static]　　[final]　　[基本数据类型]**
   - 方法声明：**[访问权限]　　[static]　　［final | abstract］　　返回类型　　方法名　　（　[参数1]　　[参数2] ···）**
   - 类声明：**[访问权限：public|友好的]　　[final | abstract]　　class**



### 4.8 方法重载

1. 多态性：方法重载、方法重写（继承，上转型对象）、接口回调；

   方法重载（同名不同参）：方法名相同，参数类型或个数不同。返回类型和参数名不参与比较；

   方法重写（同名不同类）：父类的某个实例方法被其子类重写时，可以各自产生自己的功能行为，指同一个操作被不同类型对象调用时可能产生不同的行为。

   接口回调：用法和思想同上转型对象；

### 4.12 访问权限

1. private修饰的成员变量及方法：类内可创建对象访问，类外不可创建对象访问；

   ```
   //eg:类外创建的对象不可访问private修饰的成员变量和方法
   class P2Class1
   {
       private int a=0;
       private void fun()
       {
           a++;
       }
   }
   class P2Class11 {
       public static void main(String[] args) {
           P2Class1 demo=new P2Class1();
           System.out.println(demo.a);
           //Error:java:a在P2Class1中是private访问控制
           demo.fun();
           //Error:java:fun()在P2Class1中是private访问控制
           System.out.println(demo.a);
           //Error:java:a在P2Class1中是private访问控制
       }
   }
   
   
   
   
   ```

   ```
   //eg:只有在类内创建的对象才可以访问private修饰的成员变量和方法
   class P2Class1 {
       private int a=0;
       private void fun()
       {
           a++;
       }
       public static void main(String[] args) {
           P2Class1 demo=new P2Class1();
           System.out.println(demo.a);
           demo.fun();
           System.out.println(demo.a);
       }
   }
   ```

2. public修饰的成员变量和方法：在**任何一个类**中创建了一个对象后，该对象都能访问自己的public变量和类中的public方法。

3. 友好变量和友好方法：不用private、public、protected修饰的成员变量和方法被称为友好变量和友好方法，同包不同类中创建的对象可以访问，不同包的类中创建的对象不可以访问。

   ```
   //eg:不同包的类中创建的对象不可以访问；
   package Package1;
   //P1Class1是包Package1中的类
   public class P1Class1 {
       int a=1;
       void fun()
       {
           a++;
       }
   }
   
   package Package2;
   //P2Class1是包Package2中的类，在不同的保重，所以首先需要导入Package1包中的类P1Class1，才可以创建P1Class1的对象。但由于P1Class1的成员变量和方法都是友好的，所以demo.a和demo.fun()会报错：a和fun()在类P1Class1中不是公共的；无法从外部程序包中对其进行访问；
   import Package1.*;
   class P2Class1 {
   
       public static void main(String[] args) {
           P1Class1 demo=new P1Class1();
           System.out.println(demo.a);
           demo.fun();
           System.out.println(demo.a);
       }
   }
   
   ```

4. protected修饰的成员变量和方法：不涉及继承时同友好的；涉及继承时，protected允许子对象访问不同包中的父对象用protected修饰的成员变量和方法，友好的不允许访问；

   ```
   //eg：涉及继承时，protected和友好的对比
   //protected修饰的：
   package Package1;
   public class P1Class1 {
       protected int a=1;
       protected void fun()
       {
           a++;
       }
   }
   
   package Package2;
   import Package1.P1Class1;
   class P2Class1 extends P1Class1{
       public static void main(String[] args) {
           P2Class1 demo1=new P2Class1();//子类创建的对象
           System.out.println(demo1.a);
           demo1.fun();
           System.out.println(demo1.a);
       }
   }
   结果：1 2
   ```

   ```
   //default修饰的（友好）：
   package Package1;
   public class P1Class1 {
       int a=1;
       void fun()
       {
           a++;
       }
   }
   
   package Package2;
   import Package1.P1Class1;
   class P2Class1 extends P1Class1{
       public static void main(String[] args) {
           P2Class1 demo1=new P2Class1();
           System.out.println(demo1.a);
           demo1.fun();
           System.out.println(demo1.a);
       }
   }
   结果：a和fun()在Package1.P1Class1中不是公共的；无法从外部程序包中对其进行访问
   ```

5. public类与友好类

   ```
   //public类
   package Package1;
   public class P1Class1 {
       public int a=1;
       public void fun()
       {
           a++;
       }
   }
   
   package Package2;
   import Package1.P1Class1;
   class P2Class1 extends P1Class1{
       public static void main(String[] args) {
           P1Class1 demo=new P1Class1();
           System.out.println(demo.a);
           demo.fun();
           System.out.println(demo.a);
       }
   }
   结果：1 2
   
   //default类（友好）
   package Package1;
   
   class P1Class1 {
       public int a=1;
       public void fun()
       {
           a++;
       }
   }
   
   package Package2;
   import Package1.P1Class1;
   class P2Class1 extends P1Class1{
       public static void main(String[] args) {
           P1Class1 demo=new P1Class1();
           System.out.println(demo.a);
           demo.fun();
           System.out.println(demo.a);
       }
   }
   结果：类Package1.P1Class1在Package1中不是公共的；无法从外部程序包中对其进行访问
   ```

6. 1

### 4.17  反编译和文档生成器

1. 使用SDK提供的反编译器javap.exe可以将字节码反编译为源码，查看源码类中的方法和成员

   用法：

   `javap -(public | protected | package | private) `用于指定显示哪种级别的类成员

   ```
   public class A
   {
   	public int a=0;
   	int b=1;
   	void fun()
   	{}
   	public static void main(String [] args)
   	{
   		int a=1;
   		int b=10;
   		a++;
   		b--;
   		System.out.println(a);
   		System.out.println(b);
   	}
   }
   
   cmd:
   D:\>javap A
   Compiled from "A.java"
   public class A {
     public int a;
     int b;
     public A();
     void fun();
     public static void main(java.lang.String[]);
   }
   
   D:\>javap -public A
   Compiled from "A.java"
   public class A {
     public int a;
     public A();
     public static void main(java.lang.String[]);
   }
   ```

2. 

## 第五章 继承、接口和泛型

### 5.1 父类和子类

1. Java不支持多重继承，即子类只能有一个父类。
2. 0



### 5.2 子类对象的构造过程

1. 当子类的构造方法创建一个子类的对象时，子类的构造方法总是先调用父类的某个构造方法。默认调用父类的无参构造方法；如果父类没有无参的构造方法，则会报错：

   ```
   //父类没有无参的构造方法，则会报错：
   package Package1;
   class Father
   {
       Father(int n) { }
   }
   class Son extends Father
   {
   
   }
   public class P1Class1
   {
       public static void main(String[] args) {
           Son son=new Son();
       }
   }
   结果：
   Error:(6, 1) java: 无法将类 Package1.Father中的构造器 Father应用到给定类型;
     需要: int
     找到: 没有参数
     原因: 实际参数列表和形式参数列表长度不同
   ```

2. 子类和父类在同一包中的继承性

   如果子类和父类在同一个包中，那么子类自然地继承了其父类中不是private的成员变量作为自己的成员变量，也自然地继承了父类中不是private的方法作为自己的方法。继承的成员变量以及方法的访问权限保持不变。

3. 子类和父类不在同一包中的继承性

   如果子类和父类不在同一个包中，那么子类继承了父类的protected、public成员变量作为子类的成员变量，并且继承了父类的protected、public方法，继承的成员变量或方法的访问权限保持不变，但子类不能继承父类的友好变量和友好方法。

### 5.4 成员变量隐藏和方法重写

1. 成员变量的隐藏

   同名（不必类型相同）就可以隐藏继承的成员变量。

   ```
   package Package1;
   class A
   {
       int i=100;
   }
   class B extends A
   {
       double i=3.14;
   }
   public class Class1
   {
       public static void main(String[] args) {
           B b=new B();
           System.out.println(b.i);
       }
   }
   结果：3.14
   ```

   

### 5.5 关键字super

1. 方法隐藏：当子类中定义了一个方法，并且这个方法的**返回类型**、**名字**、**参数个数和类型**与父类的某个方法完全相同时（访问权限不列入比较），子类从父类继承的这个方法将被隐藏。



### 5.6 final类和final方法

1. 类的修饰：public、友好的、final、adstract（5.9）；

   public、友好的：public修饰的类可以在不同包的类中import之后创建对象，友好的修饰的类只能在同包中创建对象；

   final：final类不能被继承，即不能有子类；

   final也可以修饰成员变量和方法。final修饰的成员变量不可更改，修饰的方法不可重写；

   总结：final修饰的成员变量

###　5.7　对象的上转型对象

1. 上转型对象不是父类创建的对象，而是子类对象的”简化“形态，它不关心子类新增的功能，只关心子类继承和重写的功能。

   ```
   package Package1;
   class A
   {
       void cry() {}
   }
   class B extends A
   {
       void cry()
       {
           System.out.println("BBB");
       }
   }
   class C extends A
   {
       void cry()
       {
           System.out.println("CCC");
       }
   }
   public class Class1
   {
       public static void main(String[] args) {
           A a;
           B b=new B();
           C c=new C();
           b.cry();
           c.cry();
   
           a=b;
           a.cry();
           a=c;
           a.cry();
       }
   }
   结果：
   BBB
   CCC
   BBB
   CCC
   ```



### 5.9 抽象类

1. 抽象类特点：
   - 抽象类中可以有抽象方法，也可以有非抽象方法。对于抽象方法，只允许声明，不允许实现，不允许使用final和abstract同时修饰一个方法。
   - 抽象类不能用new运算创建对象。非抽象子类必须重写父类的抽象方法，给出方法体。即在子类中将抽象方法重新声明，但必须去掉abstract修饰，同时保证声明的返回类型，方法名字、参数个数和类型与父类的抽象方法完全相同。这就是为什么不允许使用final和abstract同时修饰一个方法的原因。（final修饰的成员变量不可更改，修饰的方法不可重写；）
   - 抽象类不能创建对象，但他的非抽象子类必须重写其中的全部抽象方法，这样可以让抽象类声明的对象成为其子类对象的上转型对象，并调用子类重写的方法。

### 5.11 接口

　　需求：Java不支持多继承性，即一个类只能有一个父类。单继承性的优点：简单、易于管理程序。为了克服单继承性的缺点，提出了**接口**，一个类可以实现多个接口。

　　总结：

- 接口是更加抽象的抽象的类 ：抽象类里的方法可以有方法体，接口里的所有方法都没有方法体（只关注功能，不关注功能的具体实现细节，继承关注的是类之间的关系）。
- 接口体现了程序设计的多态和高内聚低偶合的设计思想。
- 接口和继承的关系可以理解为父亲和长辈的关系，只能有一个父亲，但可以有多个长辈。

1. 接口的声明和使用

   - interface 接口的名字

   - 接口体：常量（public static final修饰） + public abstract 返回类型 方法名();

     ```
     interface Printable{
     	final int MAX = 100;//省略了public static，static可有可无。每个对象有一个常量和所有对象共享一个常量，对编程人员来说是透明的
     	void add();//省略了public abstract。
     	float sum(float x,float y);//同上
     }
     ```

   - 接口的使用
     - 类实现接口：`class A implements Printable，Addable`
     - 继承+接口：`class Dog extends Animal implements Eatable，Sleepable`
     - 如果一个类实现某个接口，那么必须实现该接口的所有方法，即为这些方法提供方法体。实现接口的方法时，方法的名字、返回类型、参数个数及类型必须与接口中的完全一致。接口中的方法默认是 public abstract（可省略），实现该方法时，必须用public修饰。
     - Java提供的接口都在相应的包中，通过引入包可以使用Java提供的接口，也可以自己定义接口，一个Java源文件就是由类和接口组成的。
     - 接口可以用public和友好的修饰。public接口可以被任何一个类使用（import导入即可），友好接口可以被同一包中的类使用（不同的包import无法导入）。
     - 接口可以通过关键字extends声明一个接口是另一个接口的子接口。由于接口中的方法和常量都是public的，子类接口将继承父类接口中的全部方法和常量。
   - 

### 5.15 内部类

　　类可以有三种成员：成员变量、方法、内部类；

### 5.16 匿名类

- 匿名类一定是内部类

- 匿名类的主要用途就是向方法的参数传值。

  假设 f（B x）是一个方法

  ```
  void f(B x){
  	x.方法;//x调用B类中的方法；
  }
  ```

  其中的参数是B类对象，那么在调用方法 f() 时可以向 f() 的参数x传递一个匿名对象：

  ```
  f(new B()
  	{
  		匿名类的类体，继承B类的方法或重写B类的方法
  	}
  );//调用方法f()
  ```

  

