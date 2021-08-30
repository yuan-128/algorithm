## 选择

- 字节流可以读取任何文件 ；读取二进制文件的时候，选择字节流（视频，音频，doc，ppt）
- 读取待解析文本文件的时候：选择字符流（假如有解析文件的内容的需求，比如逐行处理，则采用字符流，比如txt文件） 

例子：

1. 复制（文件.txt/.pdf、图片、视频）

   ```
   package Package2;
   import java.io.*;
   class Test {
       public static void main(String[] args) throws IOException {
           long s=System.currentTimeMillis();
           FileInputStream fis=new FileInputStream("test/mp4/N.mp4");
           FileOutputStream fos=new FileOutputStream("N1.mp4");
           byte[] b=new byte[1024];
           int len;
           while ((len=fis.read(b))!=-1)
           {
               fos.write(b,0,len);
           }
           fos.close();
           fis.close();//先关闭写，再关闭读。写完了一定读完了，读完了未必写完了。
           long e=System.currentTimeMillis();
           System.out.println((e-s));
   
       }
   }
   ```

   