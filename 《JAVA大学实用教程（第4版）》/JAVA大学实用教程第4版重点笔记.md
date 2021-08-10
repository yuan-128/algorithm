笔记的内容：

1. 最新理解或想明白的；
2. 自己做了实验的，附加上实验。有实验的更能辅助记忆。最好是对比实验.

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

   

