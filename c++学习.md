# c++核心编程

## c++风格字符串

~~~ c++
#include<iostream>
using namespace std;
#include<string>  //c++风格字符串头文件

int main()
{
	string str = "I LOVE YOU!";
	cout << str << endl;
 } 
~~~

## 输出变量

~~~ c++
#include <iostream>
using namespace std;

int main()
{
	int a = 2;
	//输出时变量或者 “”前加 << 结束后也要加 << 
	cout <<  a << endl;
	cout << "a = "<< a << endl;
	cout << "a = "<< a <<" hh"<< endl;
}
~~~

## 整数与小数运算

~~~c++
#include<iostream>
using namespace std;

//全部为小数 
int main()
{
	double a = 2.2;
	int b = 4;
	cout << a*b << endl;//整数与小数相乘
	cout << a/b << endl;//整数与小数相除
	cout << a+b << endl;//整数与小数相加
	cout << a-b << endl;//整数与小数相减 
}
~~~

## 内存管理堆区

~~~c++
#include<iostream>
using namespace std;

//全部为小数 
int main()
{
	double a = 2.2;
	int b = 4;
	cout << a*b << endl;//整数与小数相乘
	cout << a/b << endl;//整数与小数相除
	cout << a+b << endl;//整数与小数相加
	cout << a-b << endl;//整数与小数相减 
}
~~~

## 引用（起别名）

~~~c++
/*
注意事项
		1.引用必须初始化 
			int &a;  这个就不可以
		2.引用之后不可以更改引用 
			int &a = b;
			b = c;   不可以这样，这样相当于给b赋值为c 
*/

#include<iostream>
using namespace std;

//引用的本质是   指针常量 

void swap(int &c, int &d)
{
	int temp = c;
	c = d;
	d = temp;
}

int& text()
{
	static int a = 10;//static是静态常量，保证a的值在函数text调用后不会销毁 
	return a;
}


int main()
{
	
	//引用（起别名） 
	int a = 10;
	//数据类型 &别名 = 变量名 
	int &b = a;
	cout << a << endl;
	cout << b << endl;
	
	//1.修改别名数据，原数据也会改变 
	b = 100;
	cout << a << endl;
	cout << b << endl;
	
	cout << endl << endl;
	
	//2.可以实现形参修饰实参
	int c = 20;
	int d = 10;
	swap(c, d); 
	cout << c << endl << d << endl;
	
	cout << endl << endl;
	
	//3.如果函数的返回值是引用，则函数可以作为左值
	int &ref = text();
	
	cout << ref << endl;
	cout << ref << endl;
	
	text() = 1000;
	
	 cout << ref << endl;
	cout << ref << endl;
    
    //4.引用必须是引用一块合法的空间
    /*
    	int &a = 10;   不可以，因为10是常量，而引用需要一个左值
    	
    	const int &a = 10;
    		可以，编译器把这一句翻译为
    			int temp = 10；
    			const int &a = temp；  此时a的值不可以改变，因为有const修饰
    */
}
~~~

## 函数的形参默认值

在c++中，函数的形参可以有默认值

**注意事项：**

**1. 调用函数时如果有输入的值，则采用输入的值**

**2. 函数的某个形参有了默认值，则它后面的形参也必须有默认值**

**3.函数的声明和定义只能有一个有默认值**

~~~c++
#include <iostream>
using namespace std;

void fun(int a, int b);

int main()
{
    cout << fun(2, 3) << endl;
}

void fun(int a = 10; int b = 10)  //形参有默认值
{
	return a + b;
}
~~~

## 函数重载

**条件;**

1. **同一个作用域下（如，全局区）**

​	2.**函数名称相同**

​	3.**函数的参数类型不同，或者参数个数不同，或者参数顺序不同**

​		**注意：**

​			**函数的返回值不能作为函数重载的条件** 

~~~c++
#include <iostream>
using namespace std;

void fun()									//1
{
    cout << "这是fun()函数的调用" << endl;
}

void fun(int a)								//2
{
    cout << "这是fun(int a)函数的调用" << endl;
}

int main()
{
	fun();									//调用第一个
}
~~~

<font color=red>**当函数重载碰上引用和形参默认值时**</font>

​	1.引用作为重载条件

~~~c++
#include <iostream>
using namespace std;

void fun(int &a)						//1
{
     cout << "这是fun(int &a)函数的调用" << endl;
}

void fun(const int &a)					//2
{
     cout << "这是fun(const int &a)函数的调用" << endl;
}

int main()
{
    int a = 10;
    fun(a);								//调用第一个
    fun(10);							//调用第二个
}
~~~

​	2.函数重载碰上函数默认参数

~~~c++
#include <iostream>
using namespace std;

void fun(int a, int b = 10)						//1
{
     cout << "int a, int b = 10" << endl;
}

void fun(int a, int b)							//2
{
     cout << "这是fun(int a, int b)函数的调用" << endl;
}

int main()
{
    fun(10);									//调用第一个
    	//fun(10, 20);	报错，二义性:两个函数相同了						
}
~~~

## 类和对象

c++面对对象三大特征：**封装，继承，多态**

c++认为万物皆为**对象**，对象有其对应的**属性**和**行为**

具有相同性质的的**对象**，可以抽象为**类**

- 封装的意义：

  在设计类的时候，将属性和行为写在一起，表现事物，称作**成员**

  属性：**成员属性，成员变量**

  行为：**成员函数，成员方法**

**语法**：

~~~c++
class 类名 {	访问权限：	属性	/	行为};
~~~

<font color=red>		例1：求圆的周长</font>

~~~c++
#include <iostream>
using namespace std;

#define  pi 3.14

class Circle
{
    //权限
    public:
    
    //属性
    	//半径
    	int m_r;
    //行为
    	//求周长
    	double calculateZC()
        {
            return 2 * pi * m_r;
		}
};

int main()
{
    Circle c1;
    
  c1.m_r = 2;
    cout << "c1的周长为: " << c1.calculateZC() << endl;
}
~~~

<font color=red>		例2：创建一个学生类，赋值并打印</font>

~~~c++
#include <iostream>
using namespace std;
#include<string>

class Student
{
    //权限
    public:
    
    //属性
    	string m_name;
    	int m_id;
    //行为
    	//打印 
    	void showStudent()
        {
            cout << "姓名:	" << m_name << "	学号" << m_id << endl;
		}
		//赋值 
		void setname(string name)
		{
			m_name = name;
		}
		
		void setid(int id)
		{
			m_id = id;
		}
};

int main()
{
    Student s1, s2;
    
    //2种赋值方式
    
    s1.m_name = "张三";
    s1.m_id = 1;
    
    s2.setname("李四");
    s2.setid(2);
    
  s1.showStudent();
    s2.showStudent();
}
~~~

## 访问权限

​			public				公共权限		类内可以访问，类外**也可以**访问

​			protected		  保护权限		类内可以访问，类外**不可以**访问				递级关系中，父级结构，子级**也可以**访问

​			private			   私有权限		类内可以访问，类外**不可以**访问				递级关系中，父级结构，子级**不可以**访问

~~~c++
#include <iostream>
using namespace std;
#include<string>

class person
{
    //公共权限
    public:
    string m_name；
     
    //保护权限
    protected:
    string m_car;
    
    //私有权限
    private:
    int m_password;
    
    //类内可以访问
    public://针对下面的函数的权限
    void fun()
    {
        m_name = "张三";
        m_car = "奔驰";
        m_password = 123456;
    }
}；

int main()
{
	person p1;
    p1.m_name = "李四";
    //其余的类外不可以访问
}
~~~

**struct与class的区别：**

<font color=blue>		默认访问权限不同，struct默认是**公共权限**，class默认是**私有权限**</font>

**成员属性设置为私有化的优点：**

	1. 将所有成员设置为私有化，可以自己控制读写权限
 	2. 对于写权限，可以检测数据的有效性

~~~c++
#include <iostream>
using namespace std;
#include<string>

class person
{
    public:
    
    //读姓名
    string getname()
    {
        m_name = "张三";
        return m_name;
    }
    
    //写年龄
    void setage(int age)
    {
        if(age < 0 || age > 150)			//判断输入的数据有效性
        {
            cout << "输入错误" << endl;
            return 0;
        }
        m_age = age;
    }
    //读年龄
    int getage()
    {
        m_age = 0;
        return m_age;
    }
    
    //写情人
    void setlover(string lover)
    {
        m_lover = lover;
    }
    
    //私有化
    private:
    string m_name;		//利用成员函数实现只读
    int m_age;			//利用成员函数实现可读可写
    string m_lover;		//利用成员函数实现只写
};

int main()
{
    person p;
    cout << p.getname() << endl;
    p.setage("18");
    cout << p.getage() << endl;
    p.setlover("李四");
}
~~~



## 对象的初始化和清理

**构造函数和析构函数**

构造函数:<font color=red> 主要用在创建对象时为对象的成员属性赋值,构造函数由编译器自动调用,无需手动调用 </font>

析构函数:<font color=red> 主要用在对象销毁前系统自动调用,执行一些清理工作 </font>

**构造函数: **`类名(){}`

```c++
1. 构造函数,没有返回值也不写void

 		2. 函数名称与类名相同
 		3. 构造函数可以有参数,因此可以发生重载
 		4. 程序在调用对象的时候会自动调用构造,无需手动调用,而且只会调用一次
```

 **析构函数:** `~类名(){}`

```c++
1. 析构函数,没有返回值也不写void
```
 	2. 函数名称与类名相同,在名称前加上符号 ~
 	3. 析构函数不可以有参数,因此不可以发生重载
 	4. 程序在对象销毁前会自动调用析构,无须手动调用,而且只会调用一次

```c++
#include <iostream>
using namespace std;

class Person
{
    public:
    	Person()
        {
            cout << "Person 构造函数的调用" << endl;
        }
    	
    	~Person()
        {
            cout << "Person 析构函数的调用" << endl;
		}
};

void test()
{
    Person p;	//栈上的函数,执行完后会被释放
}

int main()
{
    test();
}
```

## 构造函数的分类和调用

按参数分类	无参函数 (默认函数)	和	有参函数

```c++
#include <iostream>
using namespace std;

class Person
{
    public:
   		 //无参函数
    	Person()					
        {
            cout << "Person	无参	构造函数的调用" << endl;
        }
    
    	//有参函数
    	Person(int a)					
        {
            age = a;
            cout << "Person	有参	构造函数的调用" << endl;
        }
    	
    	//拷贝构造函数
    	Person( const person& p)					
        {
            //将参数的属性全部拷贝到新构造函数
            age = p.age;
            cout << "Person	拷贝	构造函数的调用" << endl;
        }
    	
    	
    	~Person()
        {
            cout << "Person 析构函数的调用" << endl;
		}
    	
    	int age;
    
};

void test()
{
     //调用
    	//1.括号法
    Person p1;		//默认(无参)构造函数的调用
    Person p2(10);	//有参构造函数的调用
    Person p3(p2);	//拷贝构造函数的调用
    //注意:
    	//默认(无参)构造函数不要加括号	Person p1();	会被编译器判断为函数的声明
    	//2.显示法
    Person p1;
    Person p2 = Person(10);//有参构造
    Person p3 = Person(p2);//拷贝构造
    
    Person(10);//匿名对象	特点:当前执行结束后，系统会	立即回收掉匿名对象
    count << "aaaa" << endl;
    
    //注意事项:
    	//不要利用拷贝构造函数初始化匿名对象	编译器会认为	Person(p3); == Person p3;	发生重定义错误
    
    	//3.隐式转换法-->相当于转换为显示法
    Person p1;
    Person p2 10;//有参构造
    Person p3 p2;//拷贝构造
}

int main()
{
   
    test();
}
```

## 深拷贝与浅拷贝

浅拷贝：简单的赋值拷贝操作

深拷贝：在堆区重新申请空间，进行拷贝操作

```c++
#include <iostream>
using namespace std;

class Person
{
    public:
   		 //无参函数
    	Person()					
        {
            cout << "Person	无参	构造函数的调用" << endl;
        }
    
    	//有参函数
    	Person(int age, int height)					
        {
            cout << "Person	有参	构造函数的调用" << endl;
            
             
            m_age = age;
            m_height = new int(height);
        }
    	
    	//拷贝构造函数
    	Person( const Person& p)					
        {
            cout << "Person	拷贝	构造函数的调用" << endl;
            //如果不利用深拷贝在堆区创建内存，会导致浅拷贝带来的重复释放堆区问题
            m_age = p.m_age;
            m_height = new int(*p.m_height);
        }
    	
    	
    	~Person()
        {
            cout << "Person 析构函数的调用" << endl;
            if (m_height != NULL)
            {
                delete m_height;
                m_height = NULL;
            }
		}
   public:	
    	int m_age;
   		int* m_height;
    
};

void test()
{
     
    Person p1(18,180);	
    
    Person p2(p1);	
    
    cout << "p1的年龄：" << p1.m_age << "身高：" << *p1.m_height << endl;
    cout << "p2的年龄：" << p2.m_age << "身高：" << *p2.m_height << endl; 
}

int main()
{
   
    test();
}
```

**总结：如果属性有在堆区开辟的，一定要自己提供拷贝构造函数，防止浅拷贝带来的问题**

**堆区的释放顺序是：先进后出**

## 初始化列表

**作用**;

c++提供了初始化列表语法，用来初始化属性

**语法：**`构造函数():属性1(值1)，属性2(值2)，属性3(值3)...{}`

```c++
#include <iostream>
using namespace std;

class Person
{
    
    public:
   //传统赋值
   //	Person(int a, int b, int c)
   //     {
   //        cout << "Person 构造函数的调用" << endl;
   //		 m_A = a;
   //		 m_B = b;
   // 		 m_C = c;
   //     }
    
     Person(int a, int b, int c):m_A(a),m_B(b),m_C(c)
     {
         cout << "Person 构造函数的调用" << endl;
     }
    	
   	~Person()
        {
           cout << "Person 析构函数的调用" << endl;
   	}
    
    int m_A;
    int m_B;
    int m_C;
    
};

void test()
{
    Person p(10, 20,30);	
    cout << "a=" << p.m_A << endl;
    cout << "b=" << p.m_B << endl;
    cout << "c=" << p.m_C << endl;
}

int main()
{
    test();
}
```

## 类对象作为类成员

c++类中的成员可以是另一个类的对象，我们称该成员为	对象成员

```c++
class A{};
class B
{
    A a;
};
```

B类中有对象A作为成员，A为对象成员

```c++
#include <iostream>
using namespace std;

class Phone
{
    public:
    	Phone(string pName)
        {
            m_PName = pName;
            cout << "Phone 构造函数的调用" << endl;
        }
    
    	~Phone()
        {
             cout << "Phone 析构函数的调用" << endl;
        }
    string m_PName;
};

class Person
{
    
    public:
   
    //Phone m_Phone = Pname;	隐式转换法
     Person(string name, string pName):m_Name(name) ,m_Phone(pName)
     {
         cout << "Person 构造函数的调用" << endl;
     }
    	
   	~Person()
        {                  
           cout << "Person 析构函数的调用" << endl;
   	}
    
    string m_Name;
    Phone m_Phone;
};   

//当其他类对象作为本类成员，构造是先构造类对象，再构造自身
//析构的顺序与构造相反
void test()
{
    Person p("张三", "苹果MAX");
    
    cout << p.m_Name << "使用" << p.m_Phone.m_PName << endl;
}
int main()
{
    test();
}
    
```

## 静态成员

静态成员就是在成员变量和成员函数前加上关键字static

静态成员分为：



 - 静态成员变量
   	- 所有对象共享同一份数据
      	- 在编译阶段分配内存
      	- 类内声明，类外初始化
- 静态成员函数
  - 所有对象共享同一个函数
  - 静态成员函数只能访问静态成员变量

```c++
#include <iostream>
using namespace std;

class Person
{
    
    public:
   
    static void func()
    {
        m_A = 100; //静态成员函数可以访问静态成员变量
     //m_B = 200;	静态成员函数不可以访问	非静态成员变量，无法区分到底是哪一个对象的	m_B	属性
        cout << "static void func调用" << endl;
    }
    
    static int m_A;
    int m_B;
 
    private:
    	//静态成员函数也是有访问权限的
    static void func2()
    {
        cout << "func2调用" << endl;
    }
};  

int Person::m_A = 0;

//有两种访问方式
void test()
{
    //1.通过对象访问
    Person p;
    p.func();
    
    //2.通过类名访问
    Person::func();
    
    //Person::func2();		私有权限无法访问
}
int main()
{
    test();
}
    
```

## 成员函数和成员变量分开存储

~~~c++
#include<iostream>
using namespace std;

class Person
{
	int m_A;//非静态成员变量   属于类的对象上

	static int m_B;//静态成员变量   不属于类的对象上

	void func1(){};//非静态成员函数    不属于类的对象上

	static void func2(){};//静态成员函数    不属于类的对象上
};

int Person::m_B;

void test01()
{
	Person p;
	//空对象占用内存空间为： 1
	//c++编译器会给每个空对象也分配一个字节空间，是为了区分空对象所占内存的位置
	//每个空对象也应该有一个独一无二的内存地址

	cout << "size of p = " << sizeof(p) << endl;
}

void test02()
{
	Person p;

	cout << "size of p = " << sizeof(p) << endl;
}

int main()
{

	//test01();

	test02();
}
~~~



## this指针

**this指针指向被调用的成员函数所属的对象**

this指针是隐含每一个非静态成员函数内的一种指针

this指针不需要被定义，直接使用即可



<font color=red>**this指针用途**</font>

- 当形参和成员变量同名时，可用this指针区分
- 在类的非静态成员函数中返回对象本身，可用return* this

~~~c++
#include<iostream>
using namespace std;

class Person
{
public:
	Person(int age)
	{
		//this指针指向被调用的成员函数所属的对象
		this->age = age;
	}


	Person& PersonAddAge(Person &p)
	{
		this->age += p.age;
		//this指向p2的指针，而*this指向的就是p2这个对象的本体
		return *this;
	}

	int age;
};


//1.解决名称冲突
void test01()
{
	Person p1(18);
	cout << "p1的年龄为：	" << p1.age << endl;
}

//2.返回对象本身用*this
void test02()
{

	Person p1(10);

	Person p2(10);

	//链式编程思想
	p2.PersonAddAge(p1).PersonAddAge(p1).PersonAddAge(p1).PersonAddAge(p1);

	cout << "p2的年龄为：	" << p2.age << endl;



}

int main()
{

	//test01();

	test02();
}
~~~

##  空指针访问成员函数

c++中空指针也是可以调用成员函数的，但是也要注意有没有用到**this**指针

如果用到**this**指针，需要加以判断保证代码的健壮性

~~~c++
#include<iostream>
using namespace std;

//空指针调用成员函数

class Person
{
public:
	void showClassName()
	{
		cout << "this is Person class" << endl;
	}

	void showPersonAge()
	{
		if (this == NULL)
		{
			return;
		}
		//输出	m_Age	相当于是	this->m_Age
		//传入指针为空，报错
		cout << "age = " <<m_Age << endl;
	}

	int m_Age;

};

void test01()
{
	Person* p = NULL;

	p->showClassName();

	p->showPersonAge();
}


int main()
{
	test01()；
	return 0;
}
~~~

## const修饰成员函数

**常函数：**

- 成员函数后加 const 我们称这个函数为常函数
- 常函数内不可以修改成员属性
- 成员函数声明加关键字 mutable 后，在常函数中仍然可以修改

**常对象**

- 声明对象前加 const 称该对象为常对象
- 常对象只能调用常函数

~~~c++
#include<iostream>
using namespace std;

//常函数

class Person
{
public:
	//this指针的本质是	指针常量	指针的指向是不可以修改的
	//const person* const this	第一个const限制了this不能修改指向的值，第二个限制了指向
	//在成员函数后加const，修饰的是this的指向的值，让其不能修改
	void showPerson() const
	{
		this->m_B = 100;

		//this->m_A = 100;
		//this = NULL;	//this指针不可以修改	this指针的指向
	}

	void func()
	{
		m_A = 100;
	}

	int m_A;
	mutable int m_B;//特殊变量，在常函数中也可以修改,关键字	mutable
};

void test01()
{
	Person p;
	p.showPerson();
}

void test02()
{
	const Person p;//在对象前加const，使其变为常对象
	//p.m_A = 100;
	p.m_B = 100;//m_B是特殊值，在常对象里面也可以修改

	//常对象只能调用常函数
	p.showPerson();
	//p.func();	常对象不可以调用普通成员函数，因为普通成员函数可以修改属性
}

int main()
{
	test01();
    test02();

	return 0;
}
~~~

## 友元

**友元的目的：**

​	让一个函数或者类访问	另一个类的中的私有成员

友元的关键字：friend

友元的三种实现：

- 全局函数做友元
- 类做友元
- 成员函数做友元        //合在一起写还有点问题

~~~c++
#include<string>
using namespace std;

class Building
{
	//goodGay是Bilding类的	友元	可以访问	私有属性
	friend void goodGay1(Building* building);
	friend class goodGay2;
	friend void goodGay3:: visit1();

public:
	Building()
	{
		m_SittingRoom = "客厅";
		m_BedRoom = "卧室";
	}

public:
	string m_SittingRoom;//客厅

private:
	string m_BedRoom;//卧室
};

//类做	友元
class goodGay2
{
public:

	goodGay2()
	{
		//创建一个	建筑物	对象
		building = new Building;
	}

	//访问函数	访问Building函数中的	属性
	void visit()
	{
		cout << "好基友的类	正在访问：" << building->m_SittingRoom << endl;

		cout << "好基友的类	正在访问：" << building->m_BedRoom << endl;
	}

	Building* building;
};

class goodGay3
{
public:
	goodGay3()
	{
		building = new Building;
	}

	void visit1()//让其可以访问	私有对象
	{
		cout << "好基友类的成员函数	正在访问：" << building->m_SittingRoom << endl;

		cout << "好基友类的成员函数	正在访问：" << building->m_SittingRoom << endl;
	}
	void visit2()//让其不可以访问	私有对象
	{
		cout << "好基友类的成员函数	正在访问：" << building->m_SittingRoom << endl;
	}

	Building* building;
};

//全局函数	做友元
void goodGay1(Building *building)
{
	cout << "好基友的全局函数	正在访问：" << building->m_SittingRoom << endl;

	cout << "好基友的全局函数	正在访问：" << building->m_BedRoom << endl;
}

void test01()
{
	Building building;
	goodGay1(&building);
}

void test02()
{
	goodGay2 gg;
	gg.visit();
}

void test03()
{
	goodGay3 gg;
	gg.visit1();
}

int main()
{
	test01();
	test02();
	test03();

	return 0;
}
~~~

## c++运算符重载

- 对已有的运算符进行重新定义，赋予其另一种功能，以适应不同的数据类型

### 加号运算符重载

作用：实现两个**自定义数据类型**相加的运算

特别的：对于**内置的数据类型**的表达式的运算符是**不可以**重载的

​				不要滥用运算符重载

~~~c++
# include<iostream>
using namespace std;

//加号运算符重载

class Person
{
public:

	//1.成员函数重载 +
	/*Person operator+(Person &p) {
		Person temp;
		temp.m_A = this->m_A + p.m_A;
		temp.m_B = this->m_B + p.m_B;
		return temp;
	}*/


	int m_A;
	int m_B;
};

//2.全局函数重载 +

Person operator+(Person p1, Person p2) {
	Person temp;
	temp.m_A = p1.m_A + p2.m_A;
	temp.m_B = p1.m_B + p2.m_B;
	return temp;
}

//运算符重载
Person operator+(Person p, int num) {
	Person temp;
	temp.m_A = p.m_A + num;
	temp.m_B = p.m_B + num;
	return temp;
}

void test01() {
	Person p1;
	p1.m_A = 10;
	p1.m_B = 10;
	Person p2;
	p2.m_A = 10;
	p2.m_B = 10;

	//成员函数本质调用
	//Person p3 = p1.operator+(p2);

	//全局函数本质调用
	//Person p3 = operator+(p1, p2);

	//简化形式
	Person p3 = p1 + p2;

	//运算符重载也可以发生函数重载
	Person p4 = p1 + 10;

	cout << "p3.m_A = " << p3.m_A << " p3.m_B = " << p3.m_B << endl;
	cout << "p4.m_A = " << p4.m_A << " p4.m_B = " << p4.m_B << endl;
}


int main() 
{
	test01();
}
~~~

### 左移运算符重载

作用：可以输出自定义数据类型

~~~c++
# include<iostream>
using namespace std;

class Person
{
	//友元
	friend ostream& operator<<(ostream& cout, Person p);

public:

	Person(int a, int b) {
		m_A = 10;
		m_B = 10;
	}




	//1.利用成员函数重载	左移运算符
	//p.operator<< (p)  ----  但是只有一个对象
	//p.operator<< (cout)  ----  简化版本得到的是   p << cout
	//故一般不采用成员函数重载	左移运算符<<
	//void operator<< (   ){};

private:
	int m_A;
	int m_B;
};

//2.全局函数重载 <<

//本质是 operator<<(cout, p)	---		简化	cout << p
ostream& operator<<(ostream& cout, Person p) {	//因为ostream对象全局只有一个，故采用引用的方式
	cout << "p.m_A = " << p.m_A << endl;
	cout << "p.m_B = " << p.m_B << endl;
	return cout;
}

void test01() {
	Person p(10,10);

	cout << p << endl;	//链式编程
}

int main() 
{
	test01();
}
~~~

总结：重载左移运算符配合友元可以实现输出自定义数据类型

### 递增运算符重载

作用：通过重载递增运算符，实现自己的整型数据

~~~c++
# include<iostream>
using namespace std;


//重载递增运算符

//自定义整型
class MyInteger
{
	friend ostream& operator<< (ostream &cout, MyInteger myint);
public:

	MyInteger() {
		m_Num = 0;
	}


	//重载前置++运算符		返回引用是为了一直对一个数据进行操作
	MyInteger& operator++() {
		//先进行++运算
		m_Num++;
		//再返回自身
		return *this;
	}

	//重载后置++运算符
	//void operator++(int)		int作为占位参数，用于区分前置和后置递增
	MyInteger operator++(int) {
		//先记录当前值
		MyInteger tmp = *this;
		//再递增
		m_Num++;
		//返回记录的值
		return tmp;
	}


private:
	int m_Num;

};

//全局函数重载 <<
ostream& operator<< (ostream &cout, MyInteger myint) {
	cout << myint.m_Num;
	return cout;
}

void test01() {
	MyInteger myint;

	cout << (++myint) << endl;	//链式编程
}

void test02() {
	MyInteger myint;
	cout << myint++ << endl;
	cout << myint << endl;
}

int main() 
{
	//test01();

	test02();
}
~~~

总结：**前置递增**返回的是**引用**，**后置递增**返回的是**值**

### 赋值运算符重载

作用：相当于深拷贝

~~~c++
# include<iostream>
using namespace std;

class Person
{
public:
	Person(int age) {
		m_Age = new int(age);
	}

	//重载赋值运算符
	Person& operator=(Person &p) {
		//编译器提供的是浅拷贝
		//m_Age = p.m_Age;

		//应该先判断是否有属性在堆区，如果有先释放干净，然后再深拷贝
		if (m_Age != NULL) {
			delete m_Age;
			m_Age = NULL;
		}
		//深拷贝
		m_Age = new int(*p.m_Age);

		//返回本身
		return *this;
	}

	~Person() {
		if (m_Age != NULL) {
			delete m_Age;
			m_Age = NULL;
		}
	}

	int* m_Age;

};

void test01() {
	Person p1(10);
	Person p2(20);
	Person p3(30);

	p3 = p2 = p1;

	cout << "p1的年龄为：	" << *p1.m_Age << endl;
	cout << "p2的年龄为：	" << *p2.m_Age << endl;
	cout << "p3的年龄为：	" << *p3.m_Age << endl;
}


int main() 
{
	test01();

}
~~~

### 关系运算符重载

~~~c++
# include<iostream>
#include<string>
using namespace std;


//重载关系运算符
class Person
{
public:
	Person(string name, int age) {
		m_Name = name;
		m_Age = age;
	}

	bool operator==(Person& p) {
		if (this->m_Age == p.m_Age && this->m_Name == p.m_Name)
			return true;
		return false;
	}

	bool operator!=(Person& p) {
		if (this->m_Age != p.m_Age || this->m_Name != p.m_Name)
			return true;
		return false;
	}

	string m_Name;
	int m_Age;

};

void test01() {
	Person p1("Tom", 18);
	Person p2("Jerry", 18);

	if (p1 == p2) {
		cout << "p1 和 p2 相等" << endl;
	}
	else {
		cout << "p1 和 p2 不相等" << endl;
	}
	
}

void test02() {
	Person p1("Tom", 18);
	Person p2("Jerry", 18);

	if (p1 != p2) {
		cout << "p1 和 p2 不相等" << endl;
	}
	else {
		cout << "p1 和 p2 相等" << endl;
	}
}

int main() 
{
	//test01();

	test02();

}
~~~

### 函数调用运算符重载

- 函数调用运算符	()	也可以重载
- 由于重载后的使用方式非常像函数的调用，因此称为**仿函数**
- 仿函数没有固定写法，非常灵活

~~~c++
# include<iostream>
#include<string>
using namespace std;


//函数调用运算符重载
class MyPrint
{
public:
	void operator()(string test) {
		cout << test << endl;
	}

};

void test01() {
	 MyPrint myPrint;

	 //使用起来非常类似于函数调用，所以称为仿函数
	 myPrint("Hello World");

	 //匿名函数对象，使用完后立即被释放
	 MyPrint()("Hello World");
	
	
}



int main() 
{
	test01();


}
~~~

## 继承

**继承是面向对象的三大特征之一**

### 继承的基本语法

继承的好处：减少重复代码

语法:	`class 子类 : 继承方式 父类`

子类也称为	派生类

父类也称为	基类

**派生类中的成员包括两部分**

- 一类是从基类继承过来的，一类是自己增加的成员
- 从基类继承过来的体现了其共生性，而新增的体现了其个性

### 继承方式

![image](c++%E5%AD%A6%E4%B9%A0.assets/1.png)

### 继承中的对象模型

~~~c++
# include<iostream>
#include<string>
using namespace std;

//继承中的对象模型

class Base
{
public:
	int m_A;
protected:
	int m_B;
private:
	int m_C;
};

class Son : public Base
{
public:
	int m_D;
};

void test01()
{
	//父类中所有	非静态	成员属性都会被子类继承下去
	//父类中的	私有成员	属性被编译器隐藏了,因此访问不到,但是还是会继承下去
	cout << "size of Son = " << sizeof(Son) << endl;
}

int main()
{
	test01();
}
~~~

### 继承中构造和析构顺序

- **先构造父类,再构造子类,析构的顺序与构造的顺序相反**

~~~c++
# include<iostream>
#include<string>
using namespace std;

//继承中的构造和析构顺序

class Base
{
public:
	Base()
	{
		cout << "Base的构造函数" << endl;
	}

	~Base()
	{
		cout << "Base的析构函数" << endl;
	}
};

class Son : public Base
{
public:
	Son()
	{
		cout << "Son的构造函数" << endl;
	}

	~Son()
	{
		cout << "Son的析构函数" << endl;
	}
};

void test01()
{
	Son son;
}

int main()
{
	test01();
}
~~~

### 继承同名成员处理方式

- 访问子类中同名成员	直接访问
- 访问父类中同名成员    需要加作用域

~~~c++
# include<iostream>
#include<string>
using namespace std;

//继承中同名的成员处理方式

class Base
{
public:
	Base()
	{
		m_A = 100;
	}
	void func()
	{
		cout << "Base-func的调用" << endl;
	}
	void func(int a)
	{
		cout << "Base-func(int a)的调用" << endl;
	}
	int m_A;
};

class Son : public Base
{
public:
	Son()
	{
		m_A = 200;
	}

	void func()
	{
		cout << "Son-func的调用" << endl;
	}

	int m_A;
};

//同名成员属性
void test01()
{
	Son son;
	cout << "Son	下的	m_A:	" << son.m_A << endl;
	//通过子类对象访问	父类同名成员	需要加作用域
	cout << "Base	下的	m_A:	" << son.Base::m_A << endl;
}

//同名成员函数
void test02()
{
	Son son;
	son.func();
	son.Base::func();
	//子类中出现和父类同名的成员函数,会隐藏掉父类所有的成员函数(包括重载的同名函数)
	//son.func(100);
	son.Base::func(100);
}

int main()
{
	//test01();

	test02();
}
~~~

### 继承同名静态成员处理方式

静态成员和非静态成员出现同名处理方式一致

- 访问子类中同名成员	直接访问
- 访问父类中同名成员    需要加作用域

### 多继承语法

c++允许**一个类继承多个类**

语法:`class 子类 :	继承方式	父类1	,	继承方式	父类2...`

多继承可能引发父类中有同名成员出现,需要加作用域区分

~~~c++
# include<iostream>
#include<string>
using namespace std;

//继承中同名的成员处理方式

class Base1
{
public:
	Base1()
	{
		m_A = 100;
	}

	int m_A;
};

class Base2
{
public:
	Base2()
	{
		m_A = 200;
	}

	int m_A;
};

//子类需要	继承Base1和Base2
class Son : public Base1, public Base2
{
public:
	Son()
	{
		m_C = 300;
		m_D = 400;
	}

	int m_C;
	int m_D;
};

//同名成员属性
void test01()
{
	Son s;
	cout << "size of Son = " << sizeof(Son) << endl;

	//当父类中出现同名成员,需要加作用域区分
	cout << "Base1 -- m_A = " << s.Base1::m_A << endl;
	cout << "Base2 -- m_A = " << s.Base2::m_A << endl;
}


int main()
{
	test01();

}
~~~

### 菱形继承

概念:

- 两个派生类继承同一个基类
- 又有某个类同时继承这两个派生类
- 这种继承被称为菱形继承,或者砖石继承

~~~c++
# include<iostream>
#include<string>
using namespace std;

//动物类
class Animal
{
public:
	int m_Age;
};

//利用虚继承	可以解决菱形继承的问题
//继承之前加上关键字	virtual	变为虚继承
//Animal为虚基类

//羊类
class Sheep : virtual public Animal{};

//驼类
class Tuo : virtual public Animal {};

//羊驼类
class SheepTuo :public Sheep, public Tuo{};


void test01()
{
	SheepTuo st;

	st.Sheep::m_Age = 18;
	st.Tuo::m_Age = 28;

	cout << "Sheep - m_Age = " << st.Sheep::m_Age << endl;
	cout << "Tuo - m_Age = " << st.Tuo::m_Age << endl;
	//只需要1分数据就够了,两份数据造成了资源浪费
	cout << st.m_Age << endl;
}

int main()
{
	test01();

}
~~~

## 多态

多态是c++面向对象三大特征之一

### 多态的基本概念

多态分为两类:

- 静态多态:**函数重载**和**运算符重载**属于静态多态,复用函数名
- 动态多态:派生类和虚函数实现运行时多态

静态多态和动态多态的区别:

- 静态多态的地址早绑定:编译阶段确定函数地址
- 动态多态的地址晚绑定:运行阶段确定函数地址

~~~c++
# include<iostream>
#include<string>
using namespace std;

//多态

//动态多态满足条件
//1.有继承关系
//2.子类要重写父类中的虚函数	重写:	函数返回值类型	函数名	参数列表	完全相同

//动态多态使用
//父类的指针或者引用	指向子类对象


//动物类
class Animal
{
public:
	virtual void speak()
	{
		cout << "动物在说话" << endl;
	}
};


//猫类
class Cat : public Animal
{
	void speak()
	{
		cout << "小猫在说话" << endl;
	}
};

//狗类
class Dog :public Animal
{
	void speak()
	{
		cout << "小狗在说话" << endl;
	}
};

//执行说话的函数
//地址早绑定
//如果想要不出现动物在说话	就要让地址晚绑定
void doSpeak(Animal &animal)	//Animal &animal = cat;
{
	animal.speak();
}

void test01()
{
	Cat cat;
	doSpeak(cat);
	
	Dog dog;
	doSpeak(dog);
}

int main()
{
	test01();

}
~~~

动态多态满足条件:

- 有继承关系
- 子类要重写父类中的虚函数

动态多态使用:

- 父类的指针或者引用	指向子类对象

重写:	函数返回值类型	函数名	参数列表	完全相同

### 多态的原理

对上一段代码

​		父类中的speak函数未添加	virtual	时

![image](c++%E5%AD%A6%E4%B9%A0.assets/2-1603615412030.png)

​		父类中的speak函数添加	virtual	时

![image](c++%E5%AD%A6%E4%B9%A0.assets/1-1603615462438.png)

​		子类Cat不重写speak函数时

![image](c++%E5%AD%A6%E4%B9%A0.assets/3.png)

​		子类Cat重写speak函数时

![image](c++%E5%AD%A6%E4%B9%A0.assets/4.png)

### 多态案例---计算器

多态的优点:

- 代码组织结构清晰
- 可读性强
- 利于前期和后期的扩展以及维护

~~~c++
# include<iostream>
#include<string>
using namespace std;

//抽象类
class AbstractCaculator
{
public:
	virtual int GetResult()
	{
		return 0;
	}

	int m_Num1;
	int m_Num2;
};

//加法计算类
class AddCaculator :public AbstractCaculator
{
public:
	int GetResult()
	{
		return m_Num1 + m_Num2;
	}
};
//减法计算类
class SubCaculator :public AbstractCaculator
{
public:
	int GetResult()
	{
		return m_Num1 - m_Num2;
	}
};
//乘法计算类
class MulCaculator :public AbstractCaculator
{
public:
	int GetResult()
	{
		return m_Num1 * m_Num2;
	}
};

void test01()
{
	//加法计算
	AbstractCaculator *abc = new AddCaculator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 10;

	cout << abc->m_Num1 << " + " << abc->m_Num2 << " = " << abc->GetResult() << endl;
	//用完释放
	delete abc;

	//减法运算
	abc = new SubCaculator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 10;

	cout << abc->m_Num1 << " - " << abc->m_Num2 << " = " << abc->GetResult() << endl;
	//用完释放
	delete abc;

	//乘法运算
	abc = new MulCaculator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 10;

	cout << abc->m_Num1 << " * " << abc->m_Num2 << " = " << abc->GetResult() << endl;
	//用完释放
	delete abc;
}

int main()
{
	test01();


}
~~~

c++提倡利用多态设计程序架构,因为多态优点很多

### 纯虚函数和抽象类

在多态中,通常父类中虚函数的实现是毫无意义的,主要都是调用子类中重写的内容,因此可以将虚函数改为**纯虚函数**

语法:`virtual	返回值类型	函数名	(参数列表) = 0`

当类中有了纯虚函数,这个类也被称为<font color=red> 抽象类</font>

抽象类特点:

- 无法实例化对象
- 子类必须重写抽象类中的纯虚函数,否则也属于抽象类

~~~c++
# include<iostream>
#include<string>
using namespace std;


class Base
{
public:
	//纯虚函数
	virtual void func() = 0;
	
};

class Son1 : public Base
{

};

class Son2 :public Base
{
public:
	void func()
	{
		return;
	}
};

void test01()
{
	//无法实例化对象
	//Base b;
	//new Base;
	//Son1 s;	子类未重写父类的虚函数

	Son2 s;
}

int main()
{
	test01();


}
~~~

### 多态案例--制作饮品

~~~c++
# include<iostream>
#include<string>
using namespace std;


class AbstractckDrinking
{
public:
	
	//煮水
	virtual void Boil() = 0;
	
	//冲泡
	virtual void Brew() = 0;

	//倒入杯中
	virtual void PourInCup() = 0;

	//加入辅料
	virtual void PutSomething() = 0;

	//制作饮品
	void MarkDrink()
	{
		Boil();
		Brew();
		PourInCup();
		PutSomething();
	}
};

//制作咖啡
class Coffee : public AbstractckDrinking
{
public:
	//煮水
	void Boil()
	{
		cout << "煮水" << endl;
	}

	//冲泡
	void Brew()
	{
		cout << "冲泡咖啡" << endl;
	}

	//倒入杯中
	void PourInCup()
	{
		cout << "倒入杯中" << endl;
	}

	//加入辅料
	void PutSomething()
	{
		cout << "加入糖和牛奶" << endl;
	}

};

//制作茶
class Tea : public AbstractckDrinking
{
public:
	//煮水
	void Boil()
	{
		cout << "煮矿泉水" << endl;
	}

	//冲泡
	void Brew()
	{
		cout << "冲泡茶叶" << endl;
	}

	//倒入杯中
	void PourInCup()
	{
		cout << "倒入杯中" << endl;
	}

	//加入辅料
	void PutSomething()
	{
		cout << "加入柠檬" << endl;
	}

};

//制作函数
void doWork(AbstractckDrinking* abs)
{
	abs->MarkDrink();
	delete abs;
}

void test01()
{
	//制作咖啡
	doWork(new Coffee);

	cout << "----------" << endl;

	//制作茶
	doWork(new Tea);
}

int main()
{
	test01();


}
~~~

### 虚析构和纯虚析构

多态使用时,如果子类有属性开辟到堆区,那么父类指针在释放时无法调用到子类的虚构代码

解决方式:

- 将父类中的析构函数改为**虚析构和纯虚析构**



虚析构和纯虚析构共性:

- 可以解决父类指针释放子类对象
- 都需要有具体的函数实现

虚析构和纯虚析构区别:

- 如果是纯虚析构,该类属于**抽象类**,无法实例化对象

虚析构语法:

`virtual	~类名(){}`

纯虚析构语法

`virtual ~类名() = 0`

`类名::类名(){}`

~~~c++
#include<iostream>
#include<string>
using namespace std;

//虚析构和纯虚析构
class Animal
{
public:
	Animal()
	{
		cout << "Animal的构造函数调用" << endl;
	}

	//纯虚函数
	virtual void speak() = 0;

	//虚析构函数可以解决	父类指针释放子类对象时不干净的问题
	/*virtual ~Animal()
	{
		cout << "Animal的虚析构函数调用" << endl;
	}*/

	//纯虚析构	报错,因为父类可能也有在堆区开辟的数据,所以需要对纯虚析构函数进行定义
	virtual ~Animal() = 0;
	//有了纯虚析构函数后,该类也属于抽象类,无法实例化对象
};
Animal::~Animal()
{
	cout << "Animal的纯虚析构函数调用" << endl;
}


//制作咖啡
class Cat : public Animal
{
public:
	Cat(string name)
	{
		cout << "Cat的构造函数调用" << endl;
		m_Name = new string(name);
	}

	void speak()
	{
		cout << *m_Name << "小猫在说话" << endl;
	}

	~Cat()
	{
		if (m_Name != NULL)
		{
			cout << "Cat的析构函数调用" << endl;
			delete m_Name;
			m_Name = NULL;
		}
		
	}
	
	string *m_Name;
};


void test01()
{
	Animal* animal = new Cat("Tom");
	animal->speak();
	//父类指针在析构时候	不会调用子类的析构函数,如果子类有堆区,不会被释放,导致内存泄露
	delete animal;

}

int main()
{
	test01();


}
~~~

### 多态案例--电脑组装



~~~c++
#include<iostream>
#include<string>
using namespace std;

//抽象不同的零件类
//抽象CPU类
class CPU
{
public:
	//抽象的计算函数
	virtual void calculate() = 0;
};

//抽象显卡类
class VideoCard
{
public:
	//抽象的显示函数
	virtual void display() = 0;
};

//抽象内存条类
class Memory
{
public:
	//抽象的存储函数
	virtual void storage() = 0;
};

//电脑类
class Computer
{
public:
	Computer(CPU* cpu, VideoCard* vc, Memory* mem)
	{
		m_cpu = cpu;
		m_vc = vc;
		m_mem = mem;
	}

	//提供工作的函数
	void work()
	{
		//让零件工作起来,调用实现接口
		m_cpu->calculate();
		m_vc->display();
		m_mem->storage();
	}

	//提供析构函数,释放3个电脑零件
	~Computer()
	{
		//释放cpu
		if (m_cpu != NULL)
		{
			delete m_cpu;
			m_cpu = NULL;
		}
		//释放显卡
		if (m_vc != NULL)
		{
			delete m_vc;
			m_vc = NULL;
		}
		//释放内存条
		if (m_mem != NULL)
		{
			delete m_mem;
			m_mem = NULL;
		}
	}

private:
	CPU* m_cpu;	//CPU的零件指针
	VideoCard* m_vc;	//显卡的零件指针
	Memory* m_mem;	//内存条额零件指针

};

//具体厂商
//Inter厂商
class InterCPU :public CPU
{
	void calculate()
	{
		cout << "Inter的CPU开始计算了!!" << endl;
	}
};

class InterMemory :public Memory
{
	void storage()
	{
		cout << "Inter的内存条开始存储了!" << endl;
	}
};

class InterVideoCard :public VideoCard
{
	void display()
	{
		cout << "Inter的显卡开始显示了" << endl;
	}
};

//Lenovo厂商
class LenovoCPU :public CPU
{
	void calculate()
	{
		cout << "Lenovo的CPU开始计算了!" << endl;
	}
};

class LenovoMemory :public Memory
{
	void storage()
	{
		cout << "Lenovo的内存条开始存储了!" << endl;
	}
};

class LenovoVideoCard :public VideoCard
{
	void display()
	{
		cout << "Lenovo的显卡开始显示了!" << endl;
	}
};

void test01()
{
	//第一台电脑零件
	CPU* interCPU = new InterCPU;
	VideoCard* interCard = new InterVideoCard;
	Memory* interMem = new InterMemory;

	cout << "第一台电脑开始工作" << endl;
	//创建第一台电脑
	Computer* computer1 = new Computer(interCPU, interCard, interMem);
	computer1->work();
	delete computer1;

	cout << "--------------" << endl;
	cout << "第二台电脑开始工作" << endl;
	//创建第二台电脑
	Computer* computer2= new Computer(new LenovoCPU, new LenovoVideoCard, new LenovoMemory);
	computer2->work();
	delete computer2;
}

int main()
{
	test01();
}
~~~

## 文件操作

程序运行时的数据都属于临时数据,程序一旦运行结束都会被释放

通过**文件操作可以将数据持久化**

c++中对文件进行操作需要包含头文件<fstream>



文件类型分为两类:

1. **文本文件 **   --    文件以文本的**ASCII码**形式存储在计算机中
2. **二进制文件**    --    文本以文本的**二进制**形式存储在计算机中



操作文件的三大类

1. ofstream : 写操作
2. ifstream : 读操作
3. fstream : 读写操作

### 文本文件

#### 写文件

步骤:

1. 包含头文件

   ​	#include<fstream>

2. 创建流对象

   ​	ofstream ofs;

3. 打开文件

   ​	ofs.open("文件路径", 打开方式);

4. 写数据

   ​	ofs << "写入的数据";

5. 关闭文件

   ​	ofs.close();

| 打开方式    | 解释                      |
| ----------- | ------------------------- |
| ios::in     | 为读文件而打开文件        |
| ios::out    | 为写文件而打开文件        |
| ios::ate    | 初始位置: 文件尾          |
| ios::app    | 追加方式写文件            |
| ios::trunc  | 如果文件存在,先删除再创建 |
| ios::binary | 二进制方式                |

**注意:**	文件打开方式可以配合使用,利用|运算符

​	**例如:**	用二进制方式写文件	`ios::binary	|	ios::out`

~~~c++
#include<iostream>
#include<fstream>	//文件操作的头文件
using namespace std;

//文本文件	写文件

void test01()
{
	//创建流对象
	ofstream ofs;

	//指定打开方式
	ofs.open("test.txt", ios::out);

	//写内容
	ofs << "姓名:张三" << endl;
	ofs << "性别:男" << endl;
	ofs << "年龄:18" << endl;

	//关闭文件
	ofs.close();
}

int main()
{
	test01();
}
~~~

#### 读文件

步骤:

步骤:

1. 包含头文件

   ​	#include<fstream>

2. 创建流对象

   ​	ifstream ifs;

3. 打开文件并判断文件是否打开成功

   ​	ifs.open("文件路径", 打开方式);

4. 读数据

   ​	四种方式读取

5. 关闭文件

   ​	ifs.close();

~~~c++
#include<iostream>
#include<string>
#include<fstream>	//文件操作的头文件
using namespace std;

//文本文件	读文件
void test01()
{
	//创建流对象
	ifstream ifs;

	//打开文件并判断是否打开成功
	ifs.open("test.txt", ios::in);

	if (!ifs.is_open())
	{
		cout << "文件打开失败" << endl;
		return;
	}

	//读数据
	//第一种
	/*char buf[1024] = { 0 };
	while (ifs >> buf)
	{
		cout << buf << endl;
	}*/

	//第二种
	/*char buf[1024] = { 0 };
	while (ifs.getline(buf, sizeof(buf)))
	{
		cout << buf << endl;
	}*/

	//第三种
	/*string buf;
	while ( getline(ifs, buf))
	{
		cout << buf << endl;
	}*/

	//第四种
	char c;
	while ((c = ifs.get()) != EOF)	//EOF end of file 文件尾
	{
		cout << c;
	}

	//关闭文件
	ifs.close();
}

int main()
{
	test01();
}
~~~

### 二进制文件

以二进制方式对文件进行读写操作

打开方式要指定为:	**ios::binary**

#### 写文件

二进制方式写文件主要利用流对象调用成员函数write

函数原型:	`ostream& write(const char * buffer, int len)`

参数解释:	字符指针buffer指向内存中一段存储空间, len是读写的字节数

~~~c++
#include<iostream>
#include<string>
#include<fstream>	//文件操作的头文件
using namespace std;

//二进制文件	写文件
class Person
{
public:

	char m_Name[64];
	int m_Age;
};

void test01()
{
	//创建流对象
	ofstream ofs("person.txt", ios::binary | ios::out);//ofs的构造函数

	//指定打开方式
	//ofs.open("person.txt", ios::binary | ios::out);

	//写内容
	Person p = { "张三", 18 };
	ofs.write((const char*)& p, sizeof(Person));

	//关闭文件
	ofs.close();
}

int main()
{
	test01();
}
~~~

#### 读文件

二进制方式写文件主要利用流对象调用成员函数read

函数原型:	`istream& read(char * buffer, int len)`

参数解释:	字符指针buffer指向内存中一段存储空间, len是读写的字节数

~~~c++
#include<iostream>
#include<string>
#include<fstream>	//文件操作的头文件
using namespace std;

//二进制文件	写文件
class Person
{
public:

	char m_Name[64];
	int m_Age;
};

//文本文件	读文件
void test01()
{
	//创建流对象
	ifstream ifs;

	//打开文件并判断是否打开成功
	ifs.open("person.txt", ios::binary | ios::in);

	if (!ifs.is_open())
	{
		cout << "文件打开失败" << endl;
		return;
	}

	//读数据
	Person p;
	ifs.read((char*)&p, sizeof(p));
	cout << "姓名为: " << p.m_Name << "	年龄为: " << p.m_Age << endl;
	//关闭文件
	ifs.close();
}

int main()
{
	test01();
}
~~~

# c++提高编程



## 模板

- c++另一种编程思想称为 **泛型编程** ,主要利用的技术就是模板
- c++提供两种模板机制: **函数模板**和**类模板**

概念:	建立通用的模具,提高复用性

特点:

- 模板不可以直接使用,它只是一个框架
- 模板的通用并不是万能的

### 函数模板

作用:

​	建立一个通用函数,其函数返回值类型和形参类型可以不具体制定,用一个**虚拟的类型**来代表.

语法

~~~c++
template<typename T>
函数声明或定义
~~~

template	--	声明创建模板

typename	--	表面其后面的符号是一种数据类型,可以用class代替

T	--	通用的数据类型,名称可以替换,通常为大写字母

~~~c++
#include<iostream>
using namespace std;

//交换两个整型
void swapInt(int& a, int& b)
{
	int temp = a;
	a = b;
	b = temp;
}

//交换两个浮点型
void swapDouble(double& a, double& b)
{
	double temp = a;
	a = b;
	b = temp;
}

//函数模板
template<typename T>	//声明一个模板,告诉编译器后面代码中紧跟的T不要报错,T是一个通用数据类型
void mySwap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;
}

void test01()
{
	int a = 10;
	int b = 20;
	/*swapInt(a, b);*/

	//利用函数模板交换
	//两种方式使用函数模板
	//1.自动类型推导
	//mySwap(a, b);

	//2.显示指定类型
	mySwap<int>(a, b);
	cout << "a = " << a << endl;
	cout << "b = " << b << endl;

	/*double c = 2.1;
	double d = 1.2;
	swapDouble(c, d);
	cout << "c = " << c << endl;
	cout << "d = " << d << endl;*/
}

int main()
{
	test01();

	system("pause");
}
~~~

总结:

- 关键字:	template

- 两种方式使用函数模板
  1.自动类型推导

  2.显示指定类型

- 模板的目的是提高代码的复用性,将类型参数化

#### 函数模板注意事项

- 自动类型推导,必须推导出一致的数据类型T,才能使用
- 模板必须要确定出T的数据类型,才可以使用

~~~c++
#include<iostream>
using namespace std;

//函数模板注意事项

template<typename T>
void mySwap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;
}

//1.自动类型推导,必须推导出一致的数据类型T,才能使用
void test01()
{
	int a = 10;
	int b = 20;
	//mySwap(a, b);	//正确

	char c = 'c';
	//mySwap(a, c);//错误 ,推导不出一致的的T类型
}

//2.模板必须要确定出T的数据类型,才可以使用
template<typename T>
void fun()
{
	cout << "fun 函数调用" << endl;
}

void test02()
{
	//fun();	//T的类型不确定,无法调用

	fun<int>();	//可以随意指定一个T的类型
}

int main()
{
	test01();

	test02();

	system("pause");
}
~~~

总结:	使用模板必须要确定出T的数据类型,并且可以推出一致的数据类型

#### 函数模板案例

案例描述:

- 利用函数模板封装一个排序的函数，可以对不同数据类型数组进行排序
- 排序规则从大到小，排序算法为选择排序
- 分别利用char数组和int数组进行测试

~~~c++
#include<iostream>
using namespace std;

template<typename T>
void mySort(T arry[], int len)
{
	for (int i = 0; i < len; i++)
	{
		int max = i;
		for (int j = i; j < len; j++)
		{
			if (arry[max] < arry[j])
				max = j;
		}
		if (max != i)
		{
			T temp = arry[max];
			arry[max] = arry[i];
			arry[i] = temp;
		}
	}
}

//测试char数组
void test01()
{
	char charArry[] = "bedca";
	int len = sizeof(charArry) / sizeof(char);
	mySort(charArry, len);

	for (int i = 0; i < len; i++)
	{
		cout << charArry[i] << " ";
	}
}

//测试int数组
void test02()
{
	int intArry[] = { 1,2,3,5,6,4, };
	int len = sizeof(intArry) / sizeof(int);
	mySort(intArry, len);

	for (int i = 0; i < len; i++)
	{
		cout << intArry[i] << " ";
	}
}

int main()
{
	test01();

	test02();

	system("pause");
}
~~~

#### 普通函数和函数模板的区别

区别:

- 普通函数调用时可以发生自动类型转换(隐式类型转换)
- 函数模板调用时，如果利用自动类型推导，不会发生隐式类型转换
- 如果利用显示指定类型的方式，可以发生隐式类型转换

~~~c++
#include<iostream>
using namespace std;

int myAdd01(int a, int b)
{
	return a + b;
}

template<typename T>
int myAdd02(T a, T b)
{
	return a + b;
}


void test01()
{
	int a = 10;
	char b = 'b';
	cout << myAdd01(a, b) << endl;		//发生隐式类型转换

	//cout << myAdd02(a, b) << endl;

	cout << myAdd02<int>(a, b) << endl;	//发生隐式类型转换
}



int main()
{
	test01();

	system("pause");
}
~~~

#### 普通函数与函数模板的调用规则

规则:

1. 如果函数模板和普通函数都可以实现，优先调用普通函数
2. 可以通过空模板参数列表来强制调用函数模板
3. 函数模板也可以发生重载
4. 如果函数模板可以产生更好的匹配,优先调用函数模板

~~~c++
#include<iostream>
using namespace std;

void myPrint(int a, int b)
{
	cout << "这是一个普通函数" << endl;
}

template<typename T>
void myPrint(T a, T b)
{
	cout << "这是一个模板函数" << endl;
}

template<typename T>
void myPrint(T a, T b, T c)
{
	cout << "这是一个重载模板函数" << endl;
}

void test01()
{
	//默认调用普通函数
	//myPrint(1, 2);

	//通过空模板参数列表,强制调用模板函数
	myPrint<>(1, 2);

	//调用重载模板函数
	myPrint(1, 2, 3);

	//如果函数模板可以产生更好的匹配,优先调用函数模板
	myPrint('a', 'b');	//如果调用普通函数会发生隐式类型转换,故调用模板函数
}


int main()
{
	test01();

	system("pause");
}
~~~

- 提供了模板函数就不要提供普通函数,防止产生二义性

#### 模板的局限性

~~~c++
#include<iostream>
using namespace std;

class Person
{
public:

	Person(string name, int age)
	{
		m_Name = name;
		m_Age = age;
	}
	string m_Name;

	int m_Age;
};


template<typename T>
bool myCompare(T a, T b)
{
	if (a == b)
		return true;
	return false;
}

//利用具体化Person的版本实现代码,具体化优先调用
template<>bool myCompare(Person p1, Person p2)
{
	if (p1.m_Name == p2.m_Name && p1.m_Age == p2.m_Age)
		return true;
	return false;
}

void test01()
{
	int a = 10;
	int b = 20;

	bool ret = myCompare(a, b);
	if (ret)
	{
		cout << "a == b" << endl;
	}
	else
	{
		cout << "a != b" << endl;
	}
}

void test02()
{
	Person p1("Tom", 19);
	Person p2("Tom", 19);

	bool ret = myCompare(p1, p2);
	if (ret)
	{
		cout << "p1 == p2" << endl;
	}
	else
	{
		cout << "p1 != p2" << endl;
	}
}


int main()
{
	//test01();

	test02();

	system("pause");
}
~~~

总结:

- 利用具体化的模板,可以解决自定义类型的通用化.
- 学习模板并不是为了写模板,而是可以在STL中运用系统提供的模板

## 类模板

#### 语法

作用:

- 建立一个通用类，类中的成员数据类型可以不具体制定，用一个虚拟的类型来代表。

语法:

~~~c++
template<typename T>
类
~~~

解释:

template ---声明创建模板

typename ---表面其后面的符号是一种数据类型，可以用class代替

T---通用的数据类型，名称可以替换，通常为大写字母

~~~c++
#include<iostream>
using namespace std;

template<class NameType, class AgeType>
class Person
{
public:

	Person(NameType name, AgeType age)
	{
		m_Name = name;
		m_Age = age;
	}

	void showPerson()
	{
		cout << "name: " << m_Name << " age: " << m_Age << endl;
	}

	NameType m_Name;

	AgeType m_Age;
};



void test01()
{
	//指定NameType 为string类型，AgeType 为int类型
	Person<string,int> p1("张三", 999);
	p1.showPerson();
}


int main()
{
	test01();

	system("pause");
}
~~~

#### 类模板与函数模板的区别

类模板与函数模板区别主要有两点:

1. 类模板没有自动类型推导的使用方式
2. 类模板在模板参数列表中可以有默认参数

~~~c++
#include<iostream>
using namespace std;

//类模板在模板参数列表中可以有默认参数
template<class NameType, class AgeType = int>
class Person
{
public:

	Person(NameType name, AgeType age)
	{
		m_Name = name;
		m_Age = age;
	}

	void showPerson()
	{
		cout << "name: " << m_Name << " age: " << m_Age << endl;
	}

	NameType m_Name;

	AgeType m_Age;
};


//类模板没有自动类型推导的使用方式
void test01()
{

	//Person p1("张三", 999);  错误,无法使用自动类型推导

	Person<string,int> p("张三", 999);
	p.showPerson();
}

void test02()
{
	Person<string> p("李四", 999);
	p.showPerson();
}

int main()
{
	//test01();

	test02();

	system("pause");
}
~~~

#### 类模板中的成员函数创建时机

类模板中成员函数和普通类中成员函数创建时机是有区别的:

- 普通类中的成员函数—开始就可以创建
- **类模板中的成员函数在调用时才创建**

~~~c++
#include<iostream>
using namespace std;

class Person1
{
public:
	void showPerson1()
	{
		cout << "showPerson1" << endl;
	}	
};

class Person2
{
public:
	void showPerson2()
	{
		cout << "showPerson2" << endl;
	}
};


template<class T>
class myClass{
public:
	T obj;
	void fun1()
	{
		obj.showPerson1();
	}

	void fun2()
	{
		obj.showPerson2();
	}
};

//类模板中的成员函数在调用时才创建
void test01()
{
	myClass<Person1> a;
	a.fun1();
	//a.fun2();	编译会报错,说明类模板中的成员函数在调用时才创建
	
}


int main()
{
	test01();

	system("pause");
}
~~~

#### 类模板对象做函数参数

- 类模板实例化出的对象，向函数传参的方式

三种传参方式:

1. 指定传入的类型      ---直接显示对象的数据类型
2. 参数模板化              ---将对象中的参数变为模板进行传递
3. 整个类模板化          ---将这个对象类型模板化进行传递

~~~c++
#include<iostream>
using namespace std;


template<class T1, class T2>
class Person{
public:

	Person(T1 name, T2 age)
	{
		m_Name = name;
		m_Age = age;
	}
	void showPerson()
	{
		cout << "姓名: " << m_Name << " 年龄: " << m_Age << endl;
	}

	T1 m_Name;
	T2 m_Age;
};

//指定传入的类型
void printPerson1(Person<string, int>p)
{
	p.showPerson();
}

void test01()
{
	Person<string, int>p("孙悟空", 100);
	printPerson1(p);
}

//参数模板化
template<class T1, class T2>
void printPerson2(Person<T1, T2>p)
{
	p.showPerson();
	cout << "T1的类型为: " << typeid(T1).name() << endl;
	cout << "T2的类型为: " << typeid(T2).name() << endl;
}

void test02()
{
	Person<string, int>p("猪八戒", 90);
	printPerson2(p);
}

//整个类模板化
template<class T>
void printPerson3(T p)
{
	p.showPerson();
	cout << "T 的 类型: " << typeid(T).name() << endl;
}

void test03()
{
	Person<string, int>p("唐僧", 90);
	printPerson3(p);
}


int main()
{
	//test01();

	//test02();

	test03();

	system("pause");
}
~~~

#### 类模板与继承

当类模板碰到继承时，需要注意下面几点:

- 当子类继承的父类是一个类模板时，子类在声明的时候，要指定出父类中T的类型
- 如果不指定，编译器无法给子类分配内存
- 如果想灵活指定出父类中T的类型，子类也需变为类模板

~~~c++
#include<iostream>
using namespace std;

template<class T1>
class Base
{
public:

	T1 a;
};

//class Son :public Base//错误,不知道父类中的数据类型
class Son :public Base<int>
{

};

//如果想灵活指定出父类中T的类型，子类也需变为类模板
template<class T1,class T2>
class Son2 :public Base<T2>
{
public:
	Son2()
	{
		cout << "T1的数据类型" << typeid(T1).name() << endl;
		cout << "T2的数据类型" << typeid(T2).name() << endl;
	}

	T1 b;
};


void test01()
{
	Son2<int, char> a;
}




int main()
{
	test01();

	system("pause");
}
~~~

#### 类模板成员函数类外实现

~~~c++
#include<iostream>
using namespace std;

template<class T1, class T2>
class Person{
public:

	Person(T1 name, T2 age);

	void showPerson();
	

	T1 m_Name;
	T2 m_Age;
};

//构造函数类外实现
template<class T1,class T2>
Person<T1, T2>::Person(T1 name, T2 age)
{
	m_Name = name;
	m_Age = age;
}

//成员函数类外实现
template<class T1,class T2>
void Person<T1, T2>::showPerson()
{
	cout << "姓名: " << m_Name << " 年龄: " << m_Age << endl;
}

void test01()
{
	Person<string, int>p("Tom", 18);
	p.showPerson();
}


int main()
{
	test01();
	system("pause");
}
~~~

#### 类模板分文件编写

- 掌握类模板成员函数分文件编写产生的问题以及解决方式

问题:

- 类模板中成员函数创建时机是在调用阶段，导致分文件编写时链接不到

解决:

- 解决方式1:直接包含.cpp源文件
- 解决方式2∶将声明和实现写到同一个文件中，并更改后缀名为.hpp，hpp是约定的名称，并不是强制



Person.hpp内容

~~~c++
#pragma once
#include<iostream>
using namespace std;

template<class T1, class T2>
class Person {
public:

	Person(T1 name, T2 age);

	void showPerson();


	T1 m_Name;
	T2 m_Age;
};

//构造函数类外实现
template<class T1, class T2>
Person<T1, T2>::Person(T1 name, T2 age)
{
	m_Name = name;
	m_Age = age;
}

//成员函数类外实现
template<class T1, class T2>
void Person<T1, T2>::showPerson()
{
	cout << "姓名: " << m_Name << " 年龄: " << m_Age << endl;
}
~~~



test.cpp内容

~~~c++
#include<iostream>
using namespace std;

//无法生成
//#include"Person.h"

//第一种解决方式,直接包含源码
//#include"Person.cpp"

//第二种解决方式,将声明和实现写到同一个文件中，并更改后缀名为.hpp
#include"Person.hpp"

//template<class T1, class T2>
//class Person{
//public:
//
//	Person(T1 name, T2 age);
//
//	void showPerson();
//	
//
//	T1 m_Name;
//	T2 m_Age;
//};

//构造函数类外实现
//template<class T1,class T2>
//Person<T1, T2>::Person(T1 name, T2 age)
//{
//	m_Name = name;
//	m_Age = age;
//}
//
////成员函数类外实现
//template<class T1,class T2>
//void Person<T1, T2>::showPerson()
//{
//	cout << "姓名: " << m_Name << " 年龄: " << m_Age << endl;
//}

void test01()
{
	Person<string, int>p("Tom", 18);
	p.showPerson();
}


int main()
{
	test01();
	system("pause");
}
~~~

#### 类模板与友元

- 掌握类模板配合友元函数的类内和类外实现



全局函数类内实现–直接在类内声明友元即可

全局函数类外实现–需要提前让编译器知道全局函数的存在

~~~c++
#include<iostream>
#include<string>
using namespace std;

//全局函数类外实现
template<class T1, class T2>
class Person;

template<class T1, class T2>
void printPerson2(Person<T1, T2>p)
{
	cout << "姓名: " << p.m_Name << " 年龄: " << p.m_Age << endl;
}

template<class T1, class T2>
class Person
{
	//全局函数在类内实现
	friend void printPerson(Person<T1, T2>p)
	{
		cout << "姓名: " << p.m_Name << " 年龄: " << p.m_Age << endl;
	}

	//全局函数类外实现需要加空参数列表
	//全局函数类外实现,需要让编译器提前知道这个函数
	friend void printPerson2<>(Person<string, int>p);

public:
	Person(T1 name, T2 age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}

private:
	T1 m_Name;
	T2 m_Age;
};


void test01()
{
	Person<string, int>p("Tom", 19);
	printPerson(p);

}

void test02()
{
	Person<string, int>p("Jerry", 19);
	printPerson2(p);

}


int main()
{
	//test01();

	test02();
	system("pause");
}
~~~

- 建议全局函数类内实现,用法简单

#### 类模板案例

案例描述:实现一个通用的数组类，要求如下:

- 可以对内置数据类型以及自定义数据类型的数据进行存储
- 将数组中的数据存储到堆区
- 提供对应的拷贝构造函数以及operator=防止浅拷贝问题
- 提供尾插法和尾删法对数组中的数据进行增加和删除可以通过下标的方式访问数组中的元素
- 可以获取数组中当前元素个数和数组的容量



MyArray.hpp

~~~c++
//我自己的通用数组类
#pragma once
#include<iostream>
using namespace std;

template<class T>
class MyArray
{
public:

	//有参构造
	MyArray(int Capacity)
	{
		this->m_Capacity = Capacity;
		this->m_Size = 0;
		this->pAddress = new T[this->m_Capacity];
	}

	//深拷贝
	MyArray(const MyArray& arr)
	{
		this->m_Capacity = arr.m_Capacity;
		this->m_Size = arr.m_Size;

		this->pAddress = new T[this->m_Capacity];

		//把数据拷贝过来
		for (int i = 0; i < this->m_Size; i++)
		{
			this->pAddress[i] = arr.pAddress[i];
		}
	}

	//operator= 防止浅拷贝问题
	MyArray& operator=(const MyArray &arr)
	{
		//先判断原来的堆区是否有数据
		if (this->pAddress != NULL)
		{
			delete[] this->pAddress;
			this->pAddress = NULL;
			this->m_Size = 0;
			this->m_Capacity = 0;
		}

		//深拷贝
		this->m_Capacity = arr.m_Capacity;
		this->m_Size = arr.m_Size;
		this->pAddress = new T[this->m_Capacity];
		for (int i = 0; i < this->m_Size; i++)
		{
			this->pAddress[i] = arr.pAddress[i];
		}

		return *this;
	}

	//尾插法
	void Push_Back(T& val)
	{
		//判断数组是否已满
		if (this->m_Capacity == this->m_Size)
		{
			return;
		}
		this->pAddress[this->m_Size] = val;
		this->m_Size++;		//更新数组大小
	}

	//尾删法
	void Pop_Back()
	{
		//让用户访问不到最后一个元素,即为尾删,逻辑删除
		if (this->m_Size == 0)
		{
			return;
		}
		this->m_Size--;
	}

	//通过下标访问数组  还要可以作为左值存在 arr[0] = 100;
	T& operator[](int index)
	{
		return this->pAddress[index];
	}

	//返回数组容量
	int getCapacity()
	{
		return this->m_Capacity;
	}

	//返回数组大小
	int getSize()
	{
		return this->m_Size;
	}

	~MyArray()
	{
		if (this->pAddress != NULL)
		{
			delete[] this->pAddress;
			this->pAddress = NULL;
		}
	}

private:

	T* pAddress; //指向堆区开辟的真实数组

	int m_Capacity;	//数组容量

	int m_Size;		//数组大小
};

~~~

test.cpp

~~~c++
#include<iostream>
#include<string>
#include"MyArray.hpp"
using namespace std;

void printIntArray(MyArray<int>& arr)
{
	for (int i = 0; i < arr.getSize(); i++)
	{
		cout << arr[i] << endl;
	}
}

void test01()
{
	MyArray<int>arr1(5);

	for (int i = 0; i < 5; i++)
	{
		arr1.Push_Back(i);
	}
	cout << "arr1 数组中元素为: " << endl;
	printIntArray(arr1);
	cout << "arr1 的容量为: " << arr1.getCapacity() << endl;
	cout << "arr1 的大小为: " << arr1.getSize() << endl;

	MyArray<int>arr2(arr1);
	cout << "arr2 数组中元素为: " << endl;
	printIntArray(arr2);

	arr2.Pop_Back();
	cout << "arr2 尾删后: " << endl;
	cout << "arr2 的容量为: " << arr2.getCapacity() << endl;
	cout << "arr2 的大小为: " << arr2.getSize() << endl;
}

//测试自定义类型
class Person
{
public:
	Person()
	{

	}
	Person(string name, int age)
	{
		this->m_Name = name;
		this->M_Age = age;
	}

	string m_Name;
	int M_Age;
};

void printPersonArray(MyArray<Person>& arr)
{
	for (int i = 0; i < arr.getSize(); i++)
	{
		cout << "姓名: " << arr[i].m_Name << " 年龄: " << arr[i].M_Age << endl;
	}
}

void test02()
{
	MyArray<Person>arr(10);

	Person p1("孙悟空", 999);
	Person p2("韩信", 20);
	Person p3("孙尚香", 20);
	Person p4("妲己", 9);
	Person p5("阿离", 19);

	//将数据插入到数组中
	arr.Push_Back(p1);
	arr.Push_Back(p2);
	arr.Push_Back(p3);
	arr.Push_Back(p4);
	arr.Push_Back(p5);

	//打印数组
	printPersonArray(arr);
	//输出数组容量
	cout << "数组容量: " << arr.getCapacity() << endl;
	//输出数组大小
	cout << "数组大小: " << arr.getSize() << endl;
}

int main()
{
	//test01();

	test02();

	system("pause");
}
~~~

## STL初识

**基本概念:**

- STL:标准模板库

- STL从广义上分为:**容器(container)算法(algorithm)迭代器(iterator)**
- **容器**和**算法**之间通过**迭代器**进行无缝连接
- STL几乎所有的代码都采用了模板类或者模板函数

**六大组件:**

- STL大体分为六大组件，分别是:容器、算法、迭代器、仿函数、适配器(配接器)、空间配置器



1. 容器:各种数据结构，如vector、list、deque、set、map等,用来存放数据。
2. 算法:各种常用的算法，如sort、find、copy、for_each等
3. 迭代器:扮演了容器与算法之间的胶合剂。
4. 仿函数:行为类似函数，可作为算法的某种策略。
5. 适配器:一种用来修饰容器或者仿函数或迭代器接口的东西。
6. 空间配置器:负责空间的配置与管理。

**STL中的容器,算法,迭代器**

**容器**:置物之所也
STL**容器**就是将**运用最广泛的一些数据结构****实现出来
常用的数据结构:数组,链表,树,栈,队列,集合,映射表等
这些容器分为**序列式容器**和**关联式容器**两种:

- **序列式容器**:强调值的排序，序列式容器中的每个元素均有固定的位置。
- **关联式容器**:二叉树结构，各元素之间没有严格的物理上的顺序关系



**算法**:问题之解法也

有限的步骤，解决逻辑或数学上的问题，这一门学科我们叫做算法(Algorithms)
算法分为:**质变算法**和**非质变算法**。
质变算法:是指运算过程中会更改区间内的元素的内容。例如拷贝，替换，删除等等
非质变算法:是指运算过程中不会更改区间内的元素内容，例如查找、计数、遍历、寻找极值等等



**迭代器**:容器和算法之间粘合剂
提供一种方法，使之能够依序寻访某个容器所含的各个元素，而又无需暴露该容器的内部表示方式。

每个容器都有自己专属的迭代器

迭代器使用非常类似于指针，初学阶段我们可以先理解迭代器为指针



| 种类           | 功能                                                     | 支持运算                                |
| -------------- | :------------------------------------------------------- | --------------------------------------- |
| 输入迭代器     | 对数据的只读访问                                         | 只读，支持++、==、! =                   |
| 输出迭代器     | 对数据的只写访问                                         | 只写，支持++                            |
| 前向迭代器     | 读写操作，并能向前推进迭代器                             | 读写，支持++、==、! =                   |
| 双向迭代器     | 读写操作，并能向前和向后操作                             | 读写，支持++、--，                      |
| 随机访问迭代器 | 读写操作，可以以跳跃的方式访问任意数据，功能最强的迭代器 | 读写，支持++、--、[n]、-n、<、<=、>、>= |

常用的容器中迭代器种类为双向迭代器，和随机访问迭代器

#### vector--存放内置数据类型

容器:		`vector`

算法:		`for_each`

迭代器:	`vector<int>::iterator`

~~~c++
#include<iostream>
#include<vector>
#include<algorithm>	//标准算法头文件
using namespace std;

void print(int val)
{
	cout << val << endl;
}

void test01()
{
	//创建vector容器,并且通过模板参数指定容器中存放的数据类型
	vector<int> v;
	//向容器中存放数据
	v.push_back(10);
	v.push_back(20);
	v.push_back(30);
	v.push_back(40);

	//每一个容器都有自己的迭代器，迭代器是用来遍历容器中的元素
	// v.begin()返回迭代器，这个迭代器指向容器中第—个数据
	// v.end()返回迭代器，这个迭代器指向容器元素的最后一个元素的下一个位置
	// vector<int>::iterator拿到vector<int>这种容器的迭代器类型

	vector<int>::iterator itBegin = v.begin(); 
	vector<int>::iterator itEnd = v.end();

	//第一种遍历方式
	/*while (itBegin != itEnd)
	{
		cout << *itBegin << endl;
		itBegin++;
	}*/

	//第二种遍历方式
	/*for (vector<int>::iterator it = v.begin(); it < v.end(); it++)
	{
		cout << *it << endl;
	}*/

	//第三种遍历方式	利用STL 提供的	for_each
	for_each(v.begin(), v.end(), print);

}

int main()
{
	test01();


	system("pause");
}
~~~

#### vector--存放自定义数据类型

~~~c++
#include<iostream>
#include<string>
#include<vector>
#include<algorithm>	//标准算法头文件
using namespace std;

class Person
{
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}

	string m_Name;
	int m_Age;
};


void test01()
{
	//创建vector容器,并且通过模板参数指定容器中存放的数据类型
	vector<Person> v;
	//向容器中存放数据

	Person p1("aaa", 10);
	Person p2("bbb", 20);
	Person p3("ccc", 30);
	Person p4("ddd", 40);
	Person p5("eee", 50);

	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);
	v.push_back(p4);
	v.push_back(p5);


	for (vector<Person>::iterator it = v.begin(); it < v.end(); it++)
	{
		//解出来的就是尖括号中的类型  没解引用之前相当于指针
		//cout << "姓名" << (*it).m_Name << " 年龄: " << (*it).m_Age << endl;
		cout << "姓名" << it->m_Name << " 年龄: " << it->m_Age <<endl;
	}


}

void test02()
{
	vector<Person*> v;
	//向容器中存放数据

	Person p1("aaa", 10);
	Person p2("bbb", 20);
	Person p3("ccc", 30);
	Person p4("ddd", 40);
	Person p5("eee", 50);

	v.push_back(&p1);
	v.push_back(&p2);
	v.push_back(&p3);
	v.push_back(&p4);
	v.push_back(&p5);

	for (vector<Person*>::iterator it = v.begin(); it < v.end(); it++)
	{
		
		cout << "姓名" << (*it)->m_Name << " 年龄: " << (*it)->m_Age << endl;
	}
}

int main()
{
	//test01();

	test02();

	system("pause");
}
~~~

#### vector- -容器嵌套容器

~~~c++
#include<iostream>
#include<vector>
using namespace std;

void test01()
{
	//创建vector容器,并且通过模板参数指定容器中存放的数据类型
	vector<vector<int>> v;

	//创建小容器
	vector<int> v1;
	vector<int> v2;
	vector<int> v3;
	vector<int> v4;
	vector<int> v5;
	
	//向小容器中插入数据
	for (int i = 0; i < 4; i++)
	{
		v1.push_back(i + 1);
		v2.push_back(i + 2);
		v3.push_back(i + 3);
		v4.push_back(i + 4);
		v5.push_back(i + 5);
	}

	//将小容器插入大容器
	v.push_back(v1);
	v.push_back(v2);
	v.push_back(v3);
	v.push_back(v4);
	v.push_back(v5);

	for (vector<vector<int>>::iterator it = v.begin(); it < v.end(); it++)
	{
		// (*it)--容器 vector<int>
		for(vector<int>::iterator vit = (*it).begin(); vit != (*it).end(); vit++)
			cout << *vit << " ";
		cout << endl;
	}

}



int main()
{
	test01();



	system("pause");
}
~~~

## STL常用容器

### string容器

#### 基本概念

**本质:**

- string是C++风格的字符串，而string本质上是一个类

**string和char*区别:**

- char*是一个指针
-  string是一个类，类内部封装了char *，管理这个字符串，是一个char *型的容器。

**特点:**
string类内部封装了很多成员方法
例如:查找find，拷贝copy，删除delete替换replace，插入insert
string管理char *所分配的内存，不用担心复制越界和取值越界等，由类内部进行负责


#### string构造函数

构造函数原型:

- `string();`											            	//创建一个空的字符串例如:  string str;

- `string( const char* s );`				            //使用字符串s初始化

- `string(const string& str);`				        //使用一个string对象初始化另一个string对象

- `string(int n, char c);`								//使用n个字符c初始化

  




