## 第二章

1. 【例3-5】分别用while和do-while循环计算常数e（e=1+1/1+2/2!+3/3!+···）的近似值。

   重点：利用  上一项的值/i  的计算方法可以节约计算时间。否则一项一项地去计算，最后结果为：Infinity；

   ```
   public class Test
   {
       public static void main(String[] args)
       {
           int i=1;
           double e=1;
           double temp=1;
           while (i<=1000)
           {
               temp=temp/i;
               e+=temp;
               i++;
           }
           System.out.println(e);
   
           i=1;
           e=1;
           temp=1;
           do {
               temp=temp/i;
               e+=temp;
               i++;
           }while (i<=10000);
           System.out.println(e);
       }
   }
   ```

2. 【例3-8】使用while循环和折半查找一个整数是否在一个排序的int类型数组中。

   重点：

   ```
   import java.math.BigInteger;
   import java.util.Scanner;
   
   import static java.lang.StrictMath.pow;
   
   public class Test
   {
       public static void main(String[] args)
       {
           int[] a={1,3,5,7,9};
           int l,r,m;
           Scanner read = new Scanner(System.in);
           int f;
           while (read.hasNextInt())
           {
               int n=read.nextInt();
               f=0;
               l=0;
               r=a.length-1;
               while (l<=r)//!!
               {
                   m=(l+r)/2;
                   if (a[m]==n)
                   {
                       f=1;
                       System.out.println("Yes");
                       break;
                   }
                   else if (n<a[m])
                   {
                       r=m-1;//!!
                   }
                   else
                   {
                       l=m+1;//!!
                   }
               }
               if (f==0)
                   System.out.println("没找到");
           }
   
       }
   }
   
   ```

   

3. 补充：50的阶乘 大数字的存储

   参考资料：

   1. [java 50的阶乘 大数字的存储](https://blog.csdn.net/daxi_gua/article/details/82764668)

   ```
   public class Test
   {
       public static void main(String[] args)
       {
       	//方法一
           int[] a=new int[100];
           int i,j;
           int temp=0;
           a[a.length-1]=1;
           for (i=1;i<=50;i++)
           {
               for (j=a.length-1;j>=0;j--)
               {
                   a[j]=a[j]*i;
               }
               for (j=a.length-1;j>0;j--)
               {
                   a[j-1]=a[j-1]+a[j]/10;
                   a[j]=a[j]%10;
               }
           }
           int f=0;
           for (i=0;i<a.length;i++)
           {
               if (a[i]!=0)
                   f=1;
               if (f==1)
                   System.out.print(a[i]);
   
           }
           System.out.println();
           
           //方法二
           BigInteger sum=new BigInteger("1");
   
           for (i=1;i<=50;i++)
           {
               String str=String.valueOf(i);
               sum=sum.multiply(new BigInteger(str));
           }
           System.out.println(sum);
   
       }
   }
   ```

