# 内部类

### 1. 成员内部类 `Member inner class`
        
> 在外部类内部 **直接** 定义的类就是成员内部类，它可以直接使用外部类的所有变量和方法，即使是 `private` 的
        
> 外部类要想访问内部类的成员变量和方法，则需要通过内部类的对象来获取
    
```java
//外部类   
 class Out {   
     private int age = 17;   

     //内部类   
     class In {   
         public void print() {   
             System.out.println(age);   
         }   
     }   
 }   

 public class Demo {   
     public static void main(String[] args) {   
         Out.In in = new Out().new In();   
         in.print();   
         // 或者采用下种方式访问   
         /*   
         Out out = new Out();   
         Out.In in = out.new In();   
         in.print();   
         */   
     }   
 }
```
        
> `Out` 是为了标明需要生成的内部类对象在哪个外部类当中

> 必须先有外部类的对象才能生成内部类的对象，因为内部类的作用就是为了访问外部类中的成员变量
        
### 2. 静态内部类 `Static member inner class`
        
```java
class Out {   
     private static int age = 17;   

     static class In {   
         public void print() {   
             System.out.println(age);   
         }   
     }   
 }   

 public class Demo {   
     public static void main(String[] args) {   
         Out.In in = new Out.In();   
         in.print();   
     }   
 }
```
> 如果用 `static` 将内部内静态化，那么内部类就只能访问外部类的静态成员变量，具有局限性

> 因为内部类被静态化，因此 `Out.In` 可以当做一个整体看，可以直接 `new` 出内部类的对象，通过类名访问 ，生不生成外部类对象都没关系
        
### 3. 局部内部类 `Local inner class`
        
```java
class Out {   
     private int age = 17;   

     public void Print(final int x) {   
         class In {   
             public void inPrint() {   
                 System.out.println(x);   
                 System.out.println(age);   
             }   
         }   
         new In().inPrint();   
     }   
 }   

 public class Demo {   
     public static void main(String[] args) {   
         Out out = new Out();   
         out.Print(18);   
     }   
 }
```
        
> 将内部类移到了外部类的方法中

> 局部内部类不能从方法外部调用，需要在外部类的方法中再生成一个内部类对象去调用内部类方法

> 不能被 `static` `private` 修饰，因为不再是成员

> 如果此时需要往外部类的方法中传入参数，那么外部类的方法形参必须使用 `final` 定义（JDK1.8 可以不用 `final`）
        
### 4. 匿名内部类 `Anonymous inner class` `[ə'nɒnɪməs]`
    
```java
// 不使用匿名内部类的情况

abstract class Father{
    public abstract void study();
}
class Child extends Father{
    public void study() {
        System.out.println("Child is study...");
    }
}
public class Demo {
    public static void main(String[] args) {
        Father child = new Child();
        child.study();
    }
}
```

```java
// 使用匿名内部类的情况

abstract class Father{
    public abstract void study();
}
public class Demo {
    public static void main(String[] args){
        // 直接继承 Father 类
        new Father() {
            public void study() {
                System.out.println("Child is study...");
            }
        }.study();
    }
}        
```

> 只用到类的一个实例

> 类在定义后马上用到

> 类相对比较小

> 给类命名并不会导致代码更容易被理解

---
[幕后英雄的用武之地——浅谈Java内部类的四个应用场景](http://blog.csdn.net/hivon/article/details/606312)
