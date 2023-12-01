# 第十章 多态性

> NonoTion笔记

## 10.1 后绑定

通常，一个引用变量的类型要与其应用的对象的类相匹配

```java
String s；
```

s变量用于指向一个通过实例化String类所创建的对象

但事实上，引用变量和该引用变量指向的对象必须是兼容的，但不必完全相同。

**“多态性”polymorphism：**

一个“多态引用变量”是可以在不同时间指向不同类型对象的变量 

**绑定：**

在程序执行的某个时刻，可能会产生请求事件，要求执行某段代码来完成一个方法调用，这种请求时间称为一个方法调用与一个方法定义的绑定。通常，这种绑定发生在编译阶段。

**后绑定：**

多态性引用的绑定要延迟到程序运行时才能执行，并且要绑定的方法定义取决于当时引用变量所引用的对象，这一被延迟的请求事件被称为后绑定或动态绑定。

**重点：**

1. 对于多态性引用，方法调用和方法定义代码的绑定在运行时才执行
2.  多态性引用可以随时间变化指向不同类型的对象

---

## 10.2 由继承实现多态性

一个引用变量可以指向由继承关系的任何类的任何对象。

实际将调用的方法版本取决于对象的类型而非引用变量的类型。

---

## 10.3 利用接口实现多态性

接口名可以用于声明对象引用变量

一个接口引用变量可以指向实现该接口的任何类的任何对象

方法的参数可以是多态性的，使得方法所接收的参数具有灵活性

---

## 10.4 排序方法

### 10.4.1 选择排序

在每轮循环中，找到最大（小）的元素，与对应位置交换O（$n^2$）

```java
    public static void selectSort(Comparable []list)
    {
        for(int index=0;index<list.length-1;index++)
        {
            Comparable temp;
            int min=index;
            for(int scan=index+1;scan<list.length;scan++)
            {
                if(list[scan].compareTo(list[min])<0)
                    min=scan;
            }
            temp=list[min];
            list[min]=list[index];
            list[index]=temp;
        }
    }
```

以多态性方法实现的排序算法可对任何一组可比较的对象排序

### 10.4.2 插入排序法 O（$n^2$）

```java
public static void insertSort(Comparable[] list)
    {
        for(int index=1;index<list.length;index++)
        {
            Comparable Key=list[index];
            int position=index;
            while(position>0&&Key.compareTo(list[position-1])<0)
            {
                list[position]=list[position-1];
                position--;
            }
            list[position]=Key;
        }
    }
```

---

## 10.5 搜索

### 10.5.1 线性搜索

```java
public static Comparable linearSearch(Comparable []list,Comparable target)
    {
        int index=0;
        boolean found=false;
        while(!found&&index< list.length)
        {
            if(list[index].compareTo(target)==0)
            {
                found=true;
            }
            else index++;
        }
        if(found)
            return list[index];
        else
            return null;
    }
```

### 10.5.2 二分查找

只能查找有序列表

升序查找

```java
 public static Comparable binarySearch(Comparable []list,Comparable target)
    {
        int min=0,max= list.length-1,mid=0;
        boolean found=false;
        while(!found&&min<=max)
        {
            mid=(min+max)/2;
            if (target.compareTo(list[mid])==0)
                found=true;
            else if (target.compareTo(list[mid])<0) {
                max=mid-1;
            }
            else min=mid+1;
        }
        if(found) return list[mid];
        else return null;
    }
```

---

## 10.6 多态性

多态性允许用一致性的方法实现不一致的行为

应该训练自己的软件设计敏感性，善于识别能利用多态性解法的潜在问题

---

# End