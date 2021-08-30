1. 字符串常量池、堆、栈

   栈（stack）：主要保存基本类型（或者叫内置类型）（char、byte、short、int、long、float、double、boolean）和对象的引用，数据可以共享，速度仅次于寄存器（register），快于堆。 

   堆（heap）：用于存储对象

   字符串常量池：字符串常量是对象、常量

   ![](/String/0.png)

   备注：

   1. 分清楚对象本身和对象的引用。对象是实体，对象的引用是指针。字符串实体是不可变的常量，但其引用是可变的变量，引用可以更改指向的字符串常量；
   2. 分清楚常量和对象："abc"可以理解为基本数据类型的数字的字面量；String s="abc"，可以等同于int i=3；而用到new之后，则不再是基本数据类型，属于引用类型的对象，要按照JVM的规则把对象统一存放在堆中。

2. 创建几个对象的问题：

   ```
   String str="abc";
   //1个，在字符串常量池。"abc"本身就是一个存放在字符串常量池中的对象。str是一个指向"abc"的一个指针。所以只创建了一个对象，就是字符串常量池中的"abc"；
   
   String str1="abc";
   String str2="abc";
   //2个指针（引用），1个字符串常量对象；
   
   String str= new String("abc");
   //2个，分别在字符串常量池和堆中；new是在堆中用字符串常量对象再创建一个对象。这涉及到Java的内存设计;
   
   String s1 = new String(“abc”); 
   String s2 = new String(“abc”); 
   //3个；
   
   String str1 = "abc";
   String str2 = "ab" + "c"; 
   str1==str2是true吗？
   是。因为String str2 = "ab" + "c"会查找常量池中是否存在内容为"abc"字符串对象，如存在则直接让str2引用该对象，显然String str1 = "abc"会在常量池中创建"abc"对象，所以str1引用该对象，str2也引用该对象，所以str1==str2
   
   String str1 = "abc";
   String str2 = "ab";
   String str3 = str2 + "c"; 
   str1==str3
   //结果：false；
   //解释：因为String str3 = str2 + "c"涉及到变量（不全是常量）的相加，所以会生成新的对象，其内部实现是先new一个StringBuilder，然后 append(str2),append("c");然后让str3引用toString()返回的对象
   
   String str=str+"def";
   //
   ```

   

参考资料：

1. [Java String创建了几个对象]((https://www.cnblogs.com/wulouhua/p/3875630.html))
2. [Java常量池](https://blog.csdn.net/qq_41376740/article/details/80338158)