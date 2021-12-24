---
title: 剑指offer(3)——链表（共8道题目）
date: 2020-09-09 10:28:51
tags: 剑指offer
categories: 剑指offer
---

参考资料：

[剑指offer题目汇总](https://www.cnblogs.com/gzshan/p/10910831.html)

<!--more-->

# 链表（共8道题目）

模板：

　　**题目描述：**

　　**解题思路**：

　　**注意问题**：

　　**补充知识点**：

---

[3、从尾到头打印链表](#3)（09.09）

[14、链表中倒数第k个结点](#14)（09.10）

[15、反转链表](#15)（09.11）

[16、合并两个排序的链表](#16)（09.12）

[25、复杂链表的复制](#25)（09.13）

[36、两个链表的第一个公共结点](#36)（09.14）

[55、链表中环的入口结点](#55)（09.15）

[56、删除链表中重复的结点](#56)（09.16）

---

<p id='3'>3、从尾到头打印链表</p>

　　**题目描述：**

  输入一个链表，按链表值从尾到头的顺序返回一个ArrayList。

　　**解题思路**：栈、递归

　　**注意问题**：

　　1.声明的list要在方法之外，否则递归过程中用到的不是一个list；

　　2.注意判空和递归结束的条件；

　　**补充知识点**：java链表、c语言结构体节点和java节点的对比

```java
//java
/**
*    public class ListNode {
*        int val;
*        ListNode next = null;
*
*        ListNode(int val) {
*            this.val = val;
*        }
*    }
*
*/
import java.util.ArrayList;
public class Solution {
    ArrayList<Integer> list=new ArrayList<Integer>();
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        if(listNode==null)
            return list;
        if (listNode!=null)
        {
            printListFromTailToHead(listNode.next);
            list.add(listNode.val);
        }
        return list;
    }
}
```

<p id='14'>14、链表中倒数第k个结点</p>

　　**题目描述：**

  输入一个链表，输出该链表中倒数第k个结点。为了符合习惯，从1开始计数，即链表的尾结点是倒数第1个节点。例如，一个链表有6个结点，从头结点开始，它们的值依次是1,2,3,4,5,6。则这个链表倒数第三个结点是值为4的结点。

　　**解题思路**：双指针解法

　　**注意问题**：

　　1.注意特殊情况的判断：`if(head==null)`、`if(k==0)`；

　　2.进行同时后移之前，必须判断：`k2!=null`；如果第一个for循环不能有效进行k-1次，同时后移是没有意义的；

　　3.注意引用数据类型（类c语言指针）的初始化：`k1=-head`；

　　**补充知识点**：

```java
//java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
    public ListNode FindKthToTail(ListNode head,int k) {
        if(head==null)
            return head;
        if(k==0)
            return null;
        ListNode k1,k2;
        int i;
        k1=k2=head;
        for (i=1;i<k;i++)
            k2=k2.next;
        if(k2!=null)
        {
            k1=head;
            while (k2.next!=null)
            {
                k2=k2.next;
                k1=k1.next;
            }
            return k1;
        }
        return null;
    }
}
```

<p id='15'>15、反转链表</p>

　　**题目描述：**

  输入一个链表，反转链表后，输出新链表的表头。

　　**解题思路**：迭代、递归、[图解](https://www.jianshu.com/p/f7534f8d7bf2)

　　**注意问题**：

　　1.最后一步：`second.next=first;`要深刻理解；

　　2.返回的是p2，判空的是p3；

　　**补充知识点**：

```java
//java
    //方法一：三指针
    public ListNode ReverseList(ListNode head) {
        if(head==null)
            return null;
        ListNode first=null; 
        ListNode second=head;
        ListNode third=head.next;
        while(third!=null){ 
            second.next=first; //三指针之间的变换
            first=second;
            second=third;
            third=third.next;
        }
        second.next=first;
        return second;
    }

    //方法二：递归
    public ListNode ReverseList(ListNode head) {
    	 if(head==null||head.next==null)
            return head;
        ListNode temp=ReverseList(head.next);
        head.next.next=head;
        head.next=null;
        return temp;   
    }
```

<p id='12'>16、合并两个排序的链表</p>

　　**题目描述：**

  输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

　　**解题思路**：递归、非递归；

　　**注意问题**：

​		1.采用递归方式时，head的定义位于方法内，这样每次递归都会重新定义一个head，最外层的递归调用的head不会变；

​		2.采用非递归方式时，当跳出循环：`while (list1!=null && list2!=null)`之后，剩下的链表应该用 if 连上，不能用 while ；

　　**补充知识点**：

```java
//java
//递归
public class Solution {
    public ListNode Merge(ListNode list1,ListNode list2) {
        if (list1==null)
            return list2;
        if (list2==null)
            return list1;
        ListNode head=null;
        if (list1.val<=list2.val)
        {
            head=list1;
            head.next=Merge(list1.next,list2);
        }
        else
        {
            head=list2;
            head.next=Merge(list1,list2.next);
        }
        return head;
    }
}
//非递归：设立空头节点
    public ListNode Merge(ListNode list1,ListNode list2) {
    	if(list1==null)
            return list2;
        if(list2==null)
            return list1;
        ListNode head=new ListNode(-1);//头节点
        ListNode thehead=head;
        while(list1!=null && list2!=null){
            if(list1.val<=list2.val){
                thehead.next=list1;
                list1=list1.next;
            }else{
                thehead.next=list2;
                list2=list2.next;
            }
            thehead=thehead.next;
        }
        if(list1!=null)  //归并完需要检查哪个链表还有剩余
            thehead.next=list1;
        if(list2!=null)
            thehead.next=list2;
        return head.next;
    }
//非递归：不设空头节点
public class Solution {
    public ListNode Merge(ListNode list1,ListNode list2) {
        if (list1==null)
            return list2;
        if (list2==null)
            return list1;
        ListNode head=null;
        ListNode end=null;
        if (list1.val<list2.val)
        {
            head=end=list1;
            list1=list1.next;
        }
        else 
        {
            head=end=list2;
            list2=list2.next;
        }
        while (list1!=null && list2!=null)
        {
            if (list1.val<list2.val)
            {
                end.next=list1;
                end=end.next;
                list1=list1.next;
            }
            else 
            {
                end.next=list2;
                end=end.next;
                list2=list2.next;
            }
        }
        if (list1!=null)
            end.next=list1;
        if (list2!=null)
            end.next=list2;
        return head;
    }
}
```

<p id='25'>25、复杂链表的复制</p>

　　**题目描述：**

  输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的head。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）。

　　**解题思路**：

  本题有以下三种解法：

  第一种：先按照next复制，然后依次添加random指针，添加时需要定位random的位置，定位一次需要一次遍历，需要O（n^2）的复杂度。

  第二种：先按照next复制，然后用一个hashmap保存原节点和复制后节点的对应关系，则用O（n）的空间复杂度使时间复杂度降到了O（n）。

   第三种（最优方法）：同样先按next复制，但是把**复制后的节点放到原节点后面**，则可以很容易的添加random，最后按照奇偶位置拆成两个链表，时间复杂度O（n），不需要额外空间。

　　**注意问题**：

​		链表题目的核心问题在于判空，跟参考程序写的不一样无所谓，只要注意链表的条件判断即刻。

　　**补充知识点**：

```java
//java
/*
public class RandomListNode {
    int label;
    RandomListNode next = null;
    RandomListNode random = null;

    RandomListNode(int label) {
        this.label = label;
    }
}
*/
public class Solution {
    public RandomListNode Clone(RandomListNode pHead)
    {
        if (pHead==null)
            return null;
        copyNodes(pHead);
        addRandom(pHead);
        return reconnectNodes(pHead);
    }
    //先按next复制，但是把复制后的节点放到对应原节点后面
    public void copyNodes(RandomListNode pHead)
    {
        RandomListNode p;
        p=pHead;
        while (p!=null)
        {
            RandomListNode q=new RandomListNode(p.label);
            q.next=p.next;
            p.next=q;
            p=p.next.next;
        }
    }
    //依次添加random指针
    public void addRandom(RandomListNode pHead)
    {
        RandomListNode p,q;
        p=pHead;
        q=p.next;
        while (p!=null)
        {
            if(p.random!=null)
                q.random=p.random.next;
            p=p.next.next;
            if (p!=null)//这是重点.指针在循环内部更新完之后直接用新值操作容易出界。
                q=p.next;//把这句放在循环的最开始就无需进行判断了；
        }
    }
    //按照奇偶位置拆成两个链表
    public RandomListNode reconnectNodes(RandomListNode pHead)
    {
        RandomListNode head2,p1,p2;
        p1=pHead;
        p2=head2=pHead.next;
        while (p1.next.next!=null)
        {
            p1.next=p1.next.next;
            p2.next=p2.next.next;
            p1=p1.next;
            p2=p2.next;
        }
        p1.next=p1.next.next;//上一个while结束之后，p1.p2分别指向最后两个节点，此时要更新p1.next保证原链表的原貌。
        return head2;
    }
}
```

<p id='36'>36、两个链表的第一个公共结点</p>

　　**题目描述：**

​		输入两个链表，找出它们的第一个公共结点。

　　**解题思路**：

​		方法一：针对每一个pHead1的节点，遍历pHead2的所有节点，寻找引用相等的情况。时间复杂度：O(nm)；

​		方法二：借助辅助栈，倒着遍历。用O(n+m)的时间复杂度换得了O(n+m)的时间复杂度,相当于用空间换区了时间效率的提升；

​		方法三：将两个链表设置成一样长，时间复杂度：O(n+m)；

​		方法四：**将两个链表拼接起来。** 将两个链表进行拼接，一个链表1在前链表2在后，另一个链表2在前链表1在后，则合成的两个链表一样长，然后同时遍历两个链表，就可以找到公共结点，时间复杂度同样为O(m+n)。

​		方法四证明：

![](剑指offer(3)——链表（共8道题目）/1.png)

　　1—>2—>3—>6—>7—>4—>5—>　6　—>7

　　4—>5—>6—>7—>1—>2—>3—>　6　—>7

　　假定 List1长度: a+n  List2 长度:b+n, 且 a<b；那么 p1 会先到链表尾部, 这时p2 走到 a+n位置,将p1换成List2头部；接着p2 再走b+n-(n+a) =b-a 步到链表尾部,这时p1也走到List2的b-a位置，还差a步就到可能的第一个公共节点。将p2 换成 List1头部，p2走a步也到可能的第一个公共节点。如果恰好p1==p2,那么p1就是第一个公共节点。  或者p1和p2一起走n步到达列表尾部，二者没有公共节点，退出循环。 同理a>=b。时间复杂度O(n+a+b)。如果有公共节点，两个指针都走 a+b+n步(一共是a+n+b+n,找到公共节点之后,最后一个n不用走.)

　　**注意问题**：

　　1.直接把List1和List2接上需要遍历一遍,因为不知道链表最后一个元素的地址.在操作过程共进行判断是否跳到另一个链表的方法可以少一次遍历;

　　2.所有引用类型都要进行判空;

　　**补充知识点**：java条件运算符：`p1=p1==null?pHead2:p1.next;`

```java
//java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
    public ListNode FindFirstCommonNode(ListNode pHead1, ListNode pHead2) {
        if (pHead1==null || pHead2==null)
        {
            return null;
        }
        ListNode p1,p2;
        p1=pHead1;
        p2=pHead2;
        while (p1!=p2)
        {
            p1=p1==null?pHead2:p1.next;
            p2=p2==null?pHead1:p2.next;
        }
        return p1;
    }
}
```

<p id='55'>55、链表中环的入口结点</p>

　　**题目描述：**

　　给一个链表，若其中包含环，请找出该链表的环的入口结点，否则，输出null。

　　**解题思路**：

　　**注意问题**：

　　**补充知识点**：

<p id='56'>56、删除链表中重复的结点</p>

　　**题目描述：**

  在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5。

　　**解题思路**：设立两个指针：cur和last，cur表示当前指针，last表示确定无重复结点的最后节点（即last.val!=last.next.val）。cur顺序遍历，把无重复的节点加入到last中。增加一个空头节点，当出现第一个节点就是重复节点的情况时，无需单独列出讨论。

　　**注意问题**：

　　1.last.next更新之后，last也要更新为：last.next;

　　2.因为循环的判断条件是：`cur!=null && cur.next!=null`，所以当cur指到最后一个节点或者cur==null时，已经跳出了循环，而此时last的值未更新，所以跳出循环之后要加一句：`last.next=cur;`

　　**补充知识点**：

```java
//java
/*
 public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}
*/
public class Solution {
    public ListNode deleteDuplication(ListNode pHead)
    {
        if (pHead==null || pHead.next==null)
            return pHead;
        ListNode head=new ListNode(-1);//前两个是重复节点，需要增加空头结点
        head.next=pHead;
        pHead=head;
        ListNode cur,last;
        last=pHead;
        cur=pHead.next;
        while (cur!=null && cur.next!=null)
        {
            if (cur.val!=cur.next.val)
            {
                last.next=cur;
                last=last.next;
                cur=cur.next;
            }
            else
            {
                while (cur.next!=null && cur.val==cur.next.val)
                    cur=cur.next;
                cur=cur.next;
            }
        }
        last.next=cur;
        return pHead.next;
    }
}
```

