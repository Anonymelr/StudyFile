# JavaBasic



## 一、多态

### 1.1 重写和重载的区别

#### 1.1.1 重写

##### 1.1.1.1 定义

​	override 是重写（覆盖）了一个方法，以实现不同的功能。一般是用于**子类在继承父类**时，重写（重新实现）父类中的方法。

##### 1.1.1.2 规则

- 重写方法的**参数列表**必须**完全**与被重写的方法的**相同**,否则不能称其为重写而是重载. 

- 重写方法的**访问修饰符**一定要**大于**被重写方法的访问修饰符（public>protected>default>private）。 

- 重写的方法的**返回值**必须和被重写的方法的返回**一致**； 

- 重写的方法所抛出的**异常**必须和被重写方法的所抛出的异常**一致**，**或者是其子类**； 

- **被重写的方法不能为private**，否则在其子类中只是新定义了一个方法，并没s有对其进行重写。 

- **静态方法不能被重写为非静态的方法（会编译出错）**。

#### 1.1.2 重载

##### 1.1.2.1 定义

​	overload 是重载，一般是用于**在一个类内**实现若干重载的方法，这些方法的**名称相同而参数形式不同**。

##### 1.1.2.2 规则

- 在使用重载时只能通过**相同的方法名、不同的参数形式**实现。不同的参数类型可以是**不同的参数类型**，**不同的参数个数**，**不同的参数顺序**（**参数类型必须不一样**）； 

- 不能通过访问权限、返回类型、抛出的异常进行重载； 

- **方法的异常类型和数目不会对重载造成影响**；
- 继承是子类使用父类的方法，而多态则是父类使用子类的方法。

## 二、关键字

### 2.1  Static

#### 2.1.1 定义

​	在类中，使用 static 修饰符修饰的属性（成员变量）称为**静态变量**，常量称为**静态常量**，方法称为**静态方法**，它们统称为静态成员，归整个类所有。

#### 2.1.2 调用方式

​	静态成员不依赖于类的特定实例，被类的所有实例共享，就是说 static 修饰的方法或者变量不需要依赖于对象来进行访问，只要这个类被加载，Java虚拟机就可以根据类名找到它们。

```
调用静态成员的语法形式如下：  
	类名.静态成员
```

**注意：**

- static 修饰的成员变量和方法，从属于类。
- 普通变量和方法从属于对象。
- 静态方法不能调用非静态成员，编译会报错。

#### 2.1.3 静态变量

##### 2.1.3.1 静态变量和普通变量的区别

1）静态变量

- 运行时，Java 虚拟机只为静态变量分配**一次**内存，在加载类的过程中完成静态变量的内存分配。
- 在类的内部，可以在任何方法内直接访问静态变量。
- 在其他类中，可以通过类名访问该类中的静态变量。

2）实例变量

- 每创建一个实例，Java 虚拟机就会为实例变量分配一次内存。
- 在类的内部，可以在非静态方法中直接访问实例变量。
- 在本类的静态方法或其他类中则需要通过类的实例对象进行访问。

##### 2.1.3.2 静态变量的作用

- **静态变量可以被类的所有实例共享**，因此静态变量可以作为实例之间的共享数据，增加实例之间的交互性。

- 如果类的所有实例都包含一个相同的常量属性，则可以把这个属性定义为**静态常量类型**，从而**节省内存空间**。例如，在类中定义一个静态常量 PI。

  ```java
  public static double PI = 3.14159256;
  ```

#### 2.1.4 静态方法

##### 2.1.4.1 静态方法与实例方法的区别如下：

- 静态方法不需要通过它所属的类的任何实例就可以被调用，因此**在静态方法中不能使用 this 关键字**，**也不能直接访问所属类的实例变量和实例方法**，但是**可以直接访问所属类的静态变量和静态方法**。另外，和 this 关键字一样，super 关键字也与类的特定实例相关，所以在**静态方法中也不能使用 super 关键字**。
- **在实例方法中可以直接访问所属类的静态变量、静态方法、实例变量和实例方法**。

##### 2.1.4.2 注意

​	**在访问非静态方法时，需要通过实例对象来访问，而在访问静态方法时，可以直接访问，也可以通过类名来访问，还可以通过实例化对象来访问。**

#### 2.1.5 静态代码块

##### 2.1.5.1 定义

​	静态代码块指 Java 类中的 **static{ } 代码块**，主要用于**初始化类，为类的静态变量赋初始值，提升程序性能**。

##### 2.1.5.2 特点

- 静态代码块类似于一个方法，但它**不可以存在于任何方法体**中。
- 静态代码块可以置于类中的**任何地方**，类中可以有**多个**静态初始化块。 
- Java 虚拟机在**加载类时执行静态代码块**，所以很多时候会将一些**只需要进行一次的初始化操作都放在 static 代码块中进行**。
- 如果类中包含多个静态代码块，则 Java 虚拟机将按它们**在类中出现的顺序依次执行它们**，每个静态代码块**只会被执行一次**。
- 静态代码块与静态方法一样，**不能直接访问类的实例变量和实例方法**，而需要通过类的实例对象来访问。



### 2.2 Final

#### 2.2.1 注意

- final 用在**变量**的前面表示变量的值不可以改变，此时该变量可以被称为**常量**。
- final 用在**方法**的前面表示方法**不可以被重写**（子类中如果创建了一个与父类中相同名称、相同返回值类型、相同参数列表的方法，只是方法体中的实现不同，以实现不同于父类的功能，这种方式被称为方法重写，又称为方法覆盖。这里了解即可，教程后面我们会详细讲解）。
- final 用在**类**的前面表示**该类不能有子类**，即**该类不可以被继承**。

#### 2.2.2 final 修饰变量

final 修饰的变量即成为常量，只能赋值一次，但是 **final 所修饰局部变量和成员变量有所不同**。

- final 修饰的**局部变量**必须**使用之前被赋值一次才能使用**。

- final 修饰的**成员变量**在声明时没有赋值的叫“空白 final 变量”。空白 final 变量**必须在构造方法或静态代码块中初始化**。

```
注意：final 修饰的变量不能被赋值这种说法是错误的，严格的说法是，final 修饰的变量不可被改变，一旦获得了初始值，该 final 变量的值就不能被重新赋值。
```

##### 2.2.2.1 final 修饰基本类型变量和引用类型变量的区别

​	当使用 final 修饰**基本类型变量**时，**不能**对基本类型变量**重新赋值**，因此**基本类型变量不能被改变**。 但对于**引用类型变量**而言，它保存的仅仅是一个引用，final 只保证这个引用类型变量所**引用的地址不会改变**，即一直引用同一个对象，但这个对象完全**可以发生改变**。

#### 2.2.3 final修饰方法

​	final 修饰的方法**不可被重写**，如果出于某些原因，不希望子类重写父类的某个方法，则可以使用 final 修饰该方法。

​	final 修饰的方法只是不能被重写，**完全可以被重载**。

#### 2.2.4 final修饰类

​	final 修饰的类**不能被继承**。当子类继承父类时，将可以访问到父类内部数据，并可通过重写父类方法来改变父类方法的实现细节，这可能导致一些不安全的因素。为了保证某个类不可被继承，则可以使用 final 修饰这个类。



### 2.3 Abstract

#### 2.3.1 抽象方法

​	如果一个方法使用 abstract 来修饰，则说明该方法是抽象方法，抽象方法只有声明没有实现。

​	**特征：**

- 抽象方法**没有方法体**

- 抽象方法**必须存在于抽象类中**

- 子类重写父类时，必须**重写父类所有的抽象方法**

​	**注意：**

- abstract 关键字**只能用于普通方法**，**不能用于 static 方法或者构造方法**中。

- 在使用 abstract 关键字修饰抽象方法时**不能使用 private 修饰**，因为**抽象方法必须被子类重写**，而如果使用了 private 声明，则子类是无法重写的。

#### 2.3.2 抽象类

**抽象类的定义和使用规则如下：**

- 抽象类和抽象方法都要使用 abstract 关键字声明。

- 如果一个方法被声明为抽象的，那么这个类也必须声明为抽象的。而**一个抽象类中，可以有 0~n 个抽象方法，以及 0~n 个具体方法。**

- **抽象类不能实例化**，也就是**不能使用 new 关键字创建对象**。



### 2.4 this

#### 2.4.1 this属性名 和 this.方法名

​	当一个**类的属性（成员变量）名与访问该属性的方法参数名相同**时，则需要使**用 this 关键字来访问类中的属性**，以**区分类的属性和方法中的参数**

​	this 关键字最大的作用就是**让类中一个方法，访问该类里的另一个方法或实例变量**。

```java
/**
 * 第一种定义Dog类方法
 **/
public class Dog {
    // 定义一个jump()方法
    public void jump() {
        System.out.println("正在执行jump方法");
    }
    // 定义一个run()方法，run()方法需要借助jump()方法
    public void run() {
        //省略this访问类内方法
        jump();
        System.out.println("正在执行 run 方法");
    }
}
```

​	**省略 this 前缀只是一种假象**，虽然程序员省略了调用 jump() 方法之前的 this，但实际上这个 this 依然是存在的。



​	对于 **static 修饰的方法**而言，可以使用类来直接调用该方法，如果在 static 修饰的方法中使用 this 关键字，则这个关键字就无法指向合适的对象。所以，**static 修饰的方法中不能使用 this 引用**。并且 Java 语法规定，**静态成员不能直接访问非静态成员**。

#### 2.4.2 this() 访问构造方法

​	this( ) 用来访问本类的构造方法，括号中可以有参数，如果**有参数就是调用指定的有参构造方法**。

```java
public class Student {
    String name;
    // 无参构造方法（没有参数的构造方法）
    public Student() {
        //调用了 有参构造
        this("张三");
    }
    // 有参构造方法
    public Student(String name) {
        this.name = name;
    }
    // 输出name和age
    public void print() {
        System.out.println("姓名：" + name);
    }
    public static void main(String[] args) {
        Student stu = new Student();
        stu.print();
    }
}
```

​	**注意：**

- this( ) **不能在普通方法中使用，只能写在构造方法中**。
- 在构造方法中使用时，**必须是第一条语句**。



### 2.5 super

#### 2.5.1 super 关键字的功能：

- 在子类的构造方法中**显式的调用父类构造方法**
- **访问父类的成员方法和变量**。

#### 2.5.2 super 和 this 区别：

**super 关键字的用法：**

- super.父类属性名：调用父类中的属性
- super.父类方法名：调用父类中的方法
- super()：调用父类的无参构造方法
- super(参数)：调用父类的有参构造方法


**如果构造方法的第一行代码不是 this() 和 super()，则系统会默认添加 super()。**


**this 关键字的用法：**

- this.属性名：表示当前对象的属性
- this.方法名(参数)：表示调用当前对象的方法

**当局部变量和成员变量发生冲突时，使用`this.`进行区分。**

#### 2.5.3 总结

关于 super 和 this 关键字的异同，可简单总结为以下几条。

- 子类和父类中变量或方法名称相同时，用 super 关键字来访问。可以理解为 **super 是指向自己父类对象的一个指针**。在子类中调用父类的构造方法。

- this 是自身的一个对象，代表对象本身，可以理解为 **this 是指向对象本身的一个指针**。在同一个类中调用其它方法。

- this 和 super **不能同时出现在一个构造方法里面**，因为 this 必然会调用其它的构造方法，其它的构造方法中肯定会有 super 语句的存在，所以在同一个构造方法里面有相同的语句，就失去了语句的意义，编译器也不会通过。

- this( ) 和 super( ) 都指的是对象，所以，**均不可以在 static 环境中使用，包括 static 变量、static 方法和 static 语句块**。

- 从本质上讲，**this 是一个指向对象本身的指针**, 然而 **super 是一个 Java 关键字**。



### 2.6 instanceof

#### 2.6.1 定义

严格来说 instanceof 是 Java 中的一个**双目运算符**，由于它是由字母组成的，所以也是 Java 的保留关键字。在 Java 中可以使用 **instanceof 关键字判断一个对象是否为一个类（或接口、抽象类、父类）的实例**，语法格式如下所示。

```java
boolean result = obj instanceof Class
```

#### 2.6.2 用法

- 声明一个 class 类的对象，判断 obj 是否为 class 类的实例对象（很普遍的一种用法）

  ```java
  Integer integer = new Integer(1);
  System.out.println(integer instanceof  Integer);    // true
  ```

- 声明一个 class 接口实现类的对象 obj，判断 obj 是否为 class 接口实现类的实例对象

  ```java
  public class ArrayList<E> extends AbstractList<E>
          implements List<E>, RandomAccess, Cloneable, java.io.Serializable
  //用 instanceof 运算符判断 ArrayList 类的对象是否属于 List 接口的实例，如果是返回 true，否则返回 false。
  ArrayList arrayList = new ArrayList();
  System.out.println(arrayList instanceof List);    // true
  ```

- obj 是 class 类的直接或间接子类

  ```java
  public class Person {
  }
  public class Man extends Person {
  }
  
  Person p1 = new Person();
  Person p2 = new Man();
  Man m1 = new Man();
  System.out.println(p1 instanceof Man);    // false
  System.out.println(p2 instanceof Man);    // true
  System.out.println(m1 instanceof Man);    // true
  ```

#### 2.6.3 注意

- obj 必须为引用类型，不能是基本类型

  ```java
  int i = 0;
  System.out.println(i instanceof Integer);    // 编译不通过
  System.out.println(i instanceof Object);    // 编译不通过
  ```

- 当 obj 为 null 时，直接返回 false，因为 null 没有引用任何对象

  ```java
  System.out.println(null instanceof Object);    // false
  ```

  **obj 的类型必须是引用类型或空类型，否则会编译错误。**

- 当 class 为 null 时，会发生编译错误

  ```java
  Integer i = 0;
  System.out.println(i instanceof null);
  ```

   **class 只能是类或者接口**



## 三、常用类和常用方法

### 3.1 == 和 equal() 的区别

- ==：它的作用是判断两个对象的地址是不是相等。即: 判断两个对象是不是同一个对象。(**基本数据类型比较的是值，引用数据类型＝＝比较的是内存地址**)。

- equals() : 它的作用也是判断两个对象是否相等。但它一般有**两种使用情况**，如下：

  - **类没有覆盖equals() 方法**。则通过equals() 比较该类的两个对象时，**等价于通过＝＝比较这两个对象**。

  - **类覆盖了equals() 方法**。一般，我们都**覆盖equals() 方法来两个对象的内容相等**；若它们的内容相等，则返回true (即，认为这两个对象相等)。

### 3.2 String类及常用方法

- 获取字符串长度

  ```java
  public int length()//返回该字符串的长度
  ```

- 获取字符串某一位置字符

  ```
  public char charAt(int index)//返回字符串中指定位置的字符；注意字符串中第一个字符索引是0，最后一个是length()-1。
  ```

- 获取字符串的子串

  ```java
  public String substring(int beginIndex)//该方法从beginIndex位置起，从当前字符串中取出剩余的字符作为一个新的字符串返回。
  public String substring(int beginIndex, int endIndex)//该方法从beginIndex位置起，从当前字符串中取出到endIndex-1位置的字符作为一个新的字符串返回。
  ```

- 字符串比较

  ```java
  public boolean equals(Object anotherObject)//比较当前字符串和参数字符串，在两个字符串相等的时候返回true，否则返回false。
  public boolean equalsIgnoreCase(String anotherString)//与equals方法相似，但忽略大小写
  ```

- 字符串连接

  ```java
  public String concat(String str)//将参数中的字符串str连接到当前字符串的后面，效果等价于"+"
  ```

- 字符串中单个字符查找

  ```java
  public int indexOf(int ch/String str)//用于查找当前字符串中字符或子串，返回字符或子串在当前字符串中从左边起首次出现的位置，若没有出现则返回-1。
  public int indexOf(int ch/String str, int fromIndex)//改方法与第一种类似，区别在于该方法从fromIndex位置向后查找。
  
  public int lastIndexOf(int ch/String str)//该方法与第一种类似，区别在于该方法从字符串的末尾位置向前查找。
  public int lastIndexOf(int ch/String str, int fromIndex)//该方法与第二种方法类似，区别于该方法从fromIndex位置向前查找。
  ```

- 字符串中字符的大小写转换

  ```java
  public String toLowerCase()//返回将当前字符串中所有字符转换成小写后的新串
  public String toUpperCase()//返回将当前字符串中所有字符转换成大写后的新串
  ```

- 字符串中字符的替换

  ```java
  public String replace(char oldChar, char newChar)//用字符newChar替换当前字符串中所有的oldChar字符，并返回一个新的字符串。
  
  public String replaceFirst(String regex, String replacement)//该方法用字符replacement的内容替换当前字符串中遇到的第一个和字符串regex相匹配的子串，应将新的字符串返回。
  public String replaceAll(String regex, String replacement)//该方法用字符replacement的内容替换当前字符串中遇到的所有和字符串regex相匹配的子串，应将新的字符串返回。
  ```

- 截取字符串两端的空格

  ```java
  String trim()//截去字符串两端的空格，但对于中间的空格不处理。
  ```

- 判断起始字符串prefix或者终止字符串suffix是否和当前字符串相同

  ```java
  boolean statWith(String prefix)或boolean endWith(String suffix)//用来比较当前字符串的起始字符或子字符串prefix和终止字符或子字符串suffix是否和当前字符串相同，重载方法中同时还可以指定比较的开始位置offset。
  ```

- 判断字符串中是否包含str

  ```java
  contains(String str)//判断参数s是否被包含在字符串中，并返回一个布尔类型的值。
  ```

- 分割字符串

  ```java
  String[] split(String str)//将str作为分隔符进行字符串分解，分解后的字字符串在字符串数组中返回。
  ```

- 字符串与基本类型的转换

  ```java
  字符串转换为基本类型
  public static byte parseByte(String s)
  public static short parseShort(String s)
  public static short parseInt(String s)
  public static long parseLong(String s)
  public static float parseFloat(String s)
  public static double parseDouble(String s)
      
  基本类型转换为字符串类型。
  static String valueOf(char data[])
  static String valueOf(char data[], int offset, int count)
  static String valueOf(boolean b)
  static String valueOf(char c)
  static String valueOf(int i)
  static String valueOf(long l)
  static String valueOf(float f)
  static String valueOf(double d)
  ```

  

### 3.3 String、StringBuffer、StringBuilder三者的异同

#### 3.3.1 异同之处

- 字符串：字符串是**常量**；它们的值在**创建之后不能更改，存储在堆中**。
       **如果字符串多次赋值，其实是每次重新赋值的时候程序都先在内存中寻找已开辟的空间是否存在该值;如果找不到，再开辟新的空间存储该对象**

- StringBuffer：可变的字符序列 与 StringBuilder 中的方法和功能完全是等价的。

  ​	只是**StringBuffer** 中的方法大都采用了 synchronized 关键字进行修饰，因此是**线程安全**的，而 **StringBuilder** 没有这个修饰，可以被认为是**线程不安全**的。

  ​	在**单线程程序**下，**StringBuilder效率更快**，因为它不需要加锁，不具备多线程安全而StringBuffer则每次都需要判断锁，效率相对更低。

#### 3.3.2 StringBuffer 常用方法

##### 3.3.2.1 构造方法：

- StringBuffer() //构造一个其中不带字符的字符串缓冲区，初始容量为 16 个字符。
- StringBuffer(int capacity)//构造一个不带字符，但具有指定初始容量的字符串缓冲区。

- StringBuffer(String str) //构造一个字符串缓冲区，并将其内容初始化为指定的字符串内容。

##### 3.3.2.2成员方法：

- **添加功能**
  　　 
  ```java
public StringBuffer append(anyType varName); //在缓冲区的末尾追加
  　　 public StringBuffer insert(int index,String str); //在指定索引位置添加
  ```
  
- **删除功能**
  　　 
  ```java
  public StringBuffer delete(int start,int end); //从start开始删除到end结束，不包括end位置的字符
public StringBuffer delete(0,sb.length); //清空缓冲区
  　　 public StringBuffer deleteCharAt(int index); //删除第index位置的字符
  ```
  
- **替换功能**
  　　 
  ```java
public StringBuffer replace(int start,int end, String str);//替换字符串
  　　 public void setCharAt(int index ,char); //修改,把指定索引位置的值改成传入的char值
  ```
  
- **截取功能**
  　　 
```java
  　　 public String substring(int start); //从start位置开始截取字符串
```

- **反转功能**
  　　
```java
  　　public StringBuffer reverse(); //反转字符串的所有字符
```

- **其他常用的功能**
  　　
  ```java
  public void setLength(int len); //根据传入的len值截取缓冲区的长度
  public String toString() //转换成String
  public int indexOf(str); //查找str在缓冲区第一次出现的位置
  public int lastIndexOf(str); //从后向前查找查找str在缓冲区第一次出现的位置
  ```



### 3.4 Date类

#### 3.4.1 定义

​	Date 类表示系统特定的时间戳，可以精确到毫秒。Date 对象表示时间的默认顺序是**星期、月、日、小时、分、秒、年**。

​	Date 类有如下**两个构造方法**。

- Date()：此种形式表示分配 Date 对象并初始化此对象，以表示分配它的时间（精确到毫秒），使用该构造方法创建的对象可以**获取本地的当前时间**。

- Date(long date)：此种形式表示**从 GMT 时间（格林尼治时间）1970 年 1 月 1 日 0 时 0 分 0 秒开始经过参数 date 指定的毫秒数**。

  ```java
  Date date1 = new Date();    // 调用无参数构造函数
  System.out.println(date1.toString());    // 输出：Wed Nov 18 15:34:40 CST 2020
  Date date2 = new Date(60000);    // 调用含有一个long类型参数的构造函数
  System.out.println(date2);    // 输出：Thu Jan 01 08:01:00 CST 1970
  ```

#### 3.4.2 常用方法

| 方法                            | 描述                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| boolean after(Date when)        | 判断此日期是否在指定日期之后                                 |
| boolean before(Date when)       | 判断此日期是否在指定日期之前                                 |
| int compareTo(Date anotherDate) | 比较两个日期的顺序                                           |
| boolean equals(Object obj)      | 比较两个日期的相等性                                         |
| long getTime()                  | 返回自 1970 年 1 月 1 日 00:00:00 GMT 以来，此 Date 对象表示的毫秒数 |
| String toString()               | 把此 Date 对象转换为以下形式的 String: dow mon dd hh:mm:ss zzz yyyy。 其中 dow 是一周中的某一天(Sun、Mon、Tue、Wed、Thu、Fri 及 Sat) |



### 3.5 SimpleDateFormat类

#### 3.5.1 定义

​	**SimpleDateFormat 是一个以与语言环境有关的方式来格式化和解析日期的具体类，它允许进行格式化（日期→文本）、解析（文本→日期）和规范化**。SimpleDateFormat 使得可以选择任何用户定义的日期/时间格式的模式。

SimpleDateFormat 类主要有如下 **3 种构造方法**。

- SimpleDateFormat()：用**默认的格式和默认的语言环境**构造 SimpleDateFormat。
- SimpleDateFormat(String pattern)：用**指定的格式和默认的语言环境**构造 SimpleDateFormat。
- SimpleDateFormat(String pattern,Locale locale)：用**指定的格式和指定的语言环境**构造 SimpleDateFormat。

#### 3.5.2 自定义格式中常用的字母及含义

| 字母 | 含义                                                         | 示例                                                         |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| y    | 年份。一般用 yy 表示两位年份，yyyy 表示 4 位年份             | 使用 yy 表示的年扮，如 11； 使用 yyyy 表示的年份，如 2011    |
| M    | 月份。一般用 MM 表示月份，如果使用 MMM，则会 根据语言环境显示不同语言的月份 | 使用 MM 表示的月份，如 05； 使用 MMM 表示月份，在 Locale.CHINA 语言环境下，如“十月”；在 Locale.US 语言环境下，如 Oct |
| d    | 月份中的天数。一般用 dd 表示天数                             | 使用 dd 表示的天数，如 10                                    |
| D    | 年份中的天数。表示当天是当年的第几天， 用 D 表示             | 使用 D 表示的年份中的天数，如 295                            |
| E    | 星期几。用 E 表示，会根据语言环境的不同， 显示不 同语言的星期几 | 使用 E 表示星期几，在 Locale.CHINA 语 言环境下，如“星期四”；在 Locale.US 语 言环境下，如 Thu |
| H    | 一天中的小时数（0~23)。一般用 HH 表示小时数                  | 使用 HH 表示的小时数，如 18                                  |
| h    | 一天中的小时数（1~12)。一般使用 hh 表示小时数                | 使用 hh 表示的小时数，如 10 (注意 10 有 可能是 10 点，也可能是 22 点） |
| m    | 分钟数。一般使用 mm 表示分钟数                               | 使用 mm 表示的分钟数，如 29                                  |
| s    | 秒数。一般使用 ss 表示秒数                                   | 使用 ss 表示的秒数，如 38                                    |
| S    | 毫秒数。一般使用 SSS 表示毫秒数                              | 使用 SSS 表示的毫秒数，如 156                                |

```java
import java.text.SimpleDateFormat;
import java.util.Date;
public class Test13 {
    public static void main(String[] args) {
        Date now = new Date(); // 创建一个Date对象，获取当前时间
        // 指定格式化格式
        SimpleDateFormat f = new SimpleDateFormat("今天是 " + "yyyy 年 MM 月 dd 日 E HH 点 mm 分 ss 秒");
        System.out.println(f.format(now)); // 将当前时间袼式化为指定的格式
    }
}
//结果
今天是 2018 年 10 月 15 日 星期一 09 点 26 分 23 秒
```



## 四、异常处理

### 4.1 try catch finally

#### 4.1.1 注意

- 异常处理语法结构中**只有 try 块是必需**的，也就是说，如果没有 try 块，则不能有后面的 catch 块和 finally 块；

- **catch 块和 finally 块都是可选的**，但 catch 块和 finally 块至少出现其中之一，也可以同时出现；

- **可以有多个 catch 块**，**捕获父类异常的 catch 块必须位于捕获子类异常的后面**；

- **不能只有 try 块**，既没有 catch 块，也没有 finally 块；

- **多个 catch 块必须位于 try 块之后，finally 块必须位于所有的 catch 块之后**。

- **finally 与 try 语句块匹配的语法格式**，此种情况会导致异常丢失，所以**不常见**。

#### 4.1.2 执行情况

- 如果 **try 代码块中没有拋出异常**，则**执行完 try 代码块之后直接执行 finally 代码块**，然后**执行 try catch finally 语句块之后的语句**。

- 如果 **try 代码块中拋出异常，并被 catch 子句捕捉**，那么**在拋出异常的地方终止 try 代码块的执行**，转而**执行相匹配的 catch 代码块**，之后**执行 finally 代码块**。如果 **finally 代码块中没有拋出异常**，则**继续执行 try catch finally 语句块之后的语句**；如果 **finally 代码块中拋出异常**，则**把该异常传递给该方法的调用者**。

- 如果 **try 代码块中拋出的异常没有被任何 catch 子句捕捉到**，那么将**直接执行 finally 代码块中的语句**，并**把该异常传递给该方法的调用者**。



### 4.2 throw 和 throws 关键字

#### 4.2.1 throws 声明异常

​	当一个**方法产生**一个它**不处理的异常**时，那么就**需要在该方法的头部声明这个异常**，以便**将该异常传递到方法的外部进行处理**。使用 throws 声明的方法表示此方法不处理异常。throws 具体格式如下

```java
returnType method_name(paramList) throws Exception 1,Exception2,…{…}
```

​	**如果有多个异常类，它们之间用逗号分隔**。这些异常类可以是方法中调用了可能拋出异常的方法而产生的异常，也可以是方法体中生成并拋出的异常。

​	**子类方法声明抛出的异常类型应该是父类方法声明抛出的异常类型的子类或相同，子类方法声明抛出的异常不允许比父类方法声明抛出的异常多**

#### 4.2.2 throw 抛出异常

​	**throw 语句用来直接拋出一个异常，后接一个可拋出的异常类对象**，其语法格式如下：

```java
throw ExceptionObject;
```

​	其中，**ExceptionObject 必须是 Throwable 类或其子类的对象**。如果是**自定义异常类，也必须是 Throwable 的直接或间接子类**。例如，以下语句在编译时将会产生语法错误：

```java
throw new String("拋出异常");    // String类不是Throwable类的子类
```

#### 4.2.3 throws 和 throw 的区别如下：

- **throws 用来声明一个方法可能抛出的所有异常信息，表示出现异常的一种可能性，但并不一定会发生这些异常**；**throw 则是指拋出的一个具体的异常类型，执行 throw 则一定抛出了某种异常对象。**
- 通常在一个方法（类）的声明处通过 throws 声明方法（类）可能拋出的异常信息，而在方法（类）内部通过 throw 声明一个具体的异常信息。
- throws 通常**不用显示地捕获异常，可由系统自动将所有捕获的异常信息抛给上级方法**； throw 则**需要用户自己捕获相关的异常，而后再对其进行相关包装，最后将包装后的异常信息抛出**。



## 五、多线程

### 5.1 Synchronized 和 Lock 的区别

- Synchronized是关键字，内置语言实现，Lock是接口。

- Synchronized在线程发生异常时会自动释放锁，因此不会发生异常死锁。Lock异常时不会自动释放锁，所以需要在finally中实现释放锁。

- Lock是可以中断锁，Synchronized是非中断锁，必须等待线程执行完成释放锁。

- Lock可以使用读锁提高多线程读效率。



## 六、集合

![img](https://img-blog.csdnimg.cn/20190310181825411.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2Rpd2Vpa2FuZw==,size_16,color_FFFFFF,t_70)

### 6.1 ArrayList和LinkedList区别

- ArrayList是实现了基于**动态数组**的数据结构，LinkedList基于**链表**的数据结构。

- 对于**随机访问get和set**，ArrayList觉得优于LinkedList，因为LinkedList要移动指针。

- 对于**新增和删除操作add和remove**，LinedList比较占优势，因为ArrayList要移动数据。

- 对ArrayList和LinkedList而言，在列表末尾增加一个元素所花的开销都是固定的。对ArrayList而言，主要是在内部数组中增加一项，指向所添加的元素，偶尔可能会导致对数组重新进行分配；而对LinkedList而言，这个开销是统一的，分配一个内部Entry对象。

- 在ArrayList的中间插入或删除一个元素意味着这个列表中剩余的元素都会被移动；而在LinkedList的中间插入或删除一个元素的开销是固定的。

- **LinkedList不支持高效的随机元素访问**。

- ArrayList的空间浪费主要体现在**在list列表的结尾预留一定的容量空间**，而LinkedList的空间花费则体现在**它的每一个元素都需要消耗相当的空间**



### 6.2 栈和队列

#### 6.2.1 栈

栈的实现，有两个方法：一个是用java本身的集合类型Stack类型；另一个是借用LinkedList来间接实现Stack。

| 序号 |            方法             |                       含义                       |
| :--: | :-------------------------: | :----------------------------------------------: |
|  1   |       boolean empty()       |                测试堆栈是否为空。                |
|  2   |       Object peek( )        |     查看堆栈顶部的对象，但不从堆栈中移除它。     |
|  3   |        Object pop( )        | 移除堆栈顶部的对象，并作为此函数的值返回该对象。 |
|  4   | Object push(Object element) |                把项压入堆栈顶部。                |
|  5   | int search(Object element)  |      返回对象在堆栈中的位置，以 1 为基数。       |

#### 6.2.2 队列

Queue是java中实现队列的接口，它总共只有6个方法，我们一般只用其中3个就可以了。Queue的实现类有LinkedList和PriorityQueue。最常用的实现类是LinkedList。

| 序号 |        方法        |                           含义                           |
| :--: | :----------------: | :------------------------------------------------------: |
|  1   |  boolean add(E e)  |   压入元素(添加)，在超出容量时，add()方法会对抛出异常    |
|  2   | boolean offer(E e) |      压入元素(添加)，在超出容量时，offer()返回false      |
|  3   |     E remove()     |   弹出元素(删除)，在容量为0的时候，remove()会抛出异常    |
|  4   |      E poll()      |     弹出元素(删除)，在容量为0的时候，poll()返回false     |
|  5   |    E element()     | 获取队头元素(不删除)，容量为0的时候，element()会抛出异常 |
|  6   |      E peek()      |   获取队头元素(不删除)，容量为0的时候，peek()返回null    |

|          | 抛出异常  | 返回特殊值 |
| -------- | --------- | ---------- |
| **插入** | add(e)    | offer(e)   |
| **删除** | remove()  | poll()     |
| **检查** | element() | peek()     |