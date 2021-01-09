# Java

## 基本概念

public class 和class的区别:

- 一个java源文件当中可以定义多个class
- 一个java源文件当中public的class不是必须的
- 一个class会定义生成一个xxx.class字节码文件
- 一个java源文件当中定义公开的类的话，只能有一个，并且该类名称必须和java源文件名称一致。
- 每一个class当中都可以编写main方法，都可以设定程序的入口，想执行B.class中的main方法: java B,想执行x.class当中的main方法:java x
- **注意:当在命令窗口中执行java Hello，那么要求Hello.class当中必须有主方法**，**没有主方法会出现运行阶段的错误:**
  **在类B中找不到主方法，请将主方法定义为:public static void main(string [] args)**

标识符：字母，数字，下划线，美元符号

命名规范

- 遵守驼峰命名方式
- *类名、接口名:首字母大写，后面每个单词首字母大写。*
- 变量名、方法名:首字母小写,后面每个单词首字母大写。
- 常量名:全部大写

**使用long类型的数据，需要在后面加后缀L，使用float类型需要加F**

布尔类型：boolean

定义数组格式：

~~~java
int [] array1 = new int [6];				//动态初始化

int [] array2  = new int [] {1,2,3};		//静态初始化
int [] array2 = {3,2,1};					//静态初始化省略格式

//静态初始化分步骤
int [] array3;				
array3 = new int [3];
array3 = new int [] {4,5,6};
~~~

**获取数组长度，后面没有括号`array.length`**

输出函数`System.out.println("这是一个" + "实例"  + "中间用加号+相连")`

## 对象的创建与使用

~~~java
package cn.it;
/*
通常情况下，一个类并不能直接使用，需要根据类创建一个对象，才能使用。
1．导包:也就是指出需要使用的类，在什么位置。
import包名称.类名称;
import cn.itcast.daye6 .demo01.Student;
对于和当前类属于同—个包的情况，可以省略导包语句不写。
2．创建，格式:
类名称对象名= new类名称();
Student stu = new Student();
3．使用，分为两种情况:
使用成员变量:对象名.成员变量名
使用成员方法:对象名.成员方法名(参数)(也就是，想用谁，就用对象名点儿谁。)*l
 */
public class HelloWorld {
    public static void main(String[] args) {
        Student stu = new Student();
        stu.higher = 190;
        stu.name = "张三";
        stu.weight = 130;
        System.out.println(stu.weight);
    }

}
~~~

~~~java
package cn.it;

public class Student {
    int higher;
    int weight;
    String name;
}
~~~

## 使用类的方式

1. 导包

   import 包路径.包名称;

2. 创建

   类名称 对象名 = new 类名称();

3. 使用

   对象名.成员方法名()

- java.lang路径下的不需要导包，如： String
- Scanner在java.util则需要导包

从键盘读取输入：

`Scanner sc = new Scanner(System.in);`

随机数：

`Random r = new Random();`里面有参数的话，是左闭右开区间，从0-(n-1)

## ArrayList

类比c++中的容器

`ArrayList list = new ArrayList<>();`

常用方法

- public boolean add(E e):向集合当中添加元素，参数的类型和泛型一致。
- public E get(int index):从集合当中获取元素，参数是索引编号，返回值就是对应位置的元素。
- public E remove(int index):从集合当中删除元素，参数是索引编号，返回值就是被删除掉的元素。
- public int size():获取集合的尺寸长度，返回值是集合中包含的元素个数。

集合ArrayList只能存放引用类型
如果希望向集合ArrayList当中存储基本类型数据，必须使用基本类型对应的“包装类”。
包装类（引用类型，包装类都位于java.Lang包下)

| 基本类  | 包装类            |
| ------- | ----------------- |
| byte    | Byte              |
| short   | Short             |
| int     | Integer【特殊】   |
| long    | Long              |
| float   | Float             |
| double  | Double            |
| char    | Character【特殊】 |
| boolean | Boolean           |

## String

字符串的特点:
1．字符串的内容永不可变。【重点】
2．正是因为字符串不可改变，所以字符串是可以共享使用的。
3．字符串效果上相当于是char[ ]字符数组，但是底层原理是byte[ ]字节数组。创建字符串的常见3+1种方式。
三种构造方法:

- public String():创建一个空白字符串，不含有任何内容。
- public String(char[ ] array):根据字符数组的内容，来创建对应的字符串。
- public String(byte[] array):根据字节数组的内容，来创建对应的字符串。

一种直接创建:

`String str = "abc";`

字符串常量池:程序当中直接写上的双引号字符串，就在字符串常量池中。

对于基本类型来说，==是进行数值的比较。
对于引用类型来说，==是进行地址值的比较。

~~~java
public class test {
    public static void main(String[] args) {
        String str1 = "Java";
        String str2 = "Java";

        char[] str = {'J', 'a', 'v', 'a'};
        String str3 = new String(str);

        System.out.println(str1 == str2);	//true
        System.out.println(str1 == str3);	//false	
        System.out.println(str1 == str3);	//false
    }
}

~~~




![](Java%E7%AC%94%E8%AE%B0.assets/%E5%AD%97%E7%AC%A6%E4%B8%B2.png)

### String常用方法

#### 1.比较字符串

```java
/*
==是进行对象的地址值比较，如果确实需要字符串的内容比较，可以使用两个方法:
public boolean equals(Object obj):参数可以是任何对象，只有参数是一个字符串并且内容相同的才会给true，否则返回false.
备注:
1. 任何对象都能用object进行接收。
2. equals方法具有对称性，a.equals(b)和b.equals(a)效果一样。
3. 如果比较双方一个常量一个变量，推荐把常量写在前面

public boolean equalsIgnoreCase(Object obj):忽略大小写进行比较
*/

public class test {
    public static void main(String[] args) {
        String str1 = "Java";
        String str2 = "Java";

        char[] str = {'J', 'a', 'v', 'a'};
        String str3 = new String(str);

        System.out.println(str1.equals(str2));
        System.out.println(str2.equals(str3));
        System.out.println(str3.equals("Java"));

        //区分大小写和不区分大小写
        System.out.println("区分大小写");
        System.out.println("Java".equals(str1));
        System.out.println("java".equals("str1"));
        System.out.println("不区分大小写");
        System.out.println("java".equalsIgnoreCase(str1));

        //推荐把常量写在前面，防止报错
//        String str4 = null;
//        System.out.println(str4.equals("Java"));//会报错

    }
}

```

#### 2.获取字符串

```java
/*
String当中与获取相关的常用方法有:
public int length():获取字符串当中含有的字符个数，拿到字符串长度。
public String concat(String str):将当前字符串和参数字符串拼接成为返回值新的字符串。
public char charAt(int index):获取指定索引位置的单个字符。(索引从o开始。)
public int indexOf(String str):查找参数字符串在本字符串当中首次出现的索引位置，如果没有返回-1值。
*/

public class test {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "Java";

        //获取字符串长度
        int length = str1.length();
        System.out.println(length);

        //拼接字符串
        String str3 = str1.concat(str2);
        System.out.println(str3);

        //查找字符串索引位置处的字符
        char c = str1.charAt(0);
        System.out.println(c);

        //返回最先出现匹配字符串的索引位置，未找到则返回-1
        int index = str1.indexOf("llo");
        System.out.println(index);

    }
}

```

#### 3.字符串的截取方法

```java
/*字符串的截取方法:
public String substring(int index):截取从参数位置一直到字符串末尾，返回新字符串。
public String substring(int begin，int end):截取从begin开始，一直到end结束，中间的字符串。
备注:[ begin , end)，包含左边，不包含右边。
*/

public class test {
    public static void main(String[] args) {
        String str1 = "HelloJava";
        //从某一位置截取到末尾
        String str2 = str1.substring(5);
        System.out.println(str2);
        //从某一位置截取到某一位置---左闭右开区间
        String str3 = str1.substring(5,7);
        System.out.println(str3);
    }
}

```

#### 4.字符串的转换方法

```java
package cn.it;
/*
String当中与转换相关的常用方法有:
public char[ ] toCharArray():将当前字符串拆分成为字符数组作为返回值。
public byte[] getBytes():获得当前字符串底层的字节数组。
public String replace(CharSequence oldstring,CharSequence newString):
将所有出现的老字符串替换成为新的字符串，返回替换之后的结果新字符串。
 */
public class test {
    public static void main(String[] args) {
        String str1 = "HelloJava";
        //字符串转换为字符数组
        char[] chars = str1.toCharArray();
        System.out.println(chars[0]);
        System.out.println(chars.length);
        System.out.println("==============");
        //字符串转换为底层的byte数组
        byte[] bytes = str1.getBytes();
        for (int i = 0; i < bytes.length; i++) {
            System.out.println(bytes[i]);
        }
        System.out.println("==============");
        //将所有出现过的字符串中的字符替换成新字符
        String newstring = str1.replace('a', '*');
        System.out.println(newstring);
    }
}

```

#### 5.分割字符串的方法

```java
/*
分割字符串的方法:
public String[ ] split(String regex):按照参数的规则，将字符串切分成为若干部分。
注意事项:
split方法的参数其实是一个“正则表达式”。
今天要注意:如果按照英文句点“."进行切分，必须写"\\.”(两个反斜杠)

 */
public class test {
    public static void main(String[] args) {
        String str1 = "aaa,bbb,ccc";
        String[] array1 = str1.split(",");
        for (int i = 0; i < array1.length; i++) {
            System.out.println(array1[i]);
        }
        System.out.println("========");

        String str2 = "aaa bbb ccc";
        String[] array2 = str2.split(" ");
        for (int i = 0; i < array2.length; i++) {
            System.out.println(array2[i]);
        }
        System.out.println("========");
        String str3 = "aaa.bbb.ccc";

        String[] array3 = str2.split(".");//无法识别，分割失败
        System.out.println(array3.length);

        //要用    \\. 才能分割    .
        String[] array4 = str3.split("\\.");
        for (int i = 0; i < array4.length; i++) {
            System.out.println(array4[i]);
        }
    }
}

```

## static

### 基本概念

![](Java%E7%AC%94%E8%AE%B0.assets/static.png)

如果一个成员变量使用了static关键字，那么这个变量不再属于对象自己，而属于所在的类。多个对象共享同一份数据。

```java
public class Student {

    int num;
    static int numStatic;

    public void method(){
        System.out.println("这是一个成员方法！！");
        //成员方法可以访问成员变量
        System.out.println(num);
        //成员方法可以访问静态变量
        System.out.println(numStatic);
    }

    public static void methodStatic(){
        System.out.println("这是一个静态方法！！");
        //静态可以访问静态
        System.out.println(numStatic);
        //静态不能直接访问非静态【重点】
        //System.out.println(num);

        //静态方法不能使用this关键字
        //System.out.println(this);
    }
}

```



```java
/*
一旦使用static修饰成员方法，那么这就成为了静态方法。静态方法不属于对象，而是属于类的。

如果没有static关键字，那么必须首先创建对象，然后通过对象才能使用它。
如果有了static关键字，那么不需要创建对象，直接就能通过类名称来使用它。

无论是成员变量，还是成员方法。如果有了static，都推荐使用类名称进行调用。
静态变量:类名称.静态变量
静态方法:类名称.静态方法()

注意事项:
1．静态不能直接访问非静态。
原因:因为在内存当中是【先】有的静态内容，【后】有的非静态内容。
先人不知道后人，但是后人知道先人。”
2．静态方法当中不能用this。
原因:this代表当前对象，通过谁调用的方法，谁就是当前对象。
 */
public class test {
    public static void main(String[] args) {
        Student stu = new Student();//首先创建对象
        //然后才能使用没有static关键字的内容
        stu.method();

        //对于静态方法来说，可以通过对象名进行调用，也可以直接通过类名称来调用
        stu.methodStatic();//不推荐，这种写法在编译之后也会被javac翻译成   ”类名称.静态方法名“
        Student.methodStatic();//推荐

        //对于本类当中的方法，可以省略类名称
        myMethod();
        test.myMethod();//完全等效
    }

    public static void myMethod(){
        System.out.println("我自己的方法！！");
    }
}

```

![](Java%E7%AC%94%E8%AE%B0.assets/%E5%86%85%E5%AD%98%E5%9B%BE.png)

### 静态代码块

```java
/*
静态代码块的格式是:
public class类名称{
    static {
        //静态代码块的内容
    }
}
特点:当第一次用到本类时，静态代码块热行唯一的一次。
静态内容总是优先于非静态，所以静态代码块比构造方法先执行。

静态代码块的典型用途:
用来一次性地对静态成员变量进行赋值。
 */
public class Student {
    static {
        System.out.println("静态代码块的执行！！");
    }
    Student(){
        System.out.println("默认调用的执行！！");
    }
}

```

## 数组工具类Arrays

```java
import java.util.Arrays;

/*
java.util.Arrays是一个与数组相关的工具类，里面提供了大量静态方法，用来实现数组常见的操作。

public static String toString(数组):将参数数组变成字符串（按照默认格式:[元素1，元素2，元素3...])
public static void sort(数组):按照默认升序（从小到大）对数组的元素进行排序。

备注:
1．如果是数值,sort默认按照升序从小到大
2如果是字符串，sort默认按照字母升序
3．如果是自定义的类型，那么这个自定义的类需要有Comparable或者Comparator接口的支持。
 */
public class test {
    public static void main(String[] args) {
        int [] array1 = {10, 20 ,30};
        //将int[]数组按照默认格式变成字符串
        String intStr = Arrays.toString(array1);
        System.out.println(intStr);

        int [] array2 = {8, 1, 6, 7, 3};
        Arrays.sort(array2);
        System.out.println(Arrays.toString(array2));
    }
}

```

## 数学工具类Math

```java
/*
java.util.Math类是数学相关的工具类，里面提供了大量的静态方法，完成与数学运算相关的操作。

public static double abs( double num):获取绝对值。有多种重载。
public static double ceil( double num):向上取整。
pgblic static double floor ( double num):向下取整。
public static long round ( double num):四舍五入。

Math.PI代表近似的圆周率常量（double) 。
 */
public class test {
    public static void main(String[] args) {
        System.out.println(Math.abs(1.2));
        System.out.println(Math.abs(-1));
        System.out.println(Math.abs(0));
        System.out.println("===========");

        System.out.println(Math.ceil(2.1));
        System.out.println(Math.ceil(2.9));
        System.out.println(Math.ceil(2.0));

        System.out.println("===========");
        System.out.println(Math.floor(2.1));
        System.out.println(Math.floor(2.9));
        System.out.println(Math.floor(2.0));

        System.out.println("===========");
        System.out.println(Math.round(2.4));
        System.out.println(Math.round(2.5));
        System.out.println(Math.round(2.6));
    }
}

```

## 继承

```java
/*
定义父类的格式:(一个普通的类定义)public class父类名称{
    // ...
}
定义子类的格式:
public class子类名称extends父类名称{
    //...
}
 */

public class algorithm {
    public static void main(String[] args) {
        Teacher a = new Teacher();
        a.method();
    }
}

class Employee{
    public void method(){
        System.out.println("方法执行");
    }
}

class Teacher extends Employee{

}
```

### 同名变量处理

```java
/*
局部变量:                 直接写成员变量名
本类的成员变量:            this.成员变量名
父类的成员变量:            super.成员变量名
*/

public class algorithm {
    public static void main(String[] args) {
        Teacher a = new Teacher();
        a.method();
    }
}

class Employee{
    int num = 10;
}

class Teacher extends Employee{
    int num = 20;
    public void method(){
        int num = 30;
        System.out.println(num);
        System.out.println(this.num);
        System.out.println(super.num);
    }
}

```

### 方法重写

```java
/*
方法覆盖重写的注意事项:
1．必须保证父子类之间方法的名称相同，参数列表也相同。
@Override:写在方法前面，用来检测是不是有效的正确覆盖重写。
这个注解就算不写，只要满足要求，也是正确的方法覆盖重写。

2．子类方法的返回值必须【小于等于】父类方法的返回值范围。
小扩展提示: java.Lang.Object类是所有类的公共最高父类（祖宗类)，java.Lang.String就是object的子类。。

3.子类方法的权限必须【大于等于】父类方法的权限修饰符。小扩展提示:public > protected > ( default) > private
备注:(default)不是关键字default，而是什么都不写，留空。
*/

public class algorithm {
    public static void main(String[] args) {
        Teacher a = new Teacher();
        a.method();
    }
}

class Employee{
    public void method(){
        System.out.println("父类方法调用!!");
    }
}

class Teacher extends Employee{
    
    @Override//可写可不写
    public void method(){
        System.out.println("子类方法调用！！");
    }
}

```

### 构造方法的调用（this和super）

```java
/*
继承关系中，父子类构造方法的访问特点:
1．子类构造方法当中有一个默认隐含的“super()"调用，所以一定是先调用的父类构造，后执行的子类构造。 
2．子类构造可以通过super关键字来调用父类重载构造。
3. super的父类构造调用，必须是子类构造方法的第一个语句。不能一个子类构造调用多次super构造。
总结:
子类必须调用父类构造方法，不写则赠送super();
写了则用写的指定的super调用，super只能有一个，还必须是第一个。

对于this用于构造方法，必须是子类构造方法的第一个语句。不能一个子类构造调用多次this。
this只能有一个，还必须是第一个。
super和this不能同时使用，因为他们都必须是第一个且是唯一一个！！
*/

public class algorithm {
  public static void main(String[] args) {
   
  }
}

class Employee {
  public Employee(){
  	this(10);//本类有参构造的调用
  }
    
  public Employee(int num){
    
  }
}

class Teacher extends Employee {
  public Teacher(){
    super(10);//父类有参构造的调用
  }
}
```

### super与this关键字

![](Java%E7%AC%94%E8%AE%B0.assets/super%E4%B8%8Ethis%E5%85%B3%E9%94%AE%E5%AD%97.png)

### Java继承的特点

![](Java%E7%AC%94%E8%AE%B0.assets/Java%E7%BB%A7%E6%89%BF%E7%9A%84%E7%89%B9%E7%82%B9.png)

### 抽象方法和抽象类

```java
/*
抽象方法:就是加上abstract关键字，然后去掉大括号，直接分号结束。
抽象类:抽象方法所在的类，必须是抽象类才行。在class之前写上abstract即可。
但是抽象类不一定有抽象方法
如何使用抽象类和抽象方法:
1．不能直接创建new抽象类对象。2．必须用一个子类来继承抽象父类。
3.子类必须覆盖重写抽象父类当中所有的抽象方法。(否则子类也是抽象类)
覆盖重写（实现):子类去掉抽象方法的abstract关键字，然后补上方法体大括号。4．创建子类对象进行使用。ll
*/

public class algorithm {
  public static void main(String[] args) {
    Teacher one = new Teacher();
    one.method();
  }
}

abstract class Employee {
  public abstract void method();
  public void ms(){}
}

class Teacher extends Employee {
  @Override
  public void method() {
    System.out.println("子类重写方法");
  }
}

```

## 接口

### 基本概念

```java
/*
接口就是多个类的公共规范。
接口是一种引用数据类型，最重要的内容就是其中的：抽象方法。

如何定义一个接口的格式:
public interface 接口名称{
  //接口内容
}

备注:换成了关键字interface之后，编译生成的字节码文件仍然是:.java --> .class。

如果是Java 7，那么接口中可以包含的内容有:
1．常量
2．抽象方法

如果是Java 8，还可以额外包含有:
3．默认方法
4、静态方法

如果是Java 9，还可以额外包含有:
5．私有方法
*/

/*
在任何版本的Java中，接口都能定义抽象方法。
格式:
public abstract 返回值类型 方法名称(参数列表);
注意事项:
1．接口当中的抽象方法，修饰符必须是两个固定的关键字: public abstract
2.这两个关键字修饰符，可以选择性地省略。
3．方法的三要素,可以随意定义。
*/
public interface Jiekou {
  // 这是一个抽象方法
  public abstract void method1();

  // 这也是一个抽象方法
  abstract void method2();

  // 这也是一个抽象方法
  public void method3();

  // 这也是一个抽象方法
  void method4();
}

```

### 使用方法

- 接口类

```java
public interface Jiekou {
  // 这是一个抽象方法
  public abstract void method1();

  // 这也是一个抽象方法
  abstract void method2();

  // 这也是一个抽象方法
  public void method3();

  // 这也是一个抽象方法
  void method4();
}

```



- 接口的实现类

```java
public class JiekouImpl implements Jiekou {
  @Override
  public void method1() {
    System.out.println("这是第一个方法");
  }

  @Override
  public void method2() {
    System.out.println("这是第二个方法");
  }

  @Override
  public void method3() {
    System.out.println("这是第三个方法");
  }

  @Override
  public void method4() {
    System.out.println("这是第四个方法");
  }
}

```



- 主程序

```java
/*
接口使用步骤:
1．接口不能直接使用，必须有一个“实现类”来“实现”该接口。
格式:
public class 实现类名称 implements 接口名称{
  // ...
}
2．接口的实现类必须覆盖重写（实现)接口中所有的抽象方法。
实现:去掉abstract关键字，加上方法体大括号。
3.创建实现类的对象,进行使用。

注意事项:
如果实现类并没有覆盖重写接口中所有的抽象方法，那么这个实现类自己就必须是抽象类。
*/
public class test {
  public static void main(String[] args) {
    // 错误方法，无法实例化接口
    // Jiekou jiekou = new Jiekou();

    // 创建实现类对象
    JiekouImpl impl = new JiekouImpl();
    impl.method1();
    impl.method2();
  }
}

```

### 接口默认方法使用

- MyinterfaceDefault

```java
/*
从Java 8开始，接口里允许定义默认方法。
格式:
public default 返回值类型方法名称(参数列表){
  //方法体
}
备注:接口当中的默认方法，可以解决接口升级的问题。

1.接口的默认方法，可以通过接口实现类对象，直接调用。
2.接口的默认方法，也可以被接口实现类进行覆盖重写。l

 */
public interface MyinterfaceDefault {
  // 抽象方法
  public abstract void mythodAbs();

  // 新添加了一个抽象方法，需要在“实现类中重写”
  // public abstract void methodAbs2();

  // 新添加的方法改为默认方法
  public default void mythodDefault() {
    System.out.println("这是一个默认方法");
  }
}

```

- MyinterfaceDefaultA

```java
public class MyinterfaceDefaultA implements MyinterfaceDefault {
  @Override
  public void mythodAbs() {
    System.out.println("重写实现方法，AAAA");
  }
}
```

- MyinterfaceDefaultB

```java
public class MyinterfaceDefaultB implements MyinterfaceDefault {
  @Override
  public void mythodAbs() {
    System.out.println("重写实现方法，BBB");
  }

  @Override
  public void mythodDefault() {
    System.out.println("重写默认方法，BBB");
  }
}
```

- Myinterface

```java
public class Myinterface {
  public static void main(String[] args) {
    MyinterfaceDefaultA a = new MyinterfaceDefaultA();
    // 调用默认方法
    a.mythodAbs();
    // 实现类中没有默认方法，则向上找接口
    a.mythodDefault();
    System.out.println("===========");

    MyinterfaceDefaultB b = new MyinterfaceDefaultB();
    b.mythodAbs();
    b.mythodDefault();
  }
}
```

### 接口的静态方法调用

- MyinterfaceStatic

```java
/*
从Java 8开始，接口当中允许定义静态方法。格式:
public static返回值类型方法名称(参数列表){
	方法体
}
提示:就是将abstract或者default换成static即可，带上方法体。

不需要重写
*/
public interface MyinterfaceStatic {
  public static void method() {
    System.out.println("静态方法调用！！");
  }
}
```

- MyinterfaceStaticA

```java
public class MyinterfaceStaticA implements MyinterfaceStatic {}
```

- Myinterface

```java
/*
注意事项:不能通过接口实现类的对象来调用接口当中的静态方法。
正确用法:通过接口名称，直接调用其中的静态方法。
格式:
接口名称.静态方法名(参数);
*/
public class Myinterface {
  public static void main(String[] args) {
    // 错误写法，通过实例化对象来调用静态方法
    MyinterfaceStaticA a = new MyinterfaceStaticA();
    // a.method();

     //直接通过接口名称访问
    MyinterfaceStatic.method();
  }
}
```

### 接口的私有化

```java
/*
我们需要抽取一个共有方法，用来解决两个默认方法之间重复代码的问题。

但是这个共有方法不应该让实现类使用，应该是私有化的。
解决方案:
从Java 9开始，接口当中允许定义私有方法。
1、普通私有方法，解决多个默认方法之间重复代码问题格式:
private 返回值类型 方法名称(参数列表){
	方法体
}
2．静态私有方法，解决多个静态方法之间重复代码问题格式:
private static 返回值类型 方法名称(参数列表){
	方法体
}
*/

如：
private void method(){
	System.out.printlb("普通私有方法");
}

private static void method(){
	System.out.printlb("静态私有方法");
}
```

### 接口的常量定义和使用

- 常量接口

```java
/*
接口当中也可以定义“成员变量”，但是必须使用public static final三个关键字进行修饰。
从效果上看，这其实就是接口的【常量】。
格式:
pubLic static final 数据类型常量名称 = 数据值;
备注:
一旦使用final关键字进行修饰，说明不可改变。
注意事项:
1．接口当中的常量，可以省略public static final，注意:不写也照样是这样。
2．接口当中的常量，必须进行赋值，不能不赋值。
3．接口中常量的名称，使用完全大写的字母，用下划线进行分隔。（推荐命名规则）
 */
public interface MyinterfaceConst {
  // 访问接口中的常量
  public static final int NUM_OF_MY_CLASS = 11901;
}
```

- 调用常量

```java
public class Myinterface {
  public static void main(String[] args) {
    // 访问接口中的常量
    System.out.println(MyinterfaceConst.NUM_OF_MY_CLASS);
  }
}
```

