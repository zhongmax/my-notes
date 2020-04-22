# Java核心技术笔记

## 第三章 Java基础

### 3.1 String的常用方法

```java
// 返回与字符串 str 匹配的第一个子串的开始位置，这个位置从索引 0 或 fromIndex 开始计算，如果在原始串中不存在 str，返回 - 1
// 示例: str.indexOf("ll");
int indexOf(String str);
int indexOf(String str, int fromIndex);

// 返回字符串长度
int length();

// 返回一个新字符串，这个字符串用 new String 代替原始字符串中所有的 oldString。可以使用 String 或 StringBuilder 对象作为 CharSequence 参数
// 示例: str.replace('a', 'b');
String replace(CharSequence oldString, CharSequence newString);

// 返回一个新字符创。这个字符串包含原始字符串中从 beginIndex 到串尾或 endIndex - 1的所有代码单元
// 示例: String s = str.substring(1, 3);
String substring(int beginIndex);
String substring(int beginIndex, int endIndex);

// 返回一个新的字符串，将原始字符串字母改为大写或者小写
// 示例: String s = str.toLowerCase();
//			String s = str.toUpperCase();
String toLowerCase();
String toUpperCase();

// 返回一个新的字符串，将头部与末尾空格删除
// 示例: String s = str.trim();
String trim();

// 返回一个新的字符串，用给定的定界符链接所有元素
// 示例: String s = String.join("-", arrStr);
String join(CharSequence delimiter, CharSequence ... elements);
```

### 3.2 StringBuilder常用方法

```java
// 构造方法
StringBuiilder();

// 追加一个字符串并返回 this
StringBuilder append(String str);

// 在 offset 位置插入一个字符串并返回 this
StringBuilder insert(int offset, String str);

// 删除偏移量从 startIndex 到 endIndex-1 的代码单元并返回 this
StringBuilder delete(int startIndex, int endIndex);

// 返回一个与构建器或缓冲器内容相同的字符串
String toString();
```

### 3.2 大数值

```java
// 返回这个大实数与另一个大实数 other 的和、差、积、商。
BigDecimal add(BigDecimal other);
BigDecimal subtract(BigDecimal other);
BigDecimal multiply(BigDecimal other);
// 想要计算商，必须给出舍入方式 RoundingMode.HALF_UP 0~4 舍去， 5~9进位
BigDecimal divide(BigDecimal other RoundingMode mode);

// 其中 BigInteger 方法与 BigDecimal 类似
// 返回值等于 x 的大整数
static BigInteger valueOf(long x);
```

### 3.4 数组

```java
// 如果希望将一个数组的所有值拷贝到一个新的数组中
int[] copiedLuckyNumbers = Arrays.copyOf(luckyNumbers, luckyNumbers.length);
// 第二个参数是新数组的长度，通常使用这个方法增加数组的大小
luckyNumbers = Arrays.copyOf(luckyNumbers, 2 * luckyNumbers.length);

// 数组排序 采用优化的快速排序算法对数组进行排序
Arrays.sort(type[] a);

// 采用二分搜索算法查找值 v。如果查找成功，则返回对应下标，否则返回一个负数
// a 类型为 int、long、short、char、byte、boolean、float、double 的有序数组
// v 同 a 的数据元素类型相同的值
Arrays.binarySearch(type[] a, type v);

// 将数组的所有数据元素值设置为 v
Arrays.fill(type[] a, type v);

// 比较两个数组大小、下标相同的元素是否相等
Arrays.equals(type[] a, type[] b)
```

## 第四章 对象与类

### 4.1 类之间的关系

**依赖**（dependence）即 uses-a 关系，例如，Order 类使用 Account 类是因为 Order 对象需要访问 Account 对象查看信用状态。应该尽可能将相互依赖的类减至最少，这样 B 的改变不会导致 A 产生任何 bug，用软件工程的术语来说，就是让类之间的耦合度最小。

**聚合**（aggregation）即 has-a 关系，例如，一个 Order 对象包含一些 Item 对象。聚合关系意味着类 A 的对象包含类 B 的对象。

**继承**（inheritance）即 is-a 关系，是一种用于表示特殊与一般关系的。例如，RushOrder 类由 Order 类继承而来，RushOrder 类中包含了 Order 类中的信息和自己添加的属性和方法。

### 4.2 对象与对象变量

在 Java 中，使用**构造器**（constructor）构造新实例。构造器是一种特殊方法，用来构造并初始化对象。构造器的名字应该与类名相同。

使用构造函数构造出来的对象变量没有包含一个对象，只是引用了一个对象。

在 Java 中，任何对象变量的值都是存储在另外一个地方的一个对象的引用。new 操作符的返回值也是一个引用。

声明一个对象变量，需要调用 new 或将它们设置为 null 进行初始化

### 4.3 LocalDate常用方法

```java
// 构造一个表示当前日期的对象
static LocalTime now();

// 构造一个表示给定日期的对象
static LocalTime of(int year, int month, int day);

// 获取当前日期的年、月、日
int getYear();
int getMonthValue();
int getDayOfMonth();

// 获取当前日期是星期几 1: 星期一 7：星期日
DayOfWeek getDayOfWeek;

// 生成当前日期之后或之前 n 天的日期
LocalDate plusDays(int n);
LocalDate minusDays(int n);
```

### 4.4 静态域与静态方法

```java
// 经常使用 静态常量
public static final Integer N = 22;
```

静态方法指可通过类名调用这个方法，例：

```java
public static String getXXX() {
  return XXX;
}
// 调用
类名.getXXX();
```

在下面两种情况使用静态方法

- 一个方法不需要访问对象状态，所需参数都是显式参数提供 例如 Math.pow()
- 一个方法只需要访问类的静态域 例：类名.getXXX()

### 4.5 方法参数

Java 采用了按值调用，方法得到的所有参数值都是一个拷贝的值，方法不能修改传递它的任何参数变量的内容。

当对象引用作为参数时，就可以利用对象来修改值，具体执行过程为：

1. 方法获得对象的拷贝对象，这是一个对象的引用，并没有真正重新复制一份对象
2. 在方法中使用这个对象的方法，来更改对象的属性，此时方法中拷贝的对象修改了原始对象的属性。
3. 方法结束后，方法中对象不再使用，但是原始对象中的属性已经被更改了。

总结，Java 中方法参数的使用情况：

- 一个方法不能修改一个基本数据类型的参数（即数值型或布尔型）
- 一个方法可以改变一个对象参数的状态
- 一个方法不能让对象参数引用一个新的对象

### 4.6 对象构造

#### 4.6.1 重载

**重载**（overloading）是指一个类有多个方法，每个方法名字相同、参数不同，在使用该方法的时候，编译器会根据当前方法调用的参数类型与各个方法给出的参数类型比较，挑选出相应的方法。如果没有找到匹配的参数，就会产生编译错误，这个过程叫重载解析（overloading resolution）

通常只有构造器会使用重载，但是 Java 也允许重载任何方法，重载的方法只匹配方法名与参数类型，与返回值无关，如果有两个方法名一样，参数个数与类型位置相同，但是返回值不同的方法，

这是编译器会报错。

#### 4.6.2 默认域初始化

如果构造器没有显式给域赋初值，则会被自动赋为默认值：数值为0、布尔值为false、对象引用为null

#### 4.6.3 无参构造器

当一个对象由无参构造器创建时，对象中的属性会设置为无参构造器中默认的值，如果类中没有编写构造器，系统就会提供一个无参构造器，构造对象时这个构造器将所有实例域设置为默认值。

如果类中提供了至少一个构造器，但是没有无参构造器，使用无参构造器构造对象则视为不合法

#### 4.6.4 调用另外的构造器

关键字 this 是引用方法的隐式参数，这个关键字在构造器第一个语句使用，则是调用同一个类下的另一个构造器，例：

```java
public Employee(double s) {
  this("Employee #" + nextId, s);
  nextId++;
}
```

当调用 new Employee(600)时，Employee(double) 构造器将调用 Employee(String, double) 构造器。使用这种方式，对于公共的构造器代码只需编写一次。

#### 4.6.5 类设计技巧

1. 一定要保证数据私有

2. 一定要对数据初始化

3. 不要在类中使用过多的基本类型 （有点不太认同）

4. 不是所有的域都需要独立的域访问器和域更改器

5. 将职责过多的类进行分解

6. 类名和方法名要能够体现它们的职责

   类名：采用一个名词(Order)、前面有形容词修饰的名词(RushOrder)或动词(有 "-ing" 后缀)修饰名词(例如: BillingAddress)。

   方法：访问器 get 开头 更改器 set 开头

7. 优先使用不可变的类

## 第五章 继承

### 5.1 超类与子类

**子类**比超类拥有的功能更加丰富，因为子类可以从超类中继承这些类的方法和域，也可以添加属于自己的方法与域。

在设计超类与子类的时候，将通过的方法放在超类中，将有特殊用途的方法放在子类中。

当在子类中想修改超类提供的方法时，不能直接修改这个方法，需要提供一个新的方法来**覆盖**（override）超类中的这个方法。

```java
@Override
public double getSalary() {
  double baseSalary = super.getSalary();
  return baseSalary + bonus;
}
```

需要通过 super 这个关键字获取 getSalary这个方法来获取 salary 的值

在子类构造器中，如果需要访问超类的私有域，则需要通过 super 实现对超类构造器的调用，super 调用构造器的语句必须是子类构造器的第一条语句

this的两个用途：一是引用隐式参数，二是调用该类其他的构造器。

super也有两个用途：一是调用超类的方法，二是调用超类的构造器。



下面为代码：

```java
public static void main(String[] args) {
    Manager boss = new Manager("Carl Cracker", 80000, 1987, 12, 15);
    boss.setBonus(5000);

    Employee[] staff = new Employee[3];

    staff[0] = boss;
    staff[1] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
    staff[2] = new Employee("Tony Tester", 40000, 1990, 3, 15);

    for (Employee e : staff) {
        System.out.println(e.getName() + " " + e.getSalary());
    }
}
```

其实 e.getSalary() 虽然 e 是 Employee 类型，但是 e 既可以引用 Employee 类型的对象，也可以引用 Manager 类型的对象，当 e 引用 Manager 对象时， e.getSalary() 调用的是 Manager 类中的 get Salay 方法。

一堆对象变量（例如，变量 e ）可以指示多种实际类型的现象被称为**多态**（ploymorphism）。

在运行时能够自动地选择调用哪个方法的现象称为**动态绑定**（dynamic binding）。

在 Java 中，对象变量是多态的，一个 Employee 变量既可以引用一个 Emloyee 类对象，也可以引用一个 Employee 类的任何一个子类的对象（例如：Manager、Secretary）

**注意**：在 Java 中，子类数组的引用可以转换为超类数组的引用，例：

```java
Manager[] managers = new Manager[10];
// 转换为 Employee[] 数组
Employee[] staff = managers;
// 此时，staff[0] 与 managers[0] 引用的是同一个对象
staff[0] = new Employee("xxx",, ...);
// 我们将一个职员放到了管理类中
// 当调用 managers[0].setBonus(1000) 时，将导致调用一个不存在的实例域，从而搅乱相邻存储空间的内容
```

为了避免这类错误，所有数组都要牢记创建它们的元素类型，并负责监督仅将类型兼容的引用存储在数组中。

### 5.2 理解方法调用

弄清楚如何在对象上进行方法调用是非常重要的，假设要调用 x.f(args)，隐式参数 x 声明为类 C 的一个对象。调用过程的详细描述为：

1）编译器查看对象的声明类型和方法名，假设调用 x.f(param)，且隐式参数 x 声明为 c 类对象。可能会遇到有多个名字为 f ，但是参数类型不一样的方法，例如，可能存在 f(int) 和 f(String)。编译器会列举 C类中名为 f 的方法和其超类中访问属性为 public 且名为 f 的方法（超类私有方法不可访问），至此，编译器获得了所有可能被调用的候选方法。

2）接下来编译器将查看调用方法提供的参数类型，在所有名为 f 的方法中进行匹配，如果找到就选择这个方法，这个过程被称为**重载解析**（overloading resolution）。如果没有找到参数类型匹配的方法，或者发现经过类型转换后有多个方法与之匹配，就会报一个错误。

**引申**：一个方法的名字和参数列表称为方法的签名。例如：f(int) 和 f(String) 名字相同，但是参数类型不同，就是两个不同的签名方法。如果在子类定义了一个与超类签名相同的方法，子类的这个方法会覆盖超类中的方法，但是子类中的相同签名的方法，可以将返回类型设置为原返回类型的子类型，例如 Employee 类为超类，Manager 类为子类

```java
// Employee 类
public Employee getBuddy() {...}
// Manager 类
public Manager getBuddy() {...}
```

这两个 getBuddy 方法具有可协变得返回类型

3）如果是 private、static、final 方法或者构造器，编译器可以准确知道应该调用哪个方法，这个调用方式成为**静态绑定**（static binding）。与之对应的是，调用的方法依赖于隐式参数的实际类型，并在运行时实现动态绑定。

4）当程序运行，并采用动态绑定调用方法时，虚拟机一定调用与 x 所引用对象的实际类型最合适的那个类的方法。假设 x 的实际类型是 D，它是 C 类的子类。如果 D 类定义了方法 f(String)，就直接调用它；否则，将在 D 类的超类中运行 f(String)，以此类推。

由于每次调用方法，时间开销相当大，因此虚拟机为每个类创建了一个**方法表**（method table），其中列出了所有方法的签名和实际调用的方法。这样在调用方法之前，虚拟机仅查找这个表就可以了。一个类的方法表类似下面这样：

```java
// Employee 类
getName() -> Employee.getName();
getSalary() -> Employee.getSalary();
getHireDay() -> Employee.getHireDay();
raiseSalary(double) -> Employee.raiseSalary(double);

// Manager 类
getName() -> Employee.getName();
getSalary() -> Manager.getSalary();
getHireDay() -> Employee.getHireDay();
raiseSalary(double) -> Employee.raiseSalary(double);
setBonus(double) -> Manager.setBonus(double);
```

在上面的代码中，我们新建了三个 Employee 的对象变量，将一个 Manager 的变量对象放在里面，程序是怎么进行判断的呢？

```java
for (Employee e : staff) {
    System.out.println(e.getName() + " " + e.getSalary());
}
```

在运行时，调用 e.getSalary() 的解析过程为：

1）首先，虚拟机提取 e 的实际类型的方法表，可以能是 Employee、Manager 的方法表。

2）接下来，虚拟机搜索定义的 getSalary 签名的类，此时，虚拟机已经知道该调用哪个方法。

3）最后，虚拟机调用方法。

动态绑定还有一个重要特性，无需对现存代码进行修改，就可以对程序进行扩展。

比如新增一个 Executive 类，变量 e 有可能引用这个类的对象，我们不需要对 e.getSalary 的代码进行重新编译。

**注意**：在覆盖一个方法的时候，子类方法不能低于超类方法的可见性。

### 5.3 阻止继承：final类与方法

在定义某个类的时候，使用 final 修饰符声明，则可以阻止人们定义该类的子类，例如 String 类就是 final 类，不允许任何人定义 String 的子类。

在类的方法中，使用 final，则子类不能覆盖这个方法。

当然，类中的属性(域)也可以声明为 final，对于这种属性，构造对象后，就不允许改变他们的值了

```java
// 类使用 final
public final class Executive extends Manager {
    ...
}
// 类的方法使用 final
public class Employee {
    // 不能更改
    final String xxx = "233";
    ...
    // 子类不能覆盖该方法
    public final String getName() {
        return name;
    }
}
```

### 5.4 抽象类

在类的设计中，通常上层的类更具有通用性，甚至更加抽象。我们可以建立一个抽象类，将它派生为其他类的基类，而不作为想使用的特定的实例类。

在 Java 中，我们使用 abstract 关键字让一个类变成抽象类。

**注意**：包含一个或多个抽象方法的类本身必须声明为抽象的。

在一个抽象类中的抽象方法，只是充当占位的角色，它们的具体实现在子类中。扩展抽象类，有两种方式，一是在抽象类中定义部分抽象类方法或补丁已抽象类方法，这样就必须将子类也标记为抽象类；二是定义全部的抽象方法，这样子类就不是抽象的了。例：

```java
// 抽象类 Person
public abstract class Person {
    private String name;
    public Person(String name) {
        this.name = name;
    }
    // 抽象方法，没有具体实现
    public abstract String getDescription();
    ...
}

// 扩展抽象类 Student
public class Student extends Person {
    private String major;
    // 构造方法，其中 name 为超类的域
    publiic Student(String name, String major) {
        super(name);
        this.major = major;
    }
    
    // 实现抽象方法，子类就不为抽象的
    public String getDescription() {
        return "xxx";
    }
}
```

由于抽象类不能实例化对象，所有抽象的对象只能引用它的子类的对象。例：

```java
Person[] people = new Person[2];
people[0] = new Employee();
people[1] = new Student();
```

### 5.5 受保护访问

通常，我们知道在一个类中，将域标识为 private，而方法标识为 public ，声明为 private 的内容对其他类都是不可见的，对于子类也是一样的。

如果我们希望超类中的内容能被子类访问，可以将这些方法或域声明为 protected ，这样子类就可以访问超类的内容。

**注意**：如果将超类的中的域声明为 protected，对于使用这个类的其他子类，都可以访问受保护的域，这样违背了 OOP 提倡的数据封装原则。而受保护的方法更有实际意义。

Java四个访问修饰符：

1）仅对本类可见----private

2）对所有类可见----public

3）对本包和所有子类可见----protected

4）对本包可见----默认，不需要修饰符

### 5.6 反射

反射是 Java 的特征之一，它允许运行中的 Java 程序获取自身的信息，并且可以操作类或对象的内部属性。

反射机制可以用来：

- 在运行时分析类的能力
- 在运行时查看对象，例如，编写一个 toString 方法供所有类使用
- 实现通用的数组操作代码
- 利用 Method 对象，这个对象很像 C++ 中的函数指针

#### 5.6.1 Class类

在 Java 中可以通过一个类 Class 访问所有对象的所属的类，Object 类中 getClass() 方法将会返回一个 Class 类型的实例。

```java
Employee e;
Class c1 = e.getClass();
System.out.println(e.getClass());
```

上面的输出为类的名字，如果类在一个包中，包的名字也会作为类名的一部分。

也可以调用静态方法 forName 获取类名对应的 Class 对象。

```java
String className = "java.util.Random";
Class c1 = Class.forName(className);
```

使用 forName 方法，只有 className 为 类名或接口名才能执行，否则 forName 方法会抛出一个 checked exception (已检查异常)。所有使用这个方法，需要提供一个异常处理器 (exception handler)

可以使用 == 运算符比较两个类的对象。

可以使用 newInstance() 方法，动态创建一个类的实例

```java
e.getClass().newInstance();
```

将 forName 与 newInstance 配合使用，可以根据存储在字符串中的类名创建一个对象

```java
String s = "java.util.Random";
Object m = Class.forName(s).newInstance();
```

注：如果需要向类的构造器提供参数，就不要使用上面那条语句，而必须使用 Constructor 类中的 newInstance 方法。

#### 5.6.2 捕获异常

当程序运行过程中发生错误时，会抛出异常，抛出异常比终止程序要灵活得多，想要抛出异常，则需要提供一个“捕获”异常的处理器，对异常情况进行处理。

异常有两种类型：

- 未检查异常
- 已检查异常

对于已检查异常，编译器将会检查是否提供了处理器。

未检查异常，编译器不会查看是否提供了处理器，例如 访问 null 引用就属于未检查异常。

使用 try-catch 语句处理异常

```java
try {
    ...
} catch (Exception e) {
    e.printStackTrace();
}
```

如果 try 中的语句发生异常，则会跳到 catch 子句，利用 Throwable 类的 printStackTrace 方法打印出栈的轨迹，Throwable 是 Exception 类的超类。

对于已检查异常，只需提供相应的异常处理器，可以很容易的抛出已检查异常的方法。

#### 5.6.3 利用反射分析类的能力

下面简要介绍反射机制最重要的内容--检查类的结构。

在 java.lang.reflect包中有三个类 Field、Method 和 Constructor，它们分别用于描述类的域、方法和构造器。三个类都有一个叫 getName 的方法，用来返回项目的名称。

Field 类中有一个 getType 方法，用来返回域所属类型的 Class 对象。

Method 和 Constructor 类有能够报告参数类型的方法，Method 类还有一个可以报告返回类型的方法。

三个类还有一个叫做 getModifiers 的方法，它返回一个整型数值，用不同的位开关描述 public 和 static 这样的修饰符使用情况。也可以利用 java.lang.reflect 包中的 Modifier 类的静态方法分析 getModifiers 返回的整型数值，例如，可以使用 Modifier 类中的 isPublic、isPrivate 或 isFinal 判断方法或构造器是否为 public 、private 或 final。

Class 类中的 getFields、getMethods 和 getConstructor 方法将分别返回类提供的 public 域、方法和构造器数组，其中包括超类的公有成员。

Class 类的 getDeclareFields、getDeclareMethods 和 getDeclaredConstructors 方法将返回类中声明的全部域、方法和构造器，包括私有和受保护的成员，但不包括超类的成员。

使用上述的类与方法可以实现查看类的域、方法和构造器。

#### 5.6.4 在运行时使用反射分析对象

利用反射机制，我们可以在编译时查看还不清楚的对象域。

查看对象域的关键方法是 Field 类中的 get 方法。如果 f 是一个 Field 类型的对象，obj 是某个包含 f 域的类的对象，f.get(obj) 将返回一个对象，其值为 obj 域的当前值，示例代码：

```java
Employee harry = new Employee("Harry Hacker", 35000, 10, 1, 1989);
Class c1 = harry.getClass();

Field f = c1.getDeclaredField("name");

Object v = f.get(harry);
```

上述代码存在一个问题，由于 name 是一个私有域，所有 get 方法将会抛出一个 IllegalAccessException 异常，只有利用  get 方法才可以得到可访问的值。除非拥有访问权限，否则 Java 安全机制只允许查看任意对象有哪些域，而不允许读取它们的值。

反射机制的默认行为受限于 Java 的访问控制，然鹅，如果一个 Java 程序没有收到安全管理器的控制，就可以覆盖访问控制。为了达到这个目的，需要调用 Field、Method或 Constructor 对象的 setAccessible 方法

```java
f.setAccessible(true);
```

setAccessible 方法是 AccessibleObject 类中的一个方法，它是 Field、Method 和 Constructor 类的公有超类。

还有一个问题是，name 是一个 String，因此可以吧它作为 Object 返回，如果我们要返回 salary 域，它属于 double 类型，Java 中数值类型不是对象，要解决这个问题，可以使用 Field 类中的 getDouble 方法，也可以调用 get 方法。

#### 5.7.5 使用反射编写泛型数组代码

Java.lang.reflect 包中的 Array 类允许动态地创建数组，可以使用这一特性，实现扩展已经填满的数组。

通过获取传入数组的类型、新数组的长度，使用 Array.newInstance(componentType, newLength) 创建一个与传入类型相同的数组。下面为实现代码：

```java
public static Object goodCopyOf(Object a, int newLength) {
    Class c1 = a.getClass();
    if (!c1.isArray()) {
        return null;
    }
    Class componentType = c1.getComponentType();
    int length = Array.getLength(a);
    Object newArray = Array.newInstance(componentType, newLength);
    System.arraycopy(a, 0, newArray, 0, Math.min(length, newLength));
    return newArray;
}

// 使用
int[] a = {1, 2, 3, 4, 5};
a = (int[]) goodCopyOf(a, 10);
```

### 5.7 继承的设计技巧

1. 将公共操作和域放在超类
2. 不要使用受保护的域
3. 使用继承实现 is-a 关系（需要明确继承的类是否与超类有关联）
4. 除非所有继承的方法都有意义，否则不要使用继承
5. 在覆盖方法时，不要改变预期的行为（不要毫无原由的改变行为）
6. 使用多台，而非类型信息（使用多态和接口比多类型检测更易于维护和扩展）
7. 不要过多地使用反射（反射很脆弱）

## 第六章 接口、lambda表达式与内部类

### 6.1 接口

#### 6.1.1 接口概念

在 Java 中，接口不是类，而是对类的一组需求描述，这些类要遵从接口描述的统一格式进行定义。

对于实现了某个接口的类，需要实现接口中的方法。例如，Arrays 类中的 sort 方法可以对对象数组进行排序，但对象所属的类必须实现了 Comparable 接口。下面为 Comparable 接口代码:

```java
public interface Comparable {
    int compareTo(Object other);
}
```

注：在 Java SE 5.0，Comparable 接口已经改进为泛型类型

```java
public interface Comparable<T> {
    int compareTo(T other);
}
// 实现
int compareTo(Employee other);
```

接口中的所有方法自动属于 public。因此，在接口声明方法时，不必提供关键字 public。

接口绝不能含有实例域，在 Java SE 8 之前，不能在接口中实现方法，而在 8 后，可以在接口中提供简单方法，但是这些方法也不能引用实例域，接口没有实例。

提供实例域和方法应该是实现接口的类完成的工作，可以把接口看成是没有实例域的抽象类（还是有一定区别）。

实现接口分为两个步骤：

1）将类声明为实现给定的接口。

2）对接口中的所有方法进行定义。

将类声明为实现某个接口，需要使用关键字 implements。

```java
class Employee implements Comparable {
    // 需要实现 compareTo 方法
    public int compareTo(Object otherObject) {
        Employee other = (Employee) otherObject;
        return Double.compare(salary, other.salary);
    }
}
```

为什么不能在 Employee 类中直接提供一个 compareTo 方法，而必须实现 Comparable 接口呢？

主要原因是 Java 是一种强类型语言，在调用方法时，编译器会检查这个方法是否存在。在 sort 方法中可能存在下面这样的语句：

```java
if (a[i].compareTo(a[j]) > 0) {
    ...
}
```

为此，编译器必须确认 a[i] 一定有 compareTo方法。如果 a 是一个 Comparable 对象的数组，就可以确保拥有 compareTo 方法，因此每个实现 Comparable 接口的类都必须提供这个方法的定义。

#### 6.1.2 接口的特性

接口不是类，不能通过 new 运算符实例化一个接口。虽然不能构造接口对象，但是可以声明接口的变量；接口变量必须引用了接口的类对象。

使用 instance 可以检查一个对象是否实现了某个特定的接口。

```java
// Error
x = new Comparable(...);
// OK
Comparable x;
// OK provided Employee implements Comparable
x = new Employee(...);
// instance
if (anObject instanceof Comparable) {
    ...
}
```

接口也可以被扩展。例如，假设有一个称为 Moveable 接口：

```java
public interface Moveable {
    void move(double x, doule y);
}
```

然后，可以以它为基础扩展一个叫做 Powered 的接口：

```java
public interface Powered extends Moveable {
    double milesPerGallon();
}
```

虽然在接口中不能包含实例域或静态方法，但却可以包含常量：

```java
public interface Powered extends Moveable {
    double milesPerGallon();
    // a public static final constant
    double SPEED_LIMIT = 95;
}
```

与接口中的方法都自动设置爱为 public 一样，接口中的域都将自动设为 **public static final**。

任何实现了接口的类都自动继承了这些常量。

每个类只能拥有一个超类，但可以实现多个接口，这为定义类的行为提供了极大的灵活性。

#### 6.1.3 接口和抽象类

一个类只能扩展于一个类，如果 Employee 类已经扩展于一个类，例如 Person，如果再想扩展抽象类就会发生错误，但一个类可以像下面这样实现多个接口：

```java
// Error
class Employee extends Person, Comparable {}
// OK
class Employee extends Person implements Comparable {}
```

有些程序语言允许一个类有多个超类，例如 C++，我们将此特性称为多重继承（multiple inheritance），Java不支持多重继承，主要原因是多继承会让语言本身变得复杂，效率也会降低（如同 Eiffel）。

实际上，接口可以提供多重继承的大多数好处，还能避免多重继承的复杂性和低效性。

#### 6.1.4 静态方法

在 Java SE 8 中，允许在接口中增加静态方法。理论上讲，没有任何理由认为这是不合法的，只是有违于将接口作为抽象规范的初衷。

通常的做法是将静态方法放在伴随类中。在标准库中，你会看到成对出现的接口和实用工具类，如 Collection/Collections 或 Path/Paths。

在 Path 类中，可以为 Path 接口增加以下方法：

```java
// Paths 伴随类
Paths.get("jdk1.8.0", "jre", "bin");
// Java 8 中，这样写，可以不需要 Paths
public interface Path {
    public static Path get(String first, String... more) {
        return FileSystems.getDefault().getPath(first, more);
    }
    ...
}
```

这样一来，Paths 类就没有必要了，在实现接口的时候，不再需要为实用工具提供另外一个伴随类。

#### 6.1.5 默认方法

可以为接口方法提供一个默认实现。必须用 default 修饰符标记这样一个方法。

```java
public interface Comparable<T> {
    defalut int comparaTo(T other) {
        return 0;
    }
    ...
}
```

但是这样做没有太大的用处，因为 Comparable 的每个实际实现都要覆盖这个方法。不过有些情况，默认方法可能有很有用。例如，希望在发生鼠标点击事件时得到通知，就要实现方法的接口。

#### 6.1.6 解决默认方法冲突

如果先在一个接口中将一个方法定义为默认方法，然后又在超类或另外一个接口中定义了同样的方法，会发生什么情况？

在 Java 的相应的规则为：

1）超类优先，如果一个超类提供了一个具体方法，同名且有相同参数类型的默认方法会被忽略。

2）接口冲突，如果一个超接口提供了一个默认方法，另一个接口提供了一个 同名且参数类型相同的方法，必须覆盖这个方法来解决冲突。

对于第二个规则。考虑另一个包含 getName 方法的接口：

```java
interface Named {
    default String getName() {
        return getClass().getName() + "_" + hashCode();
    }
}
// 两个接口都有 getName 方法
class Student implements Person, Named {
    ...
}
```

这时，类会继承 Person 和 Named 接口提供的两个不一致的  getName 方法，编译器会报告一个错误，需要自行解决。只需要在 Student 类中提供一个 getName 方法，在这个方法中，选择其中一个方法就可以了。

```java
class Student implements Person, Named {
    public String getName() {
        return Person.super.getName();
    }
}
```

### 6.2 接口示例

#### 6.2.1 接口与回调

**回调**（callback）是一种常见的程序设计模式。在这种模式中，可以指出某个特定事件发生时应该采取的动作。例如，可以指出在按下鼠标或选择某个菜单项时，应该采取什么行动。

在构造定时器时，需要设置一个时间间隔，并告之定时器，当到达时间间隔需要做些什么操作。

如何告之定时器做什么呢？在很多程序设计语言中，可以提供一个函数名，定时器周期性调用它。但是在 Java 标准类库中的类采用的是面向对象方法。它将某个类的对象传递给定时器，然后定时器调用这个对象的方法。

定时器还需要知道调用哪个方法，并要求传递的对象所属的类实现了 java.awt.event 包的 ActionListener 接口。

```java
public interface ActionListener {
    void actionPerformed(ActionEvent event);
}
```

当到达指定时间间隔，定时器就调用 actionPerformed 方法。

下面这个这个程序，运行后会显示一个包含 “Quit program？”字样的对话框，并且10秒后会在控制台输出定时器消息。

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Date;

/**
 * Author: maxwell
 * Date: 2020/4/18
 * Desc:
 */
public class TimerTest {
    public static void main(String[] args) {
        ActionListener listener = new TimerPrinter();

        // construct a timer that calls the listener
        Timer t = new Timer(10000, listener);
        t.start();
        JOptionPane.showMessageDialog(null, "Quit program?");
        System.exit(0);
    }
}

class TimerPrinter implements ActionListener {

    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("Ac thye tone, the time is " + new Date());
        Toolkit.getDefaultToolkit().beep();
    }
}
```

#### 6.2.2  对象克隆

这一节，我们会使用 Cloneable 接口实现对象的克隆。

这个接口提供了一个安全的 clone 方法。通过 clone 方法，可以将一个对象复制一份，两个对象拥有不同的状态。

但需要注意的是，clone 方法是 Object 的一个 protected 方法，这说明你的代码不能直接调用这个方法。只有 Employee 类可以克隆 Employee 对象。而且如果克隆的对象包括了子对象的引用，拷贝域也会得到相同的子对象的引用，这样原对象和克隆对象还是会有一些共享信息，这种默认的克隆操作称为**浅拷贝**，它并没有克隆对象中引用的其他对象。

对于浅拷贝会有什么影响？这要看具体情况。如果原对象和浅克隆对象共享的子对象是不可变得，那么这种共享是安全的。如果子对象是可变的，必须重新定义 clone 方法来建立一个深拷贝，同时克隆所有子对象。

下方代码克隆了 Employee 类的一个实例，并且为子对象也建立拷贝。

```java
public class CloneTest {
    public static void main(String[] args) {
        Employee original = new Employee("John Q. Public", 50000);
        original.setHireDay(2000, 1, 1);
        try {
            Employee copy = original.clone();
            copy.raiseSalary(10);
            copy.setHireDay(2002, 12, 31);
            System.out.println("original = " + original);
            System.out.println("copy = " + copy);
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}

public class Employee implements Cloneable {
    private String name;
    private double salary;
    private Date hireDay;

    public Employee() {
    }

    public Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
        hireDay = new Date();
    }

    public Employee clone() throws CloneNotSupportedException {
        Employee cloned = (Employee) super.clone();
        cloned.hireDay = (Date) hireDay.clone();
        return cloned;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "name='" + name + '\'' +
                ", salary=" + salary +
                ", hireDay=" + hireDay +
                '}';
    }

    public void raiseSalary(double byPercent) {
        double raise = salary * byPercent / 100;
        salary += raise;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    public Date getHireDay() {
        return hireDay;
    }

    public void setHireDay(int year, int month, int day) {
        Date newHireDay = new GregorianCalendar(year, month -1, day).getTime();
        hireDay.setTime(newHireDay.getTime());
    }
}
```

### 6.3 lambda 表达式

#### 6.3.1 lambda 表达式语法

lambda 表达式是一个可传递的代码块，可以在以后执行一次或多次。

lambda 表达式的代码为下面这种格式

```java
// first.length() - second.length()
(String first, String second) -> first.length() - second.length();
```

lambda 表达式形式：参数，箭头（->）以及一个表达式，如果要完成的代码一个表达式放不下，可以放在 {} 中，并包含显式的 return 语句。

```java
(String first, String second) -> {
    if (first.length() < second.length()) {
        return -1;
    } else if (first.length() > second.length()) {
        return 1;
    } else {
        return 0;
    }
}
```

即使 lambda 表达式没有参数，仍要提供空括号，就像无参数方法一样：

```java
() -> { for (int i = 100; i >= 0; i--) System.out.println(i); }
```

如果可以推导出一个 lambda 表达式的参数类型，则可以忽略其类型。

```java
// 编译器可以推导出 first 和 second 必然是字符串，因为这个 lambda 表达式赋值给了一个字符串比较器。
Comparator<String> comp
    = （first, second) -> first.length() - second.length();
```

**如果方法只有一个参数，而且这个参数类型可以推导得出，那么还可以省略小括号：**

```java
ActionListener listener = event -> 
    System.out.println("The time is " + new Data());
```

无需指定 lambda 表达式的返回类型，lambda 表达式的返回类型会根据上下文推导出来。

如果一个 lambda 表达式只在某些分支返回一个值，而在另外一个分支不返回值，这是不合法的。

```java
// Error
(int x) -> { if (x >= 0) return 1;}
```

下面是一个在比较器和动作监听器中使用 lambda 表达式。

```java
import javax.swing.*;
import java.util.Arrays;
import java.util.Date;

/**
 * Author: maxwell
 * Date: 2020/4/19
 * Desc:
 */
public class LambdaTest {
    public static void main(String[] args) {
        String[] planets = new String[]{"Mercury", "Venus", "Earth", "Mars", "Jupiter", "Saturn",
                "Uranus", "Neptune"};
        System.out.println(Arrays.toString(planets));
        System.out.println("Sorted in dictionary order:");
        Arrays.sort(planets);
        System.out.println(Arrays.toString(planets));
        System.out.println("Sorted by length: ");
        Arrays.sort(planets, (first, second) -> first.length() - second.length());
        System.out.println(Arrays.toString(planets));

        Timer t = new Timer(1000, event -> System.out.println("The time is " + new Date()));

        t.start();

        JOptionPane.showMessageDialog(null, "Quit program?");
        System.exit(0);
    }
}
```

#### 6.3.2 函数式接口

在 Java 中已经有很多封装代码块的接口，如果 ActionListener 或 Comparator。lambda 表达式与这些接口是兼容的。

对于只有一个抽象方法的接口，需要这种接口对象时，就可以提供一个 lambda 表达式。这种接口称为**函数式接口**（functional interface）

下面以 Arrays.sort 方法为例，它第二个参数需要一个 Comparator 实例， Comparatoc 就是一个方法的接口，所有可以提供一个 lambda 表达式：

```java
Arrays.sort(words, (first, second) -> first.length() - second.length());
```

在底层，Arrays.sort 方法会接收实现了 Comparator<String> 的某个类的对象。在这个对象上调用 compare 方法会执行 lambda 表达式的体。

最好把 lambda 表达式看做是一个函数，而不是一个对象，另外要接收 lambda 表达式可以传递到函数式接口。

Lambda 表达式可以转换为接口，例如如下：

```java
Timer t = new Timer(1000, event -> {
    System.out.println("xxx");
    Toolkit.getDefaultToolkit().beep();
});
```

与使用实现了 ActionListener 接口的类相比，这个代码可读性要好的多。

实际上，在 Java 中，对 lambda 表达式所能做的也只是能转换为函数式接口。

Java API 在 java.util.function 包中定义了很多非常通用的函数式接口。其中一个接口 BiFunction<T, U, R> 描述了参数类型为 T 和 U 而且返回类型为 R 的函数。可以把我们的字符串比较 lambda 表达式保存在这个类型的变量中：

```java
BiFunction<String, String, Integer> comp
    = (first, second) -> first.length() - second.length();
```

在 Java 中想要用 lambda 表达式做某些处理，需要知道表达式的用途，为它建立一个特定的函数式接口。

Java.util.function 包中有一个尤其有用的接口 Predicate:

```java
public interface Predicate<T> {
    boolean test(T t);
}
```

ArrayList 类有一个 removeIf 方法，它的参数就是一个 Predicate。这个接口专门用来传递 lambda 表达式。例如下面的语句将从一个数组列表删除所有 null 值：

```java
list.removeIf(e -> e == null);
```

#### 6.3.3 方法引用

有时，可能已经有现成的方法可以完成你想要的传递到其他代码的动作。例如，假设你希望只要出现一个定时器事件就打印这个事件对象。为此，可以这么调用:

```java
Timer t = new Timer(1000, event -> System.out.println(event));
```

但是，如果直接把 println 方法传递给 Timer 构造器就更好了。具体做法如下：

```java
Timer t = new Timer(1000, System.out::println);
```

表达式 System.out::println 是一个**方法引用**（method reference），它等价于 lambda 表达式 x -> System.out.println(x);

从上面的例子可以看出，要使用 :: 操作符分隔方法名和对象或类名。主要有 3 种情况：

- Object::instanceMethod
- Class::staticMethod
- Class::instanceMethod

前 2 种情况中，方法引用等价于提供方法参数的 lambda 表达式。例如 System.out::println 等价于 x -> System.out.println(x)，Math::pow 等价于 (x, y) -> Math.pow(x, y)。

第 3 种情况，第1个参数会成为方法的目标。例如，String::compareToIgnoreCase 等同于 (x, y) -> x.compareToIgnoreCase(y)。

#### 6.3.4 构造器引用

构造器引用与方法引用类似，只不过方法名为 new。例如，Person::new 是 Person 构造器的一个引用。哪一个是构造器呢？这取决于上下文。假设你有一个字符串列表。可以把它转换为一个 Person 对象数组，为此要在各个字符串上调用构造器：

```java
ArrayList<String> names = ...;
Stream<Person> stream = names.stream().map(Person::new);
List<Person> people = stream.collect(Collectors.toList());
```

上面代码中的 map 方法会为各个列表元素调用 Person(String) 构造器。如果有多个 Person 构造器，编译器会选择一个 String 参数的构造器，这是通过上下文推导出的。

可以使用数组类型建立构造器引用。例如：int[]::new 是一个构造器引用，它有一个参数：即数组的长度。这等价于 lambda 表达式 x -> new int[x]。

Java 有一个限制，无法构造泛型类型 T 的数组。数组构造器对于克服这个限制很有用。

#### 6.3.5 变量作用域

通常，你可能希望能够在 lambda 表达式中访问外围方法或类中的变量。例如下面这个例子：

```java
public static void repeatMessage(String text, int delay) {
    ActionListener listener = event -> {
        System.out.println(text);
        Toolkit.getDefaultToolkit().beep();
    };
    new Timer(delay, listener).start();
}
// 调用
repeatMessage("Hello", 1000);
```

注意，在 lambda 表达式中的变量 text，这个变量是来自 repeatMessage 方法的一个参数变量。如果这个 lambda 表达式在 repeatMessage 调用返回很久以后才运行，而那时这个参数变量已经不存在了，该如何保留这个 text 变量？

要了解到底会发生什么，下面来巩固一下我们对 lambda 表达式的理解。lambda 表达式有 3 个部分：

1）一个代码块；

2）参数；

3）自由变量的值，这是指非参数而且不在代码中定义的变量。

在上面这个例子中，lambda 表达式有1个自由变量 text。表示 lambda 表达式的数据结构必须存储自由变量的值，在这里就是字符串 "Hello"。我们说它被 lambda 表达式捕获（captured）例如：如果把一个 lambda 表达式转化为包含一个方法的对象，这样自由变量的值就会复制到这个对象的实例变量中。

**注：**关于代码块以及自由变量值有一个术语：闭包（closure）。在 Java 中，lambda 表达式就是闭包。

可以看到，lambda 表达式可以捕获外围作用域中变量的值，但是捕获的变量，在 lambda 表达式中，只能引用值不会改变的变量。例如，下面的做法是不合法的：

```java
public static void countDown(int start, int delay) {
    ActionListener listener = event -> {
        start--; // error
        ...
    };
    ...
}
```

之所以有这个限制，是因为如果在 lambda 表达式中可以改变变量，并发执行多个动作时会不安全。

另外如果在 lambda 表达式中引用的变量，而这个变量可能在外部改变，这也是不合法的。例如：

```java
public static void repeat(String text, int count) {
    for (int i = 1; i <= count; i++) {
        ActionListener listener = event -> {
            // Error: Cannot refer to changing i
            System.out.println(i + ": " + text);
        }
    }
}
```

这里有一条规则：**lambda 表达式中捕获的变量必须是最终变量**（effectively final）。最终变量指的是，这个变量初始化后就不会再为它赋新值。

Lambda 表达式的体育嵌套块有相同的作用域，所有在 lambda 表达式中声明一个与局部变量同名的参数或局部变量是不合法的。

```java
Path first = Paths.get("/usr/bin");
Comparator<String> comp = (first, second) -> first.length() - second.length();
// Error: Variable first already defined
```

在一个 lambda 表达式中使用 this 关键字时，是指创建这个 lambda 表达式的方法的 this 参数。例如：

```java
public class Application() {
    public void init() {
        ActionListener listener = event -> {
            System.out.println(this.toString());
            ...
        }
    }
}
```

表达式 this.toString() 会调用 Application 对象的 toString 方法，而不是 ActionListener 实例的方法。

