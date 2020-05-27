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

#### 6.3.6 处理 lambda 表达式

使用 lambda 表达式的重点是**延迟执行**（deferred execution）。如果想要立即执行，完全可以直接执行，而不需要把它包装在一个 lambda 表达式中。之所以希望以后执行代码有很多原因，如：

- 在一个单独的线程中运行代码；
- 多次运行代码；
- 在算法的适当位置运行代码 (例如：排序中的比较操作)；
- 发生某种情况时执行代码 (如：点击了一个按钮，数据到达等等)；
- 只在必要时运行代码。

比如你想要重复一个动作 n 次。将这个动作和重复次数传递到一个 repeat 方法：

```java
repeat(10, () -> System.out.println("Hello, World!"));
```

要接受这个 lambda 表达式，需要选择一个函数接口，这里我们使用 Runnable 接口：

```java
public static void repeat(int n, Runnable action) {
    for (int i = 0; i < n; i++) {
        action.run();
    }
}
```

需要说明，调用 action.run() 时会执行这个 lambda 表达式的主体。

![](http://images.csmaxwell.xyz/20200422190215.png)

现在让这个例子更复杂一下。我们希望告诉这个动作它出现在哪一次迭代中。为此，需要选择一个合适的函数式接口，其中要包含一个方法，这个方法有一个 int 参数而且返回类型为 void。处理 int 值得标准接口如下：

```java
public interface IntConsumer {
    void accept(int value);
}
// 改进版
public static void repeat(int n, IntConsumer action) {
    for (int i = 0; i < n; i++) {
        action.accept(i);
    }
}
// 调用
repeat(10, i -> System.out.println("Countdown: " + (9 - i)));
```

下面列出了基本类型 int、long 和 double 的34个可能的规范。最好使用这些特殊化规范来减少自动装箱。

![](http://images.csmaxwell.xyz/20200422193746.png)

### 6.4 内部类

内部类（inner class）是定义在另一个类中的类。为什么需要使用内部类？主要原因有一下三点：

- 内部类方法可以访问该类定义所在的作用域中的数据，包括私有的数据。
- 内部类可以对同一个包中的其他类隐藏起来。
- 当想要定义一个回调函数且不想编写大量代码时，使用**匿名**（anonymous）内部类比较便捷

#### 6.4.1 使用内部类访问对象状态

内部类的语法比较复杂，为此，我们选择一个简单但不太实用的例子说明内部类的使用方式。

下面将进一步分析 TimerTest 示例，并抽象出一个 TalkingClock 类。构造一个语音时钟时需要提供两个参数：发布通告的间隔和开关铃声的标志。

```java
public class TalkingClock {
    private int interval;
    private boolean beep;
    
    public TalkingClock(int interval, boolean beep) {...}
    public void start() {...}
    
    public class TimePrinter implements ActionListener {
        ...
    }
}
```

需要注意，这里的 TimerPrinter 类位于 TalkingClock 类内部。这并不意味着每个 TalkingClock 都有一个 TimePrinter 实例域。TimerPrinter 对象是由 TalkingClock 类的方法构造。

下面是 TimePrinter 类的详细内容。需要注意 actionPerformed 方法在发出铃声之前检查了 beep 标志。

```java
public class TimePrinter implements ActionListener {
    public void actionPerformed(ActionEvent event) {
        System.out.println("At the tone, the time is " + new Date());
        if (beep) {
            Toolkit.getDefaultToolkit().beep();
        }
    }
}
```

注意，TimePrinter 类没有实例域或者名为 beep 的变量，取而代之的是 beep 引用了创建 TimePrinter 的 TalkingClock 对象的域。内部类既可以访问自身的数据域，也可以访问创建它的外围类对象的数据域。

为了能够运行这个程序，内部类的对象总有一个隐式引用，它指向了创建它的外部类对象。

这个引用在内部类的定义中是不可见的，然鹅，在内部类中方法是等价于下列形式：

```java
public void actionPerformed(ActionEvent event) {
    if (外部数据域.beep) xxx;
}
```

外围类的引用在构造器中设置，编译器修改了所有内部类的构造器，添加了一个外围类引用的参数。 TimePrinter 没有定义构造器，编译器为这个类生成了一个默认的构造器，代码如下面所示：

```java
public TimePrinter(TalkingClock clock) {
    outer = clock;
}
```

其中 outer 只是用来说明内部类的这种机制。

当在 start 方法中创建了 TimePrinter 对象后，编译器就会将 this 引用传递给当前的语音构造器：

```java
ActionListener listener = new TimePrinter(this);
```

下面为该测试内部类的完整程序（注：内部类可以是私有类）

```java
public class InnerClassTest {
    public static void main(String[] args) {
        TalkingClock clock = new TalkingClock(1000, true);
        clock.start();

        JOptionPane.showMessageDialog(null, "Quit program?");
        System.exit(0);
    }
}

/**
 * A clock that prints the time in regular intervals.
 */
class TalkingClock {
    private int interval;
    private boolean beep;

    /**
     * Constructs a talking clock
     * @param interval the interval between messages (in milliseconds)
     * @param beep true if the clock should beep
     */
    public TalkingClock(int interval, boolean beep) {
        this.interval = interval;
        this.beep = beep;
    }

    public void start() {
        ActionListener listener = new TimePrinter();
        Timer t = new Timer(interval, listener);
        t.start();
    }

    public class TimePrinter implements ActionListener {
        public void actionPerformed(ActionEvent event) {
            System.out.println("At the tone, the time is " + new Date());
            if (beep) {
                Toolkit.getDefaultToolkit().beep();
            }
        }
    }
}
```

#### 6.4.2 内部类的特殊语法规则

在上一节中，我们已经讲述了内部类有一个外围类的引用 outer。事实上，使用外围类引用的正规语法还要复杂一些。表达式 OuterClass.this 表示外围类引用。例如，可以像下面这样编写 TimePrinter 内部类的 actionPerformed 方法：

```java
public void actionPerformed(ActionEvent event) {
    if (TalkingClock.this.beep) {
        xxx
    }
}
```

注：内部类中声明的所有静态域都必须是 final。因为我们希望一个静态域只有一个实例，不过对于每个外部对象，会分别有一个单独的内部类实例。内部类也不能有 static 方法。

#### 6.4.3 内部类是否有用、必要、安全

看不懂，略过...

#### 6.4.4 局部内部类

在上面的代码中，我们发现 TimerPrinter 这个类的名字只在 start 方法中创建这个类型的对象时使用了一次。

当遇到这类情况，可以在一个方法中定义局部类。

```java
public void start() {
    class TimePrinter implements ActionListener {
        public void actionPerformed(ActionEvent event) {
            xxx
        }
    }
    
    ActionListener listener = new TimePrinter();
    Timer t = new Timer(interval, listener);
    t.start();
}
```

局部类不能用 public 或 private 访问说明符进行声明，它的作用域被限定在这个局部类的块中。

局部类有一个优势，即对外部世界可以完全隐藏起来。即使 TalkingClock 类中的其他代码不能访问它。除 start() 方法之外，没有任何方法知道 TimePrinter 类的存在。

#### 6.4.5 由外部方法访问变量

与其他内部类想比较，局部类还有一个优点。它不仅能够访问它们的外部类，还可以访问局部变量，不过这些局部变量必须为 final。

下面，我们将 TalkingClock 构造器的参数 interval 和 beep 移至 start 方法中。

```java
public void start(int interval, boolean beep) {
    class TimePrinter implements ActionListener {
        public void actionPerformed(ActionEvent event) {
            System.out.println("xxx");
            if (beep) {
                Toolkit.getDefaultTookkit().beep();
            }
        }
    }
    
    ActionListener listener = new TimePrinter();
    Timer t = new Timer(interval, listener);
    t.start();
}
```

现在 TalkingClock 类不需要存储 beep 变量，它现在只是引用 start 方法的 beep 参数变量。

问题：这里书上写程序访问不了 beep，但是实际运行程序可以访问 beep。

#### 6.4.6 匿名内部类

将局部内部类的使用再深入一步。假如只创建这个类的一个对象，就不必命名了。这种类称为匿名内部类（anonymous inner class）。

```java
public void start(int interval, boolean beep) {
    // 匿名内部类
     ActionListener listener = new ActionListener() {
        public void actionPerformed(ActionEvent event) {
            System.out.println("At the tone, the time is " + new Date());
            if (beep) {
                Toolkit.getDefaultToolkit().beep();
            }
        }
    }

    Timer t = new Timer(interval, listener);
    t.start();
}
```

这种语法确实有些难以理解。它的含义是：创建一个实现 ActionListener 接口的类的新对象，需要实现的方法 actionPerformed 定义在括号内。

通常的语法格式为：

```java
new SuperType(construction parameters) {
	inner class methods and data
}
```

由于构造器的名字必须与类名相同，而匿名类没有类名，所有，匿名类不能有构造器。取而代之的是，将构造器参数传递给超类构造器。尤其是在内部类实现接口的时候，不能有任何构造参数，还需要像下面这样提供一组括号:

```java
new InterfaceType() {
    methods and data
}
```

我们来对比一下，一个类构造的新对象与构造一个扩展了那个类的匿名内部类的对象之间有什么区别。

```java
// a Person object
Person queen = new Person("Mary");

// an object of an inner class extending Person
Person count = new Person("Dracula") {...}
```

如果构造参数的闭小括号后面跟了一个大括号，正在定义的就是匿名内部类。

多年来，Java 程序员习惯的做法是用匿名内部类实现事件监听器和其他回调。如今最好还是使用 lambda 表达式。这一节的 start 方法用 lambda 表达式来写就简介的多：

```java
public void start(int interval, boolean beep) {
    Timer t = new Timer(inter, event -> {
        System.out.println("xxx");
        if (beep) Toolkit.getDefaultToolkit().beep();
    });
    t.start();
}
```

**技巧**：下面这个技巧称为 “双括号初始化”，这里利用了内部类的语法。假设你想构造一个数组列表，并将它传递到一个方法：

```java
ArrayList<String> friends = new ArrayList<>();
friends.add("Harry");
friends.add("Tony");
invite(friends);
```

或者，你可以使用匿名列表：

```java
invite(new ArrayList<String>() {{ add("Harry"); add("Tony"); }});
```

注意这里的双括号，外层括号建立了 ArrayList 的一个匿名子类，内存则是对象构造块。

#### 6.4.7 静态内部类

有时候，使用内部类只是为了吧一个类隐藏在另外一个类的内部，并不需要内部类引用外围类的对象。为此，可以讲内部类声明为 static，以便取消产生的引用。

下面为一个使用静态内部类的经典例子。考虑一下计算数组中最大值和最小值的问题。当然，可以编写两个方法，一个计算最大、一个计算最小。在调用这两个方法的时候，数组被遍历了两次。如果只遍历数组一次，就能够计算最小值和最大值，就可以大大提高效率。

```java
double min = Double.POSITIVE_INFINITY;
double max = Double.NEGATIVE_INFINITY;
for (double v : values) {
    if (min > v) {
        min = v;
    }
    if (max < v) {
        max = v;
    }
}
```

这个方法必须返回两个数值，因此需要定义一个包含两个值的类 Pair

```java
class Pair {
    private double first;
    private double second;
    
    public Pair(double f, double s) {
        first = f;
        second = s;
    }
    // getter...
}
```

minmax方法返回一个 Pair 类型的对象

```java
class ArrayAlg {
    public static Pair minmax(double[] values) {
        ...
        return new Pair(min, max);
    }
}
```

这个方法的调用者可以使用 getter 方法获取答案。

完整代码如下：

```java
public class StaticInnerClassTest {
    public static void main(String[] args) {
        double[] d = new double[20];
        for (int i = 0; i < d.length; i++) {
            d[i] = 100 * Math.random();
        }
        ArrayAlg.Pair p = ArrayAlg.minmax(d);
        System.out.println("min = " + p.getFirst());
        System.out.println("max = " + p.getSecond());
    }
}

class ArrayAlg {
    public static class Pair {
        private double first;
        private double second;

        public Pair(double first, double second) {
            this.first = first;
            this.second = second;
        }

        public double getFirst() {
            return first;
        }

        public double getSecond() {
            return second;
        }
    }

    public static Pair minmax(double[] values) {
        double min = Double.POSITIVE_INFINITY;
        double max = Double.NEGATIVE_INFINITY;
        for (double v : values) {
            if (min > v) {
                min = v;
            }
            if (max < v) {
                max = v;
            }
        }
        return new Pair(min, max);
    }
}
```

### 6.5 代理

什么是代理？代理是在运行时创建一个实现了一组给定接口的新类。这种功能只有编译时无法确定需要实现那个接口才有必要使用。

#### 6.5.1 何时使用代理

假设有一个表示接口的 Class 对象（有可能只包含一个接口），它的确切类型在编译时无法知道，要想构造一个实现这些接口的类，就需要使用 newInstance 方法或反射找出这个类的构造器。但是，不能实例化一个接口，需要在程序处于运行状态是定义一个新类。

为了解决这个问题，有些程序将会生成代码，将这些代码放置在一个文件中，调用编译器，然后加载结果类文件。然鹅，这样做的速度会比较慢，并且需要将编译器与程序放在一起。而代理机制则是一种更好的解决方案。代理类在可以运行时创建全新的类。这样的代理类能够实现指定的接口。尤其是，它具有下列方法：

- 指定接口所需要的全部方法。
- Object 类中的全部方法，例如，toString、equals 等。

然鹅，不能在运行时定义这些方法的新代码。而是要提供一个调用处理器（invocation handler）。调用处理器是实现了 InvocationHandler 接口的类对象。在这个接口中只有一个方法：

```java
Object invoke(Object proxy, Method method, Object[] args)
```

无论何时调用代理对象的方法，调用处理器的 invoke 方法都会被调用，并向其传递 Method 对象和原始的调用参数。

#### 6.5.2 创建代理对象

要想创建一个代理对象，需要使用 Proxy 类的 newProxyInstance 方法。这个方法有三个参数：

- 一个类加载器（class loader）。作为 Java 安全模型的一部分，可以使用 null 表示默认的类加载器。
- 一个 Class 对象数组，每个元素都是需要实现的接口。
- 一个调用处理器。

下面程序为使用代理对象对二分查找进行跟踪。

```java
public class ProxyTest {
    public static void main(String[] args) {
        Object[] elements = new Object[1000];
        for (int i = 0; i < elements.length; i++) {
            Integer value = i + 1;
            InvocationHandler handler = new TraceHandler(value);
            Object proxy = Proxy.newProxyInstance(null, new Class[] { Comparable.class}, handler);
            elements[i] = proxy;
        }

        Integer key = new Random().nextInt(elements.length) + 1;

        int result = Arrays.binarySearch(elements, key);

        if (result >= 0) {
            System.out.println(elements[result]);
        }
    }
}

class TraceHandler implements InvocationHandler {

    private Object target;

    public TraceHandler(Object target) {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        System.out.print(target);
        System.out.print("." + method.getName() + "(");
        if (args != null) {
            for (int i = 0; i < args.length; i++) {
                System.out.print(args[i]);
                if (i < args.length - 1) {
                    System.out.print(", ");
                }
            }
        }
        System.out.println(")");
        return method.invoke(target, args);
    }
}
```

#### 6.5.3 代理类的特性

现在我们已经看到代理类的应用，接下来了解他们的特性。需要记住，代理类是在程序运行过程总创建的。然而，一旦被创建，就变成了常规类，与虚拟机中的任何其他类没有什么区别。

所有的代理类都扩展与 Proxy 类。一个代理类只有一个实例域---调用处理器，它定义在 Proxy 的超类中。为了履行代理对象的职责，所需要的任何附加数据都必须存储在调用处理器中。

## 第七章 异常、断言和日志

在理想状态下，用户输入数据的格式永远是正确的，选择打开的文件也一定存在，并且永远不会出现 bug 。但这永远是不可能的 XD 。

当一个用户在运行程序期间，由于程序的错误或者一些外部环境的影响造成用户数据的丢失，用户就可能不再使用这个程序了，为了避免这类事情的发生，至少要做到以下几点：

- 向用户通告错误；
- 保存所有的工作结果；
- 允许用户以妥善的形式退出程序。

### 7.1 处理错误

#### 7.1.1 异常分类

在 Java 中，异常对象都是派生于 Trhowable 类的一个实例。

下图为 Java 异常层次结构的一个简化示意图

![](http://images.csmaxwell.xyz/20200422215353.png)

所有异常都是由 Throwable 继承而来，但是下一层又分为 Error 和 Exception。

Error 类描述了 Java 运行时系统的内部错误和资源耗尽错误。系统不应该抛出这种类型的异常，这种情况很少出现。

Exception 这个层次结构又分为了两个分支：一个分支派生于 RuntimeException；另一个分支包含其他异常。

划分两个分支的规则是：由程序错误导致的异常属于 RuntimeException；而程序本身没有问题，但由于 I/O 错误，这类问题属于其他异常。

两种异常分支的几种情况：

| RuntimeException | 其他异常 (非Runtime)                   |
| ---------------- | -------------------------------------- |
| 错误的类型转换   | 试图在文件尾部后面读取数据             |
| 数组访问越界     | 试图打开一个不存在的文件               |
| 访问 null 指针   | 根据字符串查找对象，但是这个类并不存在 |

**“如果出现 RuntimeException 异常，那么就一定是你的问题” 是一条相当有道理的规则。**

Java将派生于 Error 类或 RuntimeException 类的所有异常称为非受查（unchecked）异常，其他的异常称为受查（checked）异常。编译器将核查是否为所有的受查异常提供了异常处理器。

#### 7.1.2 声明受查异常

在 Java 中，如果我们遇到需要抛出异常的地方，需要告诉 Java 抛出的异常的类型。

可以在方法上声明可能抛出的异常

```java
public FileInputStream(String name) throws FileNotFoundException {...}
```

通过声明受查异常，在真的遇到异常情况时，就会搜索异常处理器，进行处理。

下面 4 种情况需要使用 throws 子句声明异常：

1）调用一个抛出受查异常的方法

2）程序运行过程中发现错误，并且利用 throw 语句抛出一个受查异常

3）程序出现错误，例如 a[-1] = 0

4）Java 虚拟机和运行时库出现的内部错误

前两种情况，必须告之调用这个方法的程序员有可能抛出异常，如果没有处理器捕获这个异常，当前执行的线程会被结束。

对于这些可能被他人使用的 Java 方法，都应该根据**异常规范**（exception specification），在方法的首部声明这个方法可能抛出的异常，当然一个方法可能抛出多个受查异常，在 throws 子句后，使用逗号进行隔开：

```java
public Image loadImage(String s) throws FileNotFoundException, EOFException {...}
```

对于 Error 和 RuntimeException 的非受查异常，都不需要声明，因为这些错误要么是我们无法控制的要么就是可以避免的。

总之，一个方法必须声明所有可能抛出的受查异常，而非受查异常要么不可控制要么可以避免。如果方法没有声明所有可能发生的受查异常，编译器会收到一个错误消息。

警告：在子类覆盖超类的一个方法，子类方法中声明的异常不能比超类声明的异常更通用。如果超类没有抛出异常，子类也不能抛出异常。

#### 7.1.3 如何抛出异常

当我们在方法上声明了受查异常，在方法中，我们通过 throw 语句抛出：

```java
String readData(Scanner in) throws EOFException {
	...
    while (...) {
        if (!in.hasNext()) // EOF encountered
            if (n < len)
                throw new EOFException(); // 抛出异常
    }
}
```

通过这种方法，一旦方法抛出了异常，这个方法就不可能返回到调用者，也不用担心返回的默认值或错误代码。

#### 7.1.4 创建异常类

在程序中，我们可能会遇到任何标准的异常类都无法充分描述的问题，此时，我们可以创建自己的异常类，只需要定义一个派生于 Exception 的类，或者派生于 Exception 子类的类。例如：

```java
// 定义一个派生于 IOException 的类
class FileFormatException extends IOException {
    public FileFormatException() {}
    public FileFormatException(String gripe) {
        super(gripe);
    }
}
// 可以抛出自己定义的异常
String readData(BufferedReader in) throws FileFormatException {
    while(...) {
        if (ch == -1) {
            if (n < len)
                throw new FileFormatException();
        }
    }
}
```

### 7.2 捕获异常

对于抛出异常，我们只需要将其抛出就不用理睬了，但是有些代码必须捕获异常。

#### 7.2.1 捕获异常

捕获异常，使用 try/catch 语句块，如果在 try 语句块中任何代码抛出了在 catch 子句说明的异常类，都会被捕获并执行相应的错误处理；如果 try 语句块中没有抛出异常，catch 不会触发。

```java
public void read(String fileName) {
    try {
    	InputStream in  = new FileInputStream(fileName);
        int b;
        while ((b = in.read()) != -1)
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

上面的代码，读取并处理字节，直到遇到文件结束符结束，在我们调用这个 read 方法，也有可能抛出一个 IOException 异常，被 catch 捕获，并生成一个栈轨迹。

通常，最好的选择是什么都不做，将异常传递给调用者，让调用者去处理这个异常，采用这种方式，就需要声明这个方法可能会抛出异常

```java
public void read(String fileName) throws IOException {
    InputStream in = new FileInputStream(fileName);
    int b;
    while ((b = in.read()) != -1) {
        ...
    }
} 
```

如果调用了一个抛出受查异常的方法，要么对处理异常，要么将异常继续传递出去。

**通过，应该捕获那些知道如何处理的异常，而将那些不知道怎么处理的异常继续进行传递。**

#### 7.2.2 捕获多个异常

在 try/catch 语句块中，可以通过多个 catch 语句块捕获多个异常

```java
try {
    ...
} catch (FileNotFoundException e) {
    ...
} catch (IOException e) {
    ...
}
```

使用 e.getMessage() 与 e.getClass().getName() 可以获得对象的更多信息。

注：同一个 catch 子句可以捕获多个异常类型。

#### 7.2.3 再次抛出异常和异常链

在 catch 子句中，还可以抛出一个异常。通过这种方式，可以改变异常的类型。通过捕获这个异常再将它再次抛出，能够更加明确具体的异常定位。

```java
try {
    ...
} catch (SQLException e) {
    throw new ServletException("database error:" + e.getMessage);
}
```

或者可以将原始异常设置为新异常的原因：

```java
try {
    ...
} catch (SQLException e) {
    Throwable se = new ServletException("database error");
    se.initCause(e);
    throw se;
}
```

通过这种方法，可以让用户抛出子系统中的高级异常，而不会丢失原始异常的细节。

如果在一个方法中发生了一个受查异常，而不允许抛出它，利用这种包装技术就可以捕获这个受查异常，并将它包装成一个运行时异常。

当然，也可以只是记录一下，然后直接抛出，不做任何改变。

```java
try {
    ...
} catch (Exception e) {
    logger.log(level, message, e);
    throw e;
}
```

#### 7.2.4 finally 子句

对于在 try 语句块中如果出现了异常，就会跳到 catch 语句中，对于 try 语句块中某些资源，需要进行关闭或回收等操作，通过 finally 子句，对于正常运行与发生异常两种情况，finally 语句都会执行。

```java
InputStream in = new Fi
```

不管是否有异常被捕获，finally 子句中的代码都会被执行。

对于 try/catch 语句中没有捕获的异常，程序会继续执行 try 语句块中的所有代码，直到发生异常或执行完 try 中所有代码，然后执行 finally 子句中的代码。

Try 语句可以只有 finally 子句，而没有 catch 子句。

建议解耦合 try/catch 和 try/finally 语句块，这样可以提供代码的清晰度。

```java
InputStream in = ...;
try {
    try {
        ...
    } finally {
        in.close();
    }
} catch (IOException e) {
    ...
}
```

内层的 try 语句块就是确保关闭输入流，外出的 try 语句块就是确保报告出现的异常。

#### 7.2.5 带资源的 try 语句

带资源的 try 语句的形式：

```java
try (Resource res = ...) {
    work with res
}
```

在 try 块退出时，会自动调用 res.close()。下面是一个读取一个文件中的所有单词：

```java
try {Scanner in = new Scanner(new FileInputStream("/usr/share/dict/words")), "UTF-8"} {
    while (in.hasNext()) {
        System.out.println(in.next);
    }
}
```

这个块正常退出或存在一个异常时，都会调用 in.close() 方法，就像使用了 finally 块一样，也可以指定多个资源，这个块退出后，都会被关闭。

#### 7.2.6 分析堆栈轨迹元素

跳过...

### 7.3 使用异常机制的技巧

1、异常处理不能代替简单的测试

2、不要过分地细化异常

3、利用异常层次结构

4、不要压制异常

5、在检查错误时，苛刻要比放任更好

6、不要羞于传递异常

### 7.4 使用断言

#### 7.4.1 断言的概念

断言是指在测试期间向代码中插入一些检查语句。当代码发布时，这些插入的检测语句会被自动移走。

Java 通过 assert 关键字进行条件检测：

```java
assert 条件;
// or
assert 条件 : 表达式;
```

上面的两种形式都会对条件进行检测，结果为 false，则会抛出一个 AssertionError 异常。第二种形式，表达式会被传入 AssertionError 的构造器，并转换为一个消息字符串。

例如，我想判断 x 是一个非负数，就可以这么使用断言：

```java
assert x >= 0;
// 或者将 x 的实际值传递给 AssertionError 对象
assert x >= 0 : x;
```

#### 7.4.2 启用和禁用断言

默认情况下，断言会被禁用。可以在运行程序时用 -enableassertions 或 -ea 选项启用：

```java
java -enableassertions MyApp
```

在启用或禁用断言是不必重新编译程序，启用或禁用断言是类加载器的功能。

也可以对某个类或整个包使用断言：

```java
java -ea:MyClass -ea:com.company.mylib...MyApp
```

使用 -disableassertions 或 -da 禁用某个类或 包的断言。

#### 7.4.3 使用断言完成参数检测

在 Java 中给了3种处理系统错误的机制：

- 抛出一个异常
- 日志
- 使用断言

该什么时候使用断言？请记住下面几点：

- 断言失败是致命的、不可恢复的错误。
- 断言检测只用于开发和测试阶段（这种做法被戏称为 “在靠近海岸时穿上救生衣，但在海中央就把救生衣抛掉吧”）。

因此，不应该使用断言向程序的其他部分通告发生了可恢复的错误，或者，不应该作为程序向用户通告问题的手短。断言只应该用于测试阶段确定程序内部的错误位置。

### 7.5 记录日志

每个 Java 程序员都很熟悉在有问题的代码中插入一些 System.out.println 方法来查看一些信息，帮助我们发现问题。当然，一旦发现问题的根源，就要把这些语句从代码中删除。实际上，我们可以通过记录日志来实现通用的功能，通过记录日志的API，我们可以把输出信息放在日志中，下面是使用这些API的优点：

- 可以很容易地取消全部日志记录，或者仅仅取消某个级别的日志，而且打开和关闭这个操作也很容易。
- 可以很简单地禁用日志记录的输出，因此，将这些日志代码留在程序中的开销很小
- 日志记录可以被定向到不同的处理器，用于在控制台中显示，用于存储在文件中等。
- 日志记录器和处理器都可以对记录进行过滤。过滤器可以根据过滤丢弃哪些无用的记录项。
- 日志记录可以采用不同的方式格式化，例如，纯文本或XML。
- 应用程序可以使用多个日志记录器，他们使用类似包名的这种具有层次结构的名字
- 默认情况下，日志系统的配置有配置文件控制。可以自己替换这个配置。

#### 7.5.1 基本日志

生成简单的日志记录，可以使用全局日志记录器（global logger）并调用其 info 方法：

```java
Logger.getGlobal().info("File->Open menu item selected");
```

#### 7.5.2 高级日志

在一个应用中，不要将所有的日志都记录到一个全局日志记录器中，可以自定义日志记录器。可以调用 getLogger 方法创建或获取记录器：

```java
private static final Logger myLogger = Logger.getLogger("com.company.myapp");
```

注：未被任何变量引用的日志记录器可能会被垃圾回收，为了避免这种情况发生，可以使用一个静态变量存储日志记录器的一个引用。

日志记录器分为7个级别：

- SEVERE
- WARNING
- INFO
- CONFIG
- FINE
- FINER
- FINEST

默认情况，只记录前三个级别，也可以设置其他的级别。例如：

```java
logger.setLevel(level.FINE);
```

记录日志的常用用途是记录哪些不可预料的异常，可以使用下面两个方法提供日志记录中包含的异常描述内容。

```java
void throwing(String className, String methodName, Throwable t);
void log(Level l, String message, Throwable t);

// 方法一
if (...) {
    IOException exception = new IOException("...");
    logger.throwing("com.company.mylib.Reader", "read", exception);
    throw exception;
}
// 方法二
try {
    ...
} catch (IOException e) {
    Logger.getLogger("com.company.myapp").log(Level.WARNING, "Reading", e);
}
```

#### 7.5.3 本地化

本地化的应用程序包含资源包中的本地特定信息，资源包由各个地区的映射集合组成。

一个程序可以包含多个资源包，每个资源包都有一个名字，要想将映射添加到一个资源包中，需要为每个地区创建一个文件。英文消息映射位于 com/company/logmessages_en.properties 文件中；德语位于 com/company/logmessages_de.properties 文件中。可以将这些文件与类文件放在一起，以便 ResourceBundle 类自动地对它们进行定位。

#### 7.5.4 日志记录说明

为一个简单的应用程序，选择一个日志记录器，通过调用下列方法得到日志记录器。

```java
Logger logger = Logger.getLogger("com.company.myprog");
// or
private static final Logger logger = Logger.getLogger("com.company.myprog");
```

默认的日志配置将级别等于或高于 INFO 级别的所有消息记录到控制台，用户可以覆盖默认的配置文件。

### 7.6 调试技巧

1）可以用下面的方法打印或几率任何变量的值

```java
System.out.println("x = " + x);
// or
Logger.getGlobal().info("x = " + x);
```

2）可以在类中放置一个单独的 main 方法进行测试

3）可以使用 JUnit 进行单元测试等。

4）日志代理（logging proxy）是一个子类的对象，它可以截获方法调用，并进行日志记录，然后调用超类的方法。

5）利用 Throwable 类提供的 printStackTrace 方法，可以从任何一个异常对象中获得堆栈情况。

6）-Xlint 选项告诉编译器对一些容易出现的代码问题进行检测。

## 第八章 泛型程序设计

### 8.1 为什么要使用泛型程序设计

泛型程序设计（Generic programming）意味编写的代码可以被不同类型的对象所重用。在 Java 增加泛型类之前有一个 ArrayList 类。下面来研究泛型程序设计的机制是如何演变的。

#### 8.1.1 类型参数的好处

在 Java 中增加泛型类之前，泛型程序设计是继承实现的。ArrayList 类只维护一个 Object 引用的数组：

```java
public class ArrayList {
    private Object[] elementData;
    public Object get(int i) {...}
    public void add(Object o) {...}
}
```

这种方法有两个问题提，当获取一个值时必须进行强制类型转换。

```java
ArrayList files = new ArrayList();
...
String filename = (String) files.get(0);
```

此外，这里没有错误检查，可以向数组列表添加任何类的对象。

泛型提供了一个更好的解决方法：类型参数（type parameters）。ArrayList 类有一个类型参数用来指示元素的类型：

```java
ArrayList<String> files = new ArrayList<>();
```

这使得代码具有更好的可读性。人们一看就知道这个数组列表中包含的 String 对象。

编译器也可以很好地利用这个信息。当调用 get 的时候，不需要进行强制类型转换，编译器就知道返回值为 String，而不是 Object：

```java
String filename = files.get(0);
```

编译器还知道 ArrayList<String> 中 add 方法有一个类型为 String 的参数，编译器可以进行检查，避免插入错误类型的对象。例如：

```java
files.add(new File("...")); // can only add String objects to an ArrayList<String>
```

是无法通过编译的。使用类型参数使程序具有更好的可读性和安全性。

#### 8.1.2 谁想成为泛型程序员

使用像 ArrayList 的泛型类很容易。大多数 Java 程序员都使用 ArrayList<String> 这样的类型，就好像已经构建在语言之中，像 String[] 数组一样。

但是，实现一个泛型类没有那么容易。对于类型参数，使用这段代码的程序员可能想内置所有的类，他们希望在没有过多的限制以及混乱的错误消息的状态下，做所有的事情。因此，一个泛型程序员的任务就是预测出所用的类未来可能有的所有用途。

Java  中有一个具有独创性的新概念，通配符类型（wildcard type），它解决了匹配对象的问题，通过通配符类型，可以让库的构建者编写除尽可能灵活的方法。

### 8.2 定义简单泛型类

一个泛型类（generic class）就是具有一个或多个类型变量的类。下面使用一个简单的 Pair 类来进行说明

```java
public class Pair<T> {
    private T first;
    private T second;
    
    public Pair() {
        first = null;
        second = null;
    }
    
    public Pair(T first, T second) {
        this.first = first;
        this.second = second;
    }
    
    public T getFirst() { return first; }
    public T getSecond() { return second; }
    
    public void setFirst(T newValue) { first = newValue; }
    public void setSecond(T newValue) { second = newValue; }
}
```

上面的 Pair 类引入了一个类型变量 T，用尖括号括起来，并放在类名后面。泛型类可以有多个类型变量。例如，可以定义 Pair 类，其中第一个域和第二个域使用不同的类型：

```java
public class Pair<T, U> {...}
```

类定义中的类型变量指定方法的返回类型以及域和局部变量的类型。例如：

```java
private T first;
```

注：类型变量使用大写形式，且比较短。在 Java 中使用变量 E 表示集合的元素类型，K 和 V 分别表示表的关键字与值的类型。T、U、S 都可以表示任意类型。

用具体的类型替换类型变量就可以实例化泛型类型，例如：

```java
Pair<String>
Pair<String>();
// 方法
String getFirst();
void setFirst(String);
```

### 8.3 泛型方法

除了定义泛型类，还可以使用类型参数定义泛型方法。

```java
class ArrayAlg {
    public static <T> T getMiddle(T a) {
        return a[a.length / 2];
    }
}
```

泛型方法可以定义在普通类，也可以定义在泛型类中。

当调用一个泛型方法时，在方法名前的尖括号中放入具体的类型：

```java
String middle = ArrayAlg.<String>getMiddle("John", "Q", "Public");
```

在这种情况下，方法调用中可以省略<String> 参数类型，编译器可以推断出所调用的方法，它用 names 类型（即 String[]）与泛型类型 T[] 进行匹配并推断出 T 一定是 String。也就是说，可以调用：

```java
String middle = ArrayAlg.getMiddle("John", "Q", "public");
```

### 8.4 类型变量的限定

有时，类或方法需要对类型变量加以约束。下面是一个经典的例子，我们要计算数组中的最小元素：

```java
class ArrayAlg {
    public static <T> T min(T[] a) {
        if (a == null || a.length == 0) {
            T smallest = a[0];
            for(int i = 1; i < a.length; i++) {
                if (smallest.compareTo(a[i]) > 0) {
                    smallest = a[i];
                }
            }
            return smallest;
        }
    }
}
```

上面的代码中，变量 smallest 类型为 T，这意味着它可以是任何一个类的对象。怎么确保 T 所属的类有 compareTo 方法呢？

解决这个问题的方案就是将 T 限制为实现了 Comparable 接口（只含一个方法 compareTo 的标准接口）的类。可以通过对类型变量 T 设置限定 (bound) 实现这一点：

```java
public static <T extends Comparable> T min(T[] a) ...
```

实际上 Comparable 接口本身就是一个泛型类型。

现在，泛型的 min 方法只能实现了 Comparable 接口的类（如 String、LocalDate 等）的数组调用。

一个类型变量或通配符可以有多个限定，例如：

```java
T extends Comparable & Serializable
```

限定符用 & 分隔，而逗号用来分隔类型变量。

下面是一个泛型方法 minmax，这个方法计算泛型数组的最小值和最大值，并返回 Pair<T> ，并且限制了为 Comparable 接口的类。

```java
public class Pair2Test2 {
    public static void main(String[] args) {
        LocalDate[] birthdays = {
                LocalDate.of(1998, 3, 31),
                LocalDate.of(1815, 12, 10),
                LocalDate.of(1903, 12, 3),
        };
        Pair<LocalDate> mm = ArrayAlg.minmax(birthdays);
        System.out.println("min = " + mm.getFirst());
        System.out.println("max = " + mm.getSecond());
    }
}

class ArrayAlg {
    public static <T extends Comparable> Pair<T> minmax(T[] a) {
        if (a == null || a.length == 0) {
            return null;
        }
        T min = a[0];
        T max = a[0];
        for (int i = 0; i < a.length; i++) {
            if (min.compareTo(a[i]) > 0) {
                min = a[i];
            }
            if (max.compareTo(a[i]) < 0) {
                max = a[i];
            }
        }
        return new Pair<>(min, max);
    }
}
```

### 8.5 泛型代码和虚拟机

虚拟机没有泛型类型对象——所有对象都属于普通类。

#### 8.5.1 类型擦除

无论何时定义一个泛型类型，都自动提供了一个相应的原始类型（raw type）。原始类型的名字就是删除类型参数后的泛型类型名。擦除（erased）类型变量，并替换为限定类型（无限定的吧变量用 Object）。

例如，Pair<T>的原始类型如下所示：

```java
public class Pair {
    private Object first;
    private Object second;
    
    ...
}
```

因为 T 是一个无限定的变量，所有直接用 Object 替换。

#### 8.5.2 翻译泛型表达式

当程序调用泛型方法时，如果擦除返回类型，编译器插入强制类型转换。例如，下面这个语句序列：

```java
Pair<Employee> buddies = ...;
Employee buddy = buddies.getFirst();
```

擦除 getFirst 的返回类型后将返回 Object 类型。编译器自动插入 Employee 的强制类型转换。也就是说，编译器把这个方法调用翻译为两条虚拟机指令：

- 对原始方法 Pair.getFirst 的调用
- 对返回的 Object 类型强制转换为 Employee 类型。

#### 8.5.3 翻译泛型方法

类型擦除也会出现在泛型方法中。程序员通常认为下述的泛型方法

```java
public static <T extends Comparable> T min(T[] a)
```

是一个完整的方法族，而擦除类型之后，只剩下一个方法：

```java
public static Comparable min(Comparable[] a)
```

注意，类型参数 T 已经被擦除了，只留下了限定类型 Comparable。

方法的擦除带来了两个复杂问题。看一看下面这个示例：

```java
class DateInterval extends Pair<LocalDate> {
    public void setSecond(LocalDate second) {
        if (second.compareTo(getFirst()) >= 0) {
            super.setSecond(second);
            ...
        }
    }
}
```

一个日期区间是一对 LocalDate 对象，并且需要覆盖这个方法来确保第二个值永远不小于第一个值。这个类擦除后变成

```java
class DateInterval extends Pair {
    public void setSecond(LocalDate second) {
        ...
    }
}
```

这里存在另一个从 Pair 继承的 setSecond 方法，这显然是一个不同的方法，因为它有一个不同类型的参数——Object，而不是 LocalDate。

总之，需要记住有关 Java 泛型转换的事实：

- 虚拟机中没有泛型，只有普通的类和方法。
- 所有的类型参数都用它们的限定类型替换
- 桥方法被合成来保持多态
- 为保持类型安全性，必要时插入强制类型转换。

### 8.6 约束与局限性

#### 8.6.1 不能用基本类型实例化类型参数

不能用类型参数代替基本类型。因此，没有 Pair<double>，只有 Pair<Double>。当然，其原因是类型擦除。

擦除后，Pair 类含有 Object 类型的域，而 Object 不能存储 double 值。

这是因为 Java 中基本类型的状态独立。

#### 8.6.2 运行时类型查询只适用于原始类型

虚拟机中的对象总有一个特定的非泛型类型。因此，所有的类型查询只产生原始类型。例如：

```java
if (a instanceof Pair<String>) // Error
if (a instanceof Pair<T>) // Error
```

当试图查询一个对象是否属于某个泛型类型时，倘若使用 instanceof 会得到一个编译器错误，如果使用强制类型转换会得到一个警告。

同样，使用 getClass 方法总是返回原始类型。例如：

```java
Pair<String stringPair = ...;
Pair<Employee> employeePair = ...;
if (stringPair.getClass() == employeePair.getClass()) // equal
```

比较的结果为 true，这是因为两次调用 getClass 都将返回 Pair.class。

#### 8.6.3 不能创建参数化类型的数组

不能实例化参数化类型的数组，例如：

```java
Pair<String>[] table = new Pair<String>[10]; //Error
```

这是因为在类型擦除后，table 的类型是 Pair[]，可以把它转换为 Object[]。

需要说明的是，只是不允许创建这些数组，而声明类型为 Pair<String>[] 的变量仍是合法的，不过不能用 new Pair<String>[10] 初始化这个变量。不过不推荐这么使用，这是不安全的。

如果需要收集参数化类型对象，推荐使用 ArrayList:ArrayList<Pair<String>>。

#### 8.6.4 不能实例化类型变量

不能使用像 new T(...)，new T[...] 或 T.class 这样的表达式中的类型变量。例如，下面的 Pair<T> 构造器就是非法的：

```java
public Pair() { // Error
    first = new T();
    second = new T();
}
```

类型擦除会将 T 改变为 Object。

在 Java SE 8 之后最好的解决办法是让调用者提供一个构造器表达式。例如：

```java
Pair<String> p = Pair.makePair(String::new);
```

makePair 方法接收一个 Supplier<T>，这是一个函数式接口，表示一个无参数而且返回值为 T 的函数：

```java
public static <T> Pair<T> makePair(Supplier<T> constr) {
    return new Pair<>(constr.get(), constr.get());
}
```

#### 8.6.5 不能构造泛型数组

就像不能实例化一个泛型实例一样，也并不能实例化数组。因为数组会填充 null 值，构造时看上去是安全的。不过，数组本身也有类型，用来监控存储在虚拟机中的数组。这个类型会被擦除。例如：

```java
public static <T extends Comparable> T[] minmax(T[] a) { // Error
    T[] mm = new T[2];
    ...
}
```

类型擦除会让这个方法永远构造 Comparable[2]数组。

如果一个数组仅仅作为一个类的私有实例域，就可以将这个数组声明为 Object[]，并且在获取元素时进行类型转换。

#### 8.6.6 泛型类的静态上下文中类型变量无效

不能在静态域或方法中引用类型变量。例如，下面高招将无法施展：

```java
public class Singleton<T> {
    private static T singleInstance; // Error
    
    public static T getSingleInstance() { // Error
        if (singleInstance == null) {
            return singleInstance;
        }
    }
}
```

如果这个程序能够运行，就可以声明一个 `Singleton<Random>` 共享随机数生成器，声明一个 `Singleton<JFileChooser>` 共享文件选择器对话框。但是，这个程序无法工作。类型擦除后，只剩下 `Singleton`类，它只包含一个 `singleInstance`域。因此，禁止使用带有类型变量的静态域和方法。

#### 8.6.7 不能抛出或捕获泛型类的实例

既不能抛出也不能捕获泛型类对象。实际上，甚至泛型类扩展 `Throwable` 都是不合法的。例如，以下定义就不能正常编译：

```java
public class Problem<T> extends Exception {...} // Error 
```

catch子句也不能使用类型变量

```java
public static<T extends Throwable> void doWork(Class<T> t) {
    try {
        ...
    } catch (T e) { // Error
        Logger.global.info(...)
    }
}
```

### 8.7 泛型类型的继承规则

在使用泛型类时，需要了解一些有关继承和子类型的准则。考虑一个类和一个子类，如 Employee 和 Manager。

`Pair<Manager>` 是 `Pair<Employee>` 的一个子类吗？答案是“不是”。例如下面的代码就不能编译成功：

```java
Manager[] topHonchos = ...;
Pair<Employee> result = ArrayAlg.minmax(topHonchos); // Error
```

`minmax` 方法返回 `Pair<Manager>`，而不是 `Pair<Employee>`，并且这样的赋值也不合法。

无论 S 与 T 有什么联系，如下图一样，通常，`Pair<S>` 与 `Pair<T>` 没有什么联系。

![](http://images.csmaxwell.xyz/20200428203009.png)

注：必须注意泛型与 Java 数组之间的重要区别。可以将一个 Manager[] 数组赋值给一个类型为 Employee[] 的变量：

```java
Manager[] managerBuddies = { ceo, cfo };
Employee[] employeeBuddies = managerBuddies; // OK
```

然而，数组带有特别的保护。如果视图将一个低级别的雇员存储到 employeeBuddies[0]，虚拟机将会抛出 ArrayStoreException 异常。

泛型类可以扩展或实现其他的泛型类。例如，`ArrayList<T>` 类可以实现 `List<T>` 接口。这意味着，一个 `ArrayList<Manager>` 可以转换为一个 `List<Manager>`。但是，一个 `ArrayList<Manager>` 不是一个 `ArrayList<Employee>` 或 `List<Employee>`。

![](http://images.csmaxwell.xyz/20200428203834.png)

### 8.8 通配符

#### 8.8.1 通配符概念

通配符类型中，允许类型参数变化。例如，通配符类型

```java
Pair<? extends Employee>
```

表示任何泛型 Pair 类型，它的类型参数是 Employee 的子类，可以为 `Pair<Manager>`，但不能为 `Pair<String>`。

假设要编写一个打印雇员的方法：

```java
public static void printBuddies(Pair<Employee> p)
```

上面的方法不能接受 `Pair<Manager>`。如果使用通配符类型就可以接收它们：

```java
public static void printBuddies(Pair<? extends Employee> p)
```

但是，这里有一个问题：

```java
Pair<Manager> managerBuddies = new Pair<>(ceo, cfo);
Pair<? extends Employee> wildcardBuddies = managerBuddies; // OK
wildcardBuddies.setFirst(lowlyEmployee); // compile-time error
```

这里对 `setFirst` 的调用有一个类型错误，因为编译器不清楚是那个 Employee 的子类型，它拒绝传递任何特定的类型，因为不能用来匹配。

可以使用有限定的通配符来解决这个问题。

#### 8.8.2 通配符的超类型限定

通配符限定于类型变量限定十分类似，但是，通配符限定可以指定一个超类型限定（supertype bound）：

```java
? super Manager
```

这个通配符限制为 `Manager`的所有超类型。

这么做，可以为方法提供参数，但不能使用返回值。例如，`Pair<? super Manager>` 有方法

```java
void setFirst(? super Manager)
? super Manager getFirst()
```

因此调用这个方法时，只能传递 manager 类型的对象。

![](http://images.csmaxwell.xyz/20200428210029.png)

## 第九章 集合

### 9.1 Java集合框架

#### 9.1.1 将集合的接口与实现分离

与现代的数据结构类库的常见情况一样，Java 集合类库也将接口与实现分离。

下面已——队列（queue）是如何分离的。

队列接口指出可以在队列的尾部添加元素，在队列的头部删除元素，并且可以查找队列中元素的个数。当需要收集对象，并按照“先进先出”的规则检索对象时就应该使用队列

![](http://images.csmaxwell.xyz/20200428211250.png)

队列接口的最简形式类似下面这样：

```java
public interface Queue<E> {
    void add(E element);
    E remove();
    int size();
}
```

这个接口并没有说明队列是如何实现的。队列通常有两种实现方式：一种是使用循环数组；另一种是使用链表

![](http://images.csmaxwell.xyz/20200428211456.png)

每一个实现都可以通过一个实现了 Queue 接口的类来表示

```java
public class CircularArrayQueue<E> implements Queue<E> {
    private int head;
    private int tail;
    
    CircularArrayQueue(int capacity) {...}
    public void add(E element) {...}
    public E remove() {...}
    public int size() {...}
    private E[] elements;
}

public class LinkedListQueue<E> implements Queue<E> {
    private Link head;
    private Link tail;
    
    LinkedListQueue() {...}
    public void add(E element);
    public E remove() {...}
    public int size() {...}
}
```

在程序中使用队列时，可以使用接口类型来存放集合的引用，需要更改另外一种实现时，只需要更改构造器的可以了。

```java
Queue<Customer> expressLane = new CircularArrayQueue<>(100);
// Queue<Customer> expressLane = new LinkedListQueue<>();
expressLane.add(new Customer("Harry"));
```

#### 9.1.2 Collection 接口

在 Java 类库中，集合类的基本接口是 Collection 接口。这个接口有两个基本方法：

```java
public interface Collection<E> {
    boolean add(E element);
    Iterator<E> iterator();
    ...
}
```

`add` 方法用于向集合中添加元素。如果添加元素确实改变了集合就返回 true，如果集合没有发生变化就返回 false。

`iterator` 方法用于返回一个实现了 Iterator 接口的对象。可以使用这个迭代对象依次访问集合中的元素。

#### 9.1.3 迭代器

Iterator 接口包含 4 个方法：

```java
public interface Interator<E> {
    E next();
    boolean hasNext();
    void remove();
    default void forEachRemaining(Consumer<? super E> action);
}
```

通过反复调用 next 方法，可以逐个访问集合中的每个元素，如果到达了集合的末尾，next 方法会抛出一个 `NoSuchElementException` 的异常。因此在调用 next 之前调用 hasNext 方法进行检测，如果还有可访问元素，则返回 true。

如果想要查看集合中所有元素，可以使用循环反复调用 next 方法，或者使用 foreach

```java
// 循环
Collection<String> c = ...;
Iterator<String> iter = c.iterator();
while (iter.hasNext()) {
    String element = iter.next();
    ...
}
// foreach
for (String element : c) {
    ...
}
```

`for each` 循环可以与任何实现了 Iterable 接口的对象一起工作，而 Collection 接口扩展了 Iterable 接口，所有标准类库中的任何集合都可以是 `for each` 循环。

在 Java SE 8 中，还可以调用 forEachRemaining 方法，它提供了一个 lambda 表达式。将对迭代器的每个元素调用这个 lambda 表达式，直到没有元素为止。

```java
iterator.forEachRemaining(element -> do something with element);
```

元素访问的顺序取决于集合类型，例如，ArrayList，迭代器从索引0开始，每次索引值加1；如果是 HashSet，则每个元素都将按随机次序出现，直到遍历所有元素。

Java 集合类库中的迭代器与其他类库的迭代器有很重要的区别。

| 传统类库迭代器                                   | Java类库迭代器                                               |
| ------------------------------------------------ | ------------------------------------------------------------ |
| 迭代器根据数组索引建模，根据索引可以找到指定元素 | 查找与位置变更是相连的，查找只能使用 next 方法               |
| 迭代器位置就在索引值得数组元素上 a[i]            | 迭代器位于两个元素之间，next 越过下一个元素，并返回刚才越过的元素 |

![](http://images.csmaxwell.xyz/20200428222323.png)

Iterator 接口的 remove 方法会删除上次调用 next 方法返回的元素。在 remove 方法之前，如果没有调用过 next 将会抛出一个 `IllegalStateException` 异常。

#### 9.1.4 泛型实用方法

由于 Collection 与 Iterator 都是泛型接口，可以编写操作任何集合类型的实用方法。

在 Collection 接口声明很多很有用的方法：

| 方法                                          | 说明                                                         |
| --------------------------------------------- | ------------------------------------------------------------ |
| Iterator<E> iterator()                        | 返回一个用于访问集合中每个元素的迭代器                       |
| int size()                                    | 返回当前存储在集合中的元素个数                               |
| boolean isEmpty()                             | 如果集合中没有元素，返回 true                                |
| boolean contains(Object obj)                  | 如果集合中包含了一个与obj相等的对象，返回true                |
| boolean containsAll(Collection<?> other)      | 如果这个集合包含 other 集合中的所有元素，返回true            |
| boolean add(Object element)                   | 将一个元素添加到集合中，如果这个调用改变了集合，返回true     |
| boolean addAll(Collection<? extends E> other) | 将other集合中的所有元素添加到这个集合，如果这个调用改变了集合，返回true |
| boolean remove(Object obj)                    | 从这个集合中删除等于 obj 的对象，如果有匹配的对象将被删除，返回 true |
| Object[] toArray()                            | 返回这个集合的对象数组                                       |

#### 9.1.5 集合框架中的接口

Java 集合框架为不同类型的集合定义了大量的接口。

![](http://images.csmaxwell.xyz/20200428230713.png)

集合有两个基本接口：`Collection` 和 `Map`。

集合插入元素使用 `boolean add(E element)`

映射因为包含键/值对，所有要用 put 方法插入 `V put(K key, V value)`

读取元素，可以使用迭代器访问，读取值则使用 get 方法 `V get(K key)`

| 接口  |                                                 |
| ----- | ----------------------------------------------- |
| List  | 有序集合，迭代器访问，索引访问                  |
| Set   | 不能增加重复的元素                              |
| Queue | 先进先出，只能在队尾插入                        |
| Map   | 每个对象指定一个key，通过key可以快速定位到value |

### 9.2 具体的集合

下面列举了 Java 类库中的集合，除了 Map 结尾的类之外，其他类都实现了 Collection 接口，Map 结尾的类实现了 Map 接口。

| 集合类型        | 描述                                                 |
| --------------- | ---------------------------------------------------- |
| ArrayList       | 一种可以动态增长和缩减的索引序列                     |
| LinkedList      | 一种可以在任何位置进行高效地插入和删除操作的有序序列 |
| ArrayDeque      | 一种用循环数组实现的双端队列                         |
| HashSet         | 一种没有重复元素的无序集合                           |
| TreeSet         | 一种有序集                                           |
| EnumSet         | 一种包含枚举类型值的集                               |
| LinkedHashSet   | 一种可以记住元素插入次序的集                         |
| PriorityQueue   | 一种允许高效删除最小元素的集合                       |
| HashMap         | 一种存储键 / 值关联的数据结构                        |
| TreeMap         | 一种键值有序排列的映射表                             |
| EnumMap         | 一种键值属于枚举类型的映射表                         |
| LinkedHashMap   | 一种可以基础键 / 值项添加次序的映射表                |
| WeakHashMap     | 一种其值无用武之地后可以被垃圾回收器回收的映射表     |
| IdentityHashMap | 一种用 == 而不是用 equals 比较键值的映射表           |

![](http://images.csmaxwell.xyz/20200429152917.png)

![](http://images.csmaxwell.xyz/20200429152948.png)

#### 9.2.1 链表

在我们使用数组或动态的 ArrayList 类的时候，会发现数组与数组列表，在进行删除或插入的操作时，其后的元素的位置都会发生改变，十分不便。

而链表则解决了这个问题，链表将每个对象都存放在独立的结点中，每个结点还存放着下一个结点的引用。在 Java 中，所有链表都是双向链表（doubly linked）——即每个结点还存放着指向前驱结点的引用

![](http://images.csmaxwell.xyz/20200429154524.png)

链表的插入与删除非常的方便，只需要更改插入或删除附近的链接。

![](http://images.csmaxwell.xyz/20200429154659.png)

在 Java 中提供了一个 LinkedList，来实现链表的操作。

```java
List<String> staff = new LinkedList<>();
staff.add("Amy");
staff.add("Bob");
staff.add("Carl");
Iterator iter =  staff.iterator();
String first = iter.next();
String second = iter.next();
iter.remove();
```

上面的代码创建了一个 LinkedList 的链表，并添加了3个元素，接着删除了第2个元素。

链表与泛型集合之间有一个重要的区别。链表是一个有序集合，每个对象的位置十分重要。`LinkedList.add` 方法将对象添加到链表的尾部。但是，常常需要将元素添加到链表的中间。由于迭代器是描述集合中位置的，所有这种依赖于位置的 add 方法将由迭代器负责。只有对自然有序的集合使用迭代器添加元素才有实际意义。例如，集（set）类型，其中的元素完全无序。因此，在 Iterator 接口中就没有 add 方法。相反地，集合类库提供了子接口 ListIterator，其中包含 add 方法：

```java
interface ListIterator<E> extends Iterator<E> {
    void add(E element);
    E previous();
    boolean hasPrevious();
}
```

ListIterator 接口还提供了两个方法，用来反向遍历链表。

LinkedList 类的 listIterator 方法返回一个实现了 ListIterator 接口的迭代器对象。

```java
ListIterator<String> iter = staff.listIterator();
```

下面为，越过链表第一个元素，插入一个元素的代码：

```java
List<String> staff = new LinkedList<>();
staff.add("Amy");
staff.add("Bob");
staff.add("Carl");
ListIterator<String> iter = staff.listIterator();
iter.next();
iter.add("Juliet");
```

最后需要说明，set 方法用一个新元素取代调用 next 或 previous 方法返回的上一个元素。例如，下面的代码将用一个新值替代链表的第一个元素：

```java
ListIterator<String> iter = list.listIterator();
String oldValue = iter.next();
iter.set(newValue);
```

使用链表就是为了尽可能减少在列表中间插入或删除元素所付出的代价。

如果需要对集合进行随机访问，就使用数组或 ArrayList。

下面这个程序创建了两个链表，并将它们合并在一起，然后从第二个链表中每间隔一个元素删除一个元素，最后测试 removeAll 方法：

```java
public class LinkedListTest {
    public static void main(String[] args) {
        List<String> a = new LinkedList<>();
        a.add("Amy");
        a.add("Carl");
        a.add("Erica");

        List<String> b = new LinkedList<>();
        b.add("Bob");
        b.add("Doug");
        b.add("Frances");
        b.add("Gloria");

        ListIterator<String> aIter = a.listIterator();
        Iterator<String> bIter = b.iterator();

        while (bIter.hasNext()) {
            if (aIter.hasNext()) {
                aIter.next();
            }
            aIter.add(bIter.next());
        }

        System.out.println(a);

        bIter = b.iterator();
        while (bIter.hasNext()) {
            bIter.next();
            if (bIter.hasNext()) {
                bIter.next();
                bIter.remove();
            }
        }

        System.out.println(b);

        a.removeAll(b);

        System.out.println(a);
    }
}
```

#### 9.2.2 数组列表

上一节，介绍了 List 接口和实现了这个接口的 LinkedList 类。List 接口用于描述一个有序集合，并且集合中每个元素的位置十分重要。有两种访问元素的协议：一种使用迭代器，另外一种使用 get 和 set 方法随机地访问每个元素。后者不适用于链表，但对数组却很有用。集合类库提供了一种大家熟悉的 ArrayList 类，这个类也实现了 List 接口。 ArrayList 封装了一个动态再分配的对象数组。

注：对一个经验丰富的 Java 程序员来说，在需要动态数组时，可能会使用 Vector 类。为什么要用 ArrayList 取代 Vector 呢？原因很简单：Vector 类的所有方法都是同步的。可以由两个线程安全地访问一个 Vector 对象。但是，如果由一个线程访问 Vector，代码要在同步操作上耗费大量的时间。而 ArrayList 方法不是同步的，因此，建议在不需要同步时使用 ArrayList，而不要使用 Vector。

#### 9.2.3 散列集

散列表（hassh  table）是一种可以快速查找所需要的对象的数据结构。它为每个对象计算一个称为散列码（hash code）的整数。散列码是由对象的实例域产生的一个整数，不同的数据域的对象会产生不同的散列码，散列码都是由 String 类的 hashCode 方法产生的。

如果自定义类，就需要实现这个类的 hashCode 方法。自己实现的 hashCode 方法与 equals 方法应该兼容，即 a.equals(b) 为 true，则 a 与 b 必须具有相同的散列码。

在 Java 中，散列表用链表数组实现。每个列表被称为桶（bucket）。可以这么理解，我们将桶号理解为数组的索引，桶号决定了我们的键存在散列表中的那个桶。要想查找表中对象的位置，就要先计算它的散列码，然后与桶的总数取余，得到的结果就是保存在这个元素的桶的索引。例如，某个对象的散列码为76268，并且有128个桶，对象应该保存在第108号桶中（76268 / 128 余 108）。如果这个桶中没有其他元素，此时将这个元素直接插入桶中就可以了。如果桶中有键了，则将元素的键放在后面，以此类推，直到桶被占满的情况。这种现象称为散列冲突（hash collision）。这时，需要用新对象与桶中所有对象进行比较，查看这个对象是否已经存在。

注：在 Java SE 8 中，桶满时会从链表变成平衡二叉树。如果选择的散列函数不当，会产生很多冲突。

一般制定初始的桶数，为预计元素的75%~150% 左右，标准库使用的桶数是2的幂，默认值为16。

如果遇到散列表太满，则需要**再散列**（rehashed），创建一个桶数更多的表，将所有元素插入到这个新表中，然后丢弃原来的表。**装填因子**（load factor）决定何时对散列表进行再散列，一般装填因子默认为 0.75，当表中超过 75% 的位置已经填入元素，这个表就会用双倍的桶数自动地进行再散列。

散列表可以用于实现几个重要的数据结构，其中最简单的是 set 类型。set 是没有重复元素的元素集合。set 的 add方法首先在集中查找要添加的对象，如果不存在，就讲这个对象添加进去。

Java 集合类库中提供了一个 HashSet 类，它实现了基于散列表的集。用 add 方法添加元素。contains 方法已经被重新定义，用来快速查看是否某个元素已经出现在集中。它只在某个桶中查找元素，而不必查看集合中的所有元素。

散列集迭代器将依次访问所有的桶。由于散列将元素分散在表的各个位置上，所有访问它们的顺序几乎是随机的。只有不关心集合中元素的顺序时，才应该使用 HashSet。

#### 9.2.4 树集

`TreeSet` 类与散列集十分类似，不过，它比散列集有所改进。树集是一个有序集合。可以以任何顺序将元素插入到集合中。对集合进行遍历，每个值将自动按照排序后的顺序出现。

```java
// 插入三个字符串，在访问添加的所有元素
SortedSet<String> sorter = new TreeSet<>();
sorter.add("Bob");
sorter.add("Amy");
sorter.add("Carl");
for (String s : sorter) {
    System.out.println(s);
}

// Amy Bob Carl
```

`TreeSet` 排序是用树结构完成的（当前实现使用的是红黑树），每次将一个元素添加到树中时，都放置在正确的排序位置上。因此，迭代器总是以排好序的顺序访问每个元素。

将一个元素添加到树中要比添加到散列表中慢。

注：要使用树集，必须能够比较元素。这些元素必须实现 Comparable 接口，或者构造集时必须提供一个 Comparator。

树集与散列集对比：

| 树集                 | 散列集                   |
| -------------------- | ------------------------ |
| 元素自动排列         | 元素打乱存放             |
| 元素必须能够比较     | 使用散列函数确定存放位置 |
| 不好确定元素比较类型 | 只需将元素存入即可       |

#### 9.2.5 队列与双端队列

队列是可以让人们有效地在尾部添加一个元素，在头部删除一个元素。

双端队列，则是有两个端口的队列，可以在头部与尾部同时添加或删除元素。

队列不支持在队列中间添加元素。

在 Java SE 6 中引入了 Deque 接口，并由 ArrayDeque 和 LinkedList 类实现。 这两个类都提供了双端队列，而且在必要时可以增加队列的长度。

#### 9.2.6 优先级队列

优先级队列（priority queue）中的元素可以按照任意的顺序插入，却总是按照排序的顺序进行检索。也就是说，无论何时调用 remove 方法，总会获得当前优先级队列中最小的元素。然而，优先级队列并没有对所有的元素进行排序。如果用迭代的方式处理这些元素，并不需要对它们进行排序。优先级队列使用了一个优雅且高效的数据结构，称为堆（heap）。堆是一个可以自我调整的二叉树，对数执行添加 add 和删除 remove 操作，可以让最小的元素移动到根，而不必花费时间对元素进行排序。

与 TreeSet 一样，一个优先级队列既可以保存实现了 Comparable 接口的类对象，也可以保存在构造器中提供的 Comparator 对象。

使用优先级队列的典型示例是任务调度。每一个任务有一个优先级，任务以随机顺序添加到队列中。每当启动一个新的任务时，都将优先级最高的任务从队列中删除（由于习惯上将1设为最高优先级，所有会将最小的元素删除）。

下面的程序是一个正在运行的优先级队列，这里的迭代器不是按照元素的顺序进行访问的。而删除总是删掉剩余元素中优先级最小的那个元素。

```java
public class PriorityQueueTest {
    public static void main(String[] args) {
        PriorityQueue<LocalDate> pq = new PriorityQueue<>();
        pq.add(LocalDate.of(1906, 12, 9));
        pq.add(LocalDate.of(1815, 12, 10));
        pq.add(LocalDate.of(1903, 12, 3));

        System.out.println("Iterating over elements...");
        for (LocalDate localDate : pq) {
            System.out.println(localDate);
        }
        System.out.println("Removing elements...");
        while (!pq.isEmpty()) {
            System.out.println(pq.remove());
        }
    }
}
```

### 9.3 映射

集是一个集合，它可以快速查找现有的元素。但是，要查看一个元素，需要有查找元素的精确副本。通常，我们知道某些键的信息，并想要查找与之对应的元素。映射（map）数据结构 就是为此设计的。映射用来存放键 / 值对。如果提供了键，就能够查找到值。

#### 9.3.1 基本映射操作

Java 类库为映射提供了两个通用的实现：`HashMap` 和 `TreeMap` 这两个类都实现了 Map 接口。

下面对比了 HashMap 与 TreeMap 两种映射类的区别，以及该如何选择

| 散列映射（HashMap）                    | 树映射（TreeMap）                      |
| -------------------------------------- | -------------------------------------- |
| 对键（K）进行散列（hash）              | 用键的整体顺序对元素排序，并组成搜索树 |
| 散列或比较函数只能作用于键，不能用于值 | 没有限制                               |

**如果不需要按照排列顺序访问键，推荐使用 `HashMap`。**

一个简单的 `HashMap`，

```java
Map<String, Employee> staff = new HashMap<>();
Employee harry = new Employee("Harry Hacker");
staff.put("9996", harry);
```

使用 put 方法放置一个键/值，使用 get 方法获取值：

```java
String id = "9996";
e = staff.get(id);
```

如果没有找到相应的键的信息，则 get 将返回 null。

使用 remove 方法从映射中删除给定键的元素。

foreach 加上 lambda 表达式可以轻松的读取映射的每一项。

下面代码演示了对映射的基本操作：

```java
public class MapTest {
    public static void main(String[] args) {
        Map<String, Employee> staff = new HashMap<>();
        staff.put("1", new Employee("Amy Lee"));
        staff.put("2", new Employee("Harry Hacker"));
        staff.put("3", new Employee("Maxwell Zhong"));

        System.out.println(staff);

        staff.remove("3");

        staff.put("3", new Employee("Francesa Miller"));

        System.out.println(staff.get("2"));

        // iterate throught all entries
        staff.forEach((k, v) -> {
            System.out.println("key = " + k + ", value = " + v);
        });
    }
}
```

#### 9.3.2 更新映射项

处理映射还有一个难点就是更新映射项。正常情况下，可以得到与一个键关联的原值，完成更新，再放回更新后的值。不过，必须考虑一个特殊情况，即键第一次出现。例如，使用一个映射统计一个单词在文件中出现的次数，看到一个单词，就使用计数器加1：

```java
counts.put(word, counts.get(word) + 1);
```

当程序第一次 word 时，get 会返回 null。

有三种方法进行补救

```java
// 1. getOrDefault 方法
counts.put(word, counts.getOrDefault(word, 0) + 1);
// 2. putIfAbasent 方法，只有键原先存在时才会放入一个值
counts.putIfAbsent(word, 0);
counts.put(word, counts.get(word) + 1);
// 3. merge 方法
counts.merge(word, 1, Integer::sum);
// 将 word 与 1 关联，否则使用 Integer::sum 函数组合 原值+1
```

#### 9.3.3 弱散列映射

`WeakHashMap` 类是为了解决一个有趣的问题。如果有一个值，对应的键已经不再使用了，将会出现什么情况？假设对某个键的最后一次引用已经消亡，不再有任何途径引用这个值得对象了。由于程序中没有任何地方有这个键，所有无法将它从映射中删除，垃圾回收期也不能删除它，尽管它已经是无用的对象了。

实际上，垃圾回收器跟踪活动的对象。只要映射对象是活动的，其中的桶也是活动的，它们就不能被回收。因此需要有程序负责从长期存活的映射表中删除那些无用的值。或者 `WeakHashMap` 完成这件事情。当对键的唯一引用来自散列条目时，这一数据结构将与垃圾回收器协同工作一起删除键 / 值对。

下面是这种机制的内部运行情况。`WeakHashMap `使用弱引用（weak references）保存键。`WeakReference` 对象将引用保存到另外一个对象中，在这里，就是散列键。对于这种类型的对象，垃圾回收器用一种特有的方式进行处理。通常，如果垃圾回收器发现某个特定的对象已经没有他人引用了，就将其回收。然而，如果某个对象只能由 `WeakReference` 引用，垃圾回收器仍然回收它，但要将引用这个对象的弱引用放入队列中。`WeakHashMap` 将周期性地检查队列，以便找出新添加的弱引用。一个弱引用进入队列意味着这个键不再被他人使用，并且已经被收集起来，于是，`WeakHashMap` 将删除对应的条目。

#### 9.3.4 链接散列集与映射

`LinkedHashSet` 和 `LinkedHashMap` 类用来记住插入元素项的顺序。这样就可以避免在散列表中项从表面上看是随机排列的。当条目插入到表中时，就会并入到双向链表中。

![](http://images.csmaxwell.xyz/20200430213754.png)

例如，想映射插入的处理：

```java
Map<String, Employee> staff = new LinkedHashMap<>();
staff.put("144", new Employee("Amy Lee"));
staff.put("567", new Employee("Harry Hacker"));
staff.put("157", new Employee("Gary Cooper"));
staff.put("456", new Employee("Francesca Cruz"));

// staff.keySet().iterator() 以下面的次序枚举键
144
567
157
456
// staff.values().iterator() 以下列顺序枚举这些值
Amy Lee
Harry Hacker
Gary Cooper
Francescca Cruz
```

链接散列映射（LinkedHashMap）将用访问顺序，而不是插入顺序，对映射条目进行迭代。每次调用 get 或 put，受影响的条目将从当前位置删除，并放到条目链表的尾部（只有条目在链表中的位置会受到影响，而散列表中的桶不会受影响。一个条目总位于与键散列码对应的桶中）。要构造这样一个的散列映射表：

```java
LinkedHashMap<K, V>(initialCapacity, loadFactor, true)
```

访问顺序对于实现高数缓存的“最近最少使用”原则十分重要。例如，可能希望将访问频率高的元素放在内存中，而访问频率低的元素则从数据库中读取。当在表中找不到元素项且表又已经满时，可以将迭代器加入到表中，并将枚举的前几个元素删除掉。这些是近期最少使用的几个元素。

甚至可以让这一过程自动化。即构造一个 LinkedHashMap 的子类，然后覆盖下面这个方法：

```java
protected boolean removeEldestEntry(Map.Entry<K, V> eldest)
```

每当方法返回 true 时，就添加一个新条目，从而导致删除 eldest 条目。例如，下面的高速缓存可以存放 100 个元素：

```java
Map<K, V> cache = new LinkedHashMap<>(128, 0.75F, true) {
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > 100;
    }
}();
```

另外，还可以对 eldest 条目进行评估，以此决定是否应该将它删除。例如，检查与这个条目一起存在的时间戳。

#### 9.3.5 枚举集与映射

EnumSet 是一个枚举类型元素集的高效实现。由于枚举类型只有有限个实例，所有 EnumSet 内部用位序列实现。如果对应的值在集中，则相应的位被置为 1。

EnumSet 类没有公共构造器。可以使用静态工厂方法构造这个集：

```java
enum Weekday {MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY};
EnumSet<Weekday> always = EnumSet.allOf(Weekday.class);
EnumSet<Weekday> never = EnumSet.noneOf(Weekday.class);
EnumSet<Weekday> workday = EnumSet.range(Weekday.MONDAY, Weekday.FRIDAY);
EnumSet<Weekday> mwf = EnumSet.of(Weekday.MONDAY, Weekday.WEDNESDAY, Weekday.FRIDAY);
```

可以使用 Set 接口的常用方法来修改 EnumSet。

EnumMap 是一个键类型为枚举类型的映射。它可以直接切高效地用一个值数组实现。在使用时，需要在构造器中指定键类型：

```java
EnumMap<Weekday, Employee> personInCharge = new EnumMap<>(Weekday.class);
```

注：在 EnumSet 的 API 文档中，将会看到 `E extends Enum<E>` 这种奇怪的类型参数，这里的 E 表示为一个枚举类型。所有的枚举类型都扩展与泛型 Enum 类。 

#### 9.3.6 标识散列映射

类 `IdentityHashMap` 有特殊的作用。在这个类中，键的散列值不是用 hashCode 函数计算的。而是用 `System.identityHashCode` 方法计算的。这是 `Object.hashCode` 方法根据对象的内存地址来计算散列码所使用的方式。而且，在对两个对象进行比较时，`IdentityHashMap` 类使用 `==` 而不使用 `equals`。

也就是说，不同的键对象，即使内容相同，也被设为是不同的对象。在实现对象遍历算法（如：对象串行化）时，这个类非常有用，可以用来跟踪每个对象的遍历状况。

### 9.4 视图与包装器

#### 9.4.1 轻量级集合包装器

Arrays 类的静态方法 asList 可以返回一个包装了普通 Java 数组的 List 包装器。这个方法可以将数组传递给一个期望得到列表或集合参数的方法。

```java
Card[] cardDeck = new Card[52];
...
List<Card> cardList = Arrays.asList(cardDeck);
```

返回的对象不是 ArrayList。它是一个视图对象，带有访问底层数组的 get 和 set 方法。改变数组大小的所有方法（例如，与迭代器相关的 add 和 remove 方法）都会抛出一个 Unsupported OperationException 异常。

asList 方法可以接受可变数目的参数。例如：

```java
List<String> names = Arrays.asList("Amy", "Bob", "Carl");
```

或者可以使用下面的方法：

```java
List<String> settings = Collections.nCopies(100, "DEFAULT");
```

创建了一个包含 100 个字符串的 List，每个串都被设置为 "DEFAULT"。

注：Collections 类包含了很多实用的方法，这些方法的参数和返回值都是集合。不要将它与 Collection 接口混淆起来。

#### 9.4.2 子范围

可以为很多集合建立子范围（subrange）视图。例如，假设有一个列表 staff，想从中取出第10个~第19个元素。可以使用 subList 方法来获得一个列表的子范围视图。

```java
List group2 = staff.subList(10, 20);
```

第一个索引包含在内，第二个索引则不包含在内。这与 String 类的 substring 操作中的参数情况相同。

可以将任何操作应用于子范围，并且能够自动地反映整个列表的情况。例如，可以删除整个子范围：

```java
group2.clear();
```

现在，元素自动从 staff 列表中清除了，并且 group2 为空。

对于有序集与映射，可以使用下列方法进行范围操作元素。

| 有序集（SortedSet）                 | 有序映射（SortedMap）                |
| ----------------------------------- | ------------------------------------ |
| SortedSet< E > subSet(E from, E to) | SortedMap<K, V> subMap(K from, K to) |
| SortedSet< E > headSet(E to)        | SortedMap<K, V> headMap(K to)        |
| SortedSet< E > tailSet(E from)      | SortedMap<K, V> tailMap(K from)      |

在 Java SE 6引入的 `NavigableSet` 接口赋予了范围操作的更多控制能力。

```java
NavigableSet< E > subSet(E from, boolean fromInclusive, E to, boolean toInclusive)
NavigableSet< E > headSet(E to, boolean toInclusive)
NavigableSet< E > tailSet(E from, boolean fromInclusive)
```

#### 9.4.3 不可修改的视图

`Collections` 还有几个方法，用于产生集合的不可修改视图（unmodifiable views）。这些视图对现有集合增加了一个运行时的检查。如果发现试图对集合进行修改，就抛出一个异常，同时这个集合将保持为修改的状态。

8个不可修改视图的方法：

```java
Collections.unmodifiableCollection
Collections.unmodifiableList
Collections.unmodifiableSet
Collections.unmodifiableSortedSet
Collections.unmodifiableNavigableSet
Collections.unmodifiableMap
Collections.unmodifiableSortedMap
Collections.unmodifiableNavigableMap
```

每个方法都定义与一个接口。例如，`Collections.unmodifiableList` 与 ArrayList、LinkedList 或者任何实现了 List 接口的其他类一起协同工作。

例如，假设想要查看某部分代码，但又不触及某个集合的内容，就可以进行下列操作：

```java
List<String> staff = new LinkedList<>();
...
lookAt(Collections.unmodifiableList(staff));
```

`Collections.unmodifiableList` 方法将返回一个实现 List 接口的类对象。其访问器方法将从 staff 集合中获取值。所有的访问器方法，已经被重新定意思为抛出一个 `UnsupportedOperationException` 异常，而不是将调用传递给底层集合。

不可修改视图并不是集合本身不可修改。仍然可以通过集合的原始引用，对集合进行修改。并且仍然可以让集合的元素调用更改器方法。

视图只是包装了接口而不是实际的集合对象，所有只能访问接口中定义的方法。例如，LinkedList 类有一些非常方便的方法，addFirst 和 addLast，它们都不是 List 接口的方法，不能通过不可修改视图进行访问 。

#### 9.4.4 同步视图

如果由多个线程访问集合，就必须确保集不会被意外地破坏。例如，如果一个线程试图将元素添加到散列表中，同时另一个线程正在对散列表进行再散列，其结果将是灾难性的。

类库的设计者使用视图机制来确保常规集合的线程安全，而不是实现线程安全的集合类。例如，Collections 类的静态 `synchronizedMap` 方法可以将任何一个映射表转换成具有同步访问方法的 Map:

```java
Map<String, Employee> map = Collections.synchronizedMap(new HashMap<String, Employee>());
```

现在，就可以由多线程访问 map 对象了。像 get 和 put 这类方法都是同步操作的，即在另一个线程调用另一个方法之前，刚才的方法调用必须彻底完成。

#### 9.4.5 受查视图

受查视图用来对泛型类型发生问题时提供调试支持。例如，将错误类型的元素混入泛型集合中。

```java
ArrayList<String> strings = new ArrayList<>();
ArrayList rawList = strings;
rawList.add(new Date());
```

这个错误的 add 命令在运行时检测不到。只有在另一部分代码中调用 get 方法，并将结果转化为 String 时，这个类才会抛出异常。

受查视图可以探测到这类问题。下面定义了一个安全列表：

```java
List<String> safeStrings = Collections.checkedList(strings, String.class);
```

视图的 add 方法将检测插入的对象是否属于给定的类。如果不属于给定的类，就立即抛出一个 ClassCastException。这样做的好处是错误可以在正确的位置得以报告。

### 9.5 算法

泛型集合接口有一个很大的优点，即算法只需实现一次。例如，考虑一下计算集合中最大元素这样一个简单的算法。使用传统方式，程序设计人员可能会使用循环实现这个算法。

```java
if (a.length == 0) throw new NoSuchElementException();
T largest = a[0];
for (int i = 1; i < a.length; i++) {
    if (largest.compareTo(a[i] < 0)) {
        largest = a[i];
    }
}
```

我们可以考虑使用集合接口，来编写一个在链表、数组列表或数组中找最大元素的方法。

我们使用迭代器遍历每个元素找出最大的元素，并将 max 方法实现为能够接受 Collection 接口的对象。

```java
public static <T extends Comparable> T max(Collection<T> c) {
    if (c.isEmpty()) {
        throw new NoSuchElementException();
    }
    Iterator<T> iter = c.iterator();
    T largest = iter.next();
    while (iter.hasNext()) {
        T next = iter.next();
        if (largest.compareTo(next) < 0) {
            largest = next;
        }
    }
    return largest;
}
```

#### 9.5.1 排序与混排

在 Collections 类中的 sort 方法可以对实现了 List 接口的集合进行排序。

```java
List<String> staff = new LinkedList<>();
...
Collections.sort(staff);
// 降序
staff.sort(Comparator.reverseOrder())
```

这个方法假定列表元素实现了 Comparable 接口。如果想采用其他方式对列表进行排序，可以使用 List 接口的 sort 方法传入一个 Comparator 对象。例如，按工资排序：

```java
staff.sort(Comparator.comparingDouble(Employee::getSalary));
// 逆序
staff.sort(Comparator.comparingDouble(Employee::getSalary).reversed())
```

Collections 类有一个算法 shuffle，其功能与排序刚好相反，即随机混排列表中的元素。

```java
ArrayList<Card> cards = ...;
Collections.shuffle(cards);
```

如果提供的列表没有实现 RandomAccess 接口，shuffle 方法将元素复制到数组中，然后打乱数组元素的顺序，最后再将打乱顺序后的元素复制回列表。

#### 9.5.2 二分查找

Collection 类的 binarySearch 方法实现了二分查找算法。但是，集合必须是排好序的，否则会返回错误的答案。

要查找某个元素，必须提供集合以及要查找的元素。如果集合没有采用 Comparable 接口的 compareTo 方法进行排序，还需要提供一个比较器对象。

```java
i = Collections.binarySearch(c, element);
i = Collections.binarySearch(c, element, comparator);
```

binarySearch 方法返回的数值大于等于 0，表示匹配对象的索引，也就是说，c.get(i) 等于这个比较顺序下的 element。如果返回负值，则表示没有匹配的元素。

#### 9.5.3 简单算法

在 Collections 类中提供几个简单且很有用的算法，通过这些算法，可以快速知道其用途。

常用的方法：

```
static <T extends Comparable<? super T>> T min(Collection<T> elements)
static <T extends Comparable<? super T>> T max(Collection<T> elements)
static <T> min(Collection<T> elements, Comparator<? super T> c)
static <T> max(Collection<T> elements, Comparator<? super T> c)
// 返回集合中最小/大的元素

static <T> void copy(List<? super T> to, List<T> from)
// 复制原列表的元素到目标列表

static <T> void fill(List<? super T> l, T value)
// 将列表中所有位置设置为相同的值

static <T> boolean ddAll(Collection<? super T> c, T... values)
// 将所有值添加到集合中，如果集合改变，返回 true

static <T> boolean replaceAll(List<T> l, T oldValue, T newValue)
// 用 newValue 取代所有值为 oldValue 的元素

static void swap(List<?> l, int i, int j)
// 交换给定偏移量的两个元素

static void reverse(List<?> l)
// 逆置列表中元素的顺序

default boolean removeIf(Predicate<? super E> filter)
// 删除所有匹配的元素

default void replaceAll(UnaryOperator<E> op)
// 对这个列表的所有元素应用这个操作
```

#### 9.5.4 批操作

很多操作会“成批”复制或删除元素。例如：

```java
// 从 coll1 中删除 coll2 中出现的所有元素
coll1.removeAll(coll2);

// 从 coll1 中删除所有未在 coll2 中出现的元素
coll1.retainAll(coll2);
```

如果，我们想找出两个集的交集，也就是两个元素共有的元素，可以这么操作：

```java
// 建立一个新集存放结果，a 为另外一个集合
Set<String> result = new HashSet<>(a);
// 使用 retainAll 方法
// 这会保留在 b 中出现的元素
result.retainAll(b);
```

#### 9.5.5 集合与数组的转换

数组 -> 集合：

```java
String[] values = ...;
HashSet<String> staff = new HashSet<>(Arrays.asList(values));
```

集合 -> 数组:

```java
Object[] values = staff.toArray();
```

这样得到是一个对象数组，不能使用强制类型转换：

``` 
String[] values = (String[]) staff.toArray(); // Error
```

toArray 方法返回的数组时一个 Object[] 数组，不能更改它的类型，或者使用 toArray 方法的一个变体形式，提供一个所需类型而且长度为 0 的数组。这样一来，返回的数组就会创建相同的数组类型：

```java
String[] values = staff.toArray(new String[0]);
```

还可以构造一个指定大小的数组：

```java
staff.toArray(new String[staff.size()]);
```

#### 9.5.6 编写自己的算法

如果编写自己的算法（实际上，是以集合作为参数的任何方法），应该尽可能地使用接口，而不要使用具体的实现。

### 9.6 遗留的集合

#### 9.6.1 Hashtable 类

Hashtable 类与 HashMap 类的作用一样，实际上，它们拥有相同的接口。与 Vector 类的方法一样。 Hashtable 的方法也是同步的。如果对同步性或遗留代码的兼容性没有任何要求，就应该使用 HashMap。如果需要并发访问，则需要使用 ConcurrentHashMap。

#### 9.6.2 枚举

枚举集合使用 Enumeration 接口对元素序列进行遍历。Enumeration 接口有两个方法，即 `hasMoreElements` 和 `nextElement`，这两个方法与 Iterator 接口的 hasNext 方法和 next 方法十分类似。

#### 9.6.3 属性映射

**属性映射**（property map）是一个类型非常特殊的映射结构。它有下面3个特性：

- 键与值都是字符串
- 表可以保存到一个文件中，也可以从文件中加载
- 使用一个默认的辅助表

实现属性映射的 Java 平台类称为 Properties。

属性映射通常用于程序的特殊配置选项。

#### 9.6.4 栈

从1.0版开始，标准类库中就包含了 Stack 类，其中就有大家熟悉的 push 方法和 pop 方法。但是，Stack 类扩展为 Vector 类，从理论角度看，Vector 类并不太令人满意，它可以让栈使用不属于栈操作的 insert 和 remove 方法，即可以在任何地方进行插入或删除操作，而不仅仅在栈顶。

#### 9.6.5 位集

Java 平台的 BitSet 类用于存放一个位序列。如果需要高效地存储位序列，可以使用位集。

BitSet 类提供了一个便于读取、设置或清除各个位的接口。使用这个接口可以避免屏蔽和麻烦的位操作。

例如，对于一个名为 bucketOfBits 的 BitSet，

```java
bucketOfBits.get(i)
```

如果第 i 位处于“开”状态，就返回 true；否则返回 false。同样地，

```java
bucketOfBits.set(i)
```

将第 i 位设置为"开"状态。最后

```java
bucketOfBits.clear(i)
```

将第 i 位设置为“关”状态。

## 第十四章 并发

在我们日常使用电脑时，操作系统将CPU的时间片分配给每个进程，从而让系统支持多任务（multitasking），在同一时刻运行多个程序。

而在一个程序中同时执行多个任务，每个任务称为线程（thread），它是线程控制的简称。可以同时运行一个以上线程的程序称为多线程程序（multithreaded）。

多进程与多线程的区别：

| 多进程                 | 多线程               |
| ---------------------- | -------------------- |
| 拥有自己的一套变量     | 线程之间数据是共享的 |
| 进程之间交换数据不方便 | 线程之间通信更容易   |
| 进程对系统耗费资源大   | 相较于进程，更轻量化 |

### 14.1 什么是线程

可以把线程比喻为车间里的工人，一个车间（进程）可以容纳多个工人，一个车间有多个房间，工人可以在各个房间进出，就象征一个进程的空间是共享的，每个线程都可以使用这些共享内存。但是，房间的大小是不同的，有些房间最多只能容纳一个人，比如厕所，里面有人的时候，其他人就不能进去了。这代表一个线程使用某些共享内存时，其他线程必须等它结束，才能使用这块内存。或者可以在门口加一把锁，先到的人锁上门，后到的人看到上锁，就在门口排队，等锁打开再进去。这就叫互斥锁（Mutual exclusion Mutex），防止多个线程同时读写某一块内存区域。

对于多人协助的区域，例如，厨房，则可以在门口挂n把钥匙，进去的人就取一把钥匙，出来再把钥匙挂回，后来的人发现钥匙架空了，就知道必须在门口排队等着。这种做法叫“信号量”（Semaphore），用来保证多个线程不会互相冲突。

想要在一个单独的线程中执行一个简单的任务的过程为：

1）将任务代码移到实现了 Runnable 接口的类的 run 方法中。这个接口非常简单，只有一个方法：

```java
public interface Runnable {
    void run();
}
```

由于 Runnable 是一个函数式接口，可以用 lambda 表达式建立一个实例：

```java
Runnable r = () -> {task code};
```

2）由 Runnable 创建一个 Thread 对象：

```java
Thread t = new Thread(r);
```

3）启动线程

```java
t.start();
```

### 14.2 中断线程

当线程的 run 方法执行方法体中最后一条语句后，并经由执行 return 语句返回时，或者出现了在方法中没有捕获的异常时，线程将终止。在 Java 的早期版本中，还有一个 stop 方法，其他线程可以调用它终止线程。但是，这个方法现在已经被弃用了。

没有可以强制线程终止的方法。然而，interrupt 方法可以用来请求终止线程。

对一个线程调用 interrupt 方法时，线程的中断状态将被置位，这是每个线程都具有的 boolean 标志。每个线程都应该不时地检查这个标志，以判断线程是否被中断。

要想弄清中断状态是否被置位，可以通过调用静态的 `Thread.currentThread` 方法获得当前线程，然后调用 isInterrupted 方法：

```java
while (!Thread.currentThread().isInterrupted() && more work to do) {
    ...
}
```

但是，如果线程被阻塞，就无法检测中断状态。这是产生 InterruptedException 异常的地方。当一个被阻塞的线程（调用 sleep 或 wait）上调用 interrupt 方法时，阻塞调用将会被 Interrupted Exception 异常中断。（存在不能被中断的阻塞 I/O 调用，应该考虑选择可中断的调用。）

没有任何语言方面的需求要求一个被中断的线程应该终止。中断一个线程不过是引起它的注意。被中断的线程可以决定如何响应中断。某些线程是如此重要以至于应该处理完异常后，继续执行，而不理会中断。但是，更普遍的情况是，线程将简单地将中断作为一个终止的请求。这种线程的 run 方法具有以下形式：

```java
Runnable r = () -> {
    try {
        ...
        while (!Thread.currentThread().isInterrupted() && more work to do) {
            ...
        }
    }
    catch(InterruptedException e) {
        // thread was interrupted during sleep or wait
    }
    finally {
        cleanup, if required
    }
    // exiting the run method terminates the thread
};
```

如果在每次工作迭代之后都调用 sleep 方法（或者其他的可中断方法），isInterrupted 检测既没有必要也没有用处。如果在中断状态被置位时调用 sleep 方法，它不会休眠。相反，它将清除这一状态并抛出 InterrptedException。因此，如果你的循环调用 sleep，不会检测中断状态。捕获 InterruptedException 异常：

```java
Runnable r = () -> {
    try {
        ...
        while (more work to do) {
            ...
            Thread.sleep(delay);
        }
    } catch(InterruptedException e) {
        // thread was interrupted during sleep
    } finally {
        
    }
};
```

interrupted 与 isInterrupted 方法的区别

| interrupted                      | isInterrupted              |
| -------------------------------- | -------------------------- |
| 静态方法                         | 实例方法                   |
| 检测当前线程是否被中断           | 检验是否有线程被中断       |
| 调用该方法会清除该线程的中断状态 | 调用该方法不会改变中断状态 |

对于 InterruptedException 异常有两种合理的处理方式：

- 在 catch 子句中调用 Thread.currentThread().interrupte() 来设置中断状态。调用者可以对其进行检测

```java
void mySubTask() {
    try {
        sleep(delay);
    } catch(InterruptedException e) {
        Thread.currentThread().interrupte();
    }
}
```

- 用 throws InterruptedException 标记你的方法，不采用 try 语句捕获异常。让调用者（或者，最终的 run 方法）捕获这一异常。

```java
void mySubTask() throws InterruptedException {
    sleep(delay);
}
```

### 14.3 线程状态

线程有以下6种状态：

- New（新创建）
- Runnable（可运行）
- Blocked（被阻塞）
- Waiting（等待）
- Timed waiting（计时等待）
- Terminated（被终止）

使用 getState 方法获取一个线程的当前状态。

#### 14.3.1 新创建线程

当用 new 操作符创建一个新线程时，如 new Thread(r)，该线程还没有开始运行。这意味着它的状态是 new。当一个线程处于新创建状态时，程序还没有开始运行线程中的代码。在线程运行之前还有一些基础工作要做。

#### 14.3.2 可运行线程

当我们调用 start 方法，线程处于 runnable 状态。一个可运行的线程可能正在运行也可能没有运行，这取决于操作系统给线程提供运行的时间。

现在的操作系统都使用抢占式调度，系统给每一个可运行线程一个时间片来执行任务，当时间片用完，操作系统剥夺该线程的运行权，并给另一个线程运行。

在多个处理器的机器上，每个处理器运行一个线程，当线程数超过处理器的数目，调度器采用时间片机制分配。

一个可运行的线程可能正在运行也可能没有运行（这就是为什么将这个状态称为可运行而不是运行）。

#### 14.3.3 被阻塞线程和等待线程

当线程处于被阻塞或等待状态时，它暂时不活动。它不运行任何代码且消耗最少的资源。直到线程调度器重新激活它。细节取决于它是怎样达到非活动状态的。

- 当一个线程视图获取一个内部的对象锁，而该锁被其他线程持有，则该线程进入阻塞状态。当所有其他线程释放该锁，并且线程调度器允许本线程持有它的时候，该线程将变成非阻塞状态。
- 当线程等待另一个线程通知调度器一个条件时，它自己进入等待状态。在调用 Object.wait 方法或 Thread.join 方法，或者是等待 java.util.concurrent 库中的 Lock 或 Condition 时，就会出现这种情况。实际上，被阻塞状态与等待状态有很大不同的。
- 有几个方法有一个超时参数。调用它们导致线程进入计时等待（timed waiting）状态。这一状态将一直保持到朝时期满或者接收到适当的通知。带有超时参数的方法有 Thread.sleep 和 Object.join、Lock.tryLock 以及 Condition.await 的计时版。

下图为线程可以具有的状态以及从一个状态到另一个状态可能的转换

![](http://images.csmaxwell.xyz/20200513212854.png)

#### 14.3.4 被终止的线程

线程会因为下面两个原因而被终止：

- 因为 run 方法正常退出而自然死亡。
- 因为一个没有捕获的异常终止了 run 方法二意外死亡。

### 14.4 线程属性

下图将讨论线程的各种属性，其他包括：线程优先级、守护线程、线程组以及处理未捕获异常的处理器。

#### 14.4.1 线程优先级

在 java 中，每一个线程有一个优先级。默认情况下，一个线程继承它的父线程的优先级。可以使用 setPriority 方法提高或降低任何一个线程的优先级。

```java
// 优先级 1
MIN_PRIORITY
// 优先级 5（默认）
NORM_PRIORITY
// 1优先级 10
MAX_PRIORITY
```

当线程调度器有机会选择新线程时，它会选择具有较高优先级的线程。但是线程优先级是高度依赖于系统的。当虚拟机依赖于宿主平台的线程实现机制时，Java 线程的优先级被映射到宿主平台的优先级上，优先级个数可能更多，也可能更少。

需要避免过度使用线程优先级，特别是将程序构建为功能的正确依赖于优先级。

#### 14.4.2 守护线程

可以通过调用 `t.setDaemon(true);` 将线程转换为守护线程（daemon thread）。守护进程的唯一用途是为其他线程提供服务。例如，计时线程就是一个守护进程，它定时发送“计时器嘀嗒”信号给其他线程或清空过时的高速缓存项的线程。当只剩下守护线程时，虚拟机就退出了，因为只剩下守护进程，就没必要继续运行程序了。

注：守护进程应该永远不去访问固有资源，如文件、数据库，因为它会在任何时候甚至一个操作的中间发生中断。

#### 14.4.3 未捕获异常处理器

线程的 run 方法不能抛出任何受查异常，但是，非受查异常会导致线程终止。在这种情况下，线程就死亡了。

但是，不需要任何 catch 子句来处理可以被传播的异常。相反，就在线程死亡之前，异常被传递到一个用于未捕获异常的处理器。

该处理器必须属于一个实现 Thread.UncaughtExceptionHandler 接口的类。这个接口只有一个方法。

```java
void uncaughtException(Thread t, Throwable e)
```

可以用 `setUncaughtExceptionHandler` 方法为任何线程 安装一个处理器。也可以用 Thread 类的静态放啊 `setDefaultUncaughtExceptionHandler` 为所有线程安装一个默认的处理器。替换处理器可以使用日志 API 发送未捕获异常的报告到日志文件。

如果不按照默认的处理器，默认的处理器为空。但是，如果不为独立的线程安装处理器，此时的处理器就是该线程的 ThreadGroup 对象。

线程组是一个可以统一管理的线程集合。默认情况下，创建的所有线程属于相同的线程组，但是，也可能会建立其他的组。现在引入了更好的特性用于线程集合的操作，所有建议不要在自己的程序中使用线程组。

ThreadGroup 类实现 `Thread.UncaughtExceptionHandler` 接口。它的 `uncaughtException` 方法有如下操作：

1）如果该线程组有父线程组，那么父线程组的 `uncaughtException` 方法被调用。

2）否则，如果 `Thread.getDefaultExceptionHandler` 方法返回一个非空的处理器，则调用该处理器。

3）否则，如果 Throwable 是 ThreadDeath 的一个实例，什么都不做。

4）否则，线程的名字以及 Throwable 的栈轨迹被输出到 System.err 上。

### 14.5 同步

在大多数实际的多线程应用中，两个或两个以上的线程需要共享对同一数据的存取。如果两个线程存取相同的对象，并且每个线程都调用了一个修改该对象状态的方法，将会发生什么呢？可以想象，线程彼此踩了对方的脚。根据各线程访问数据的次序，可能会产生讹误的对象。这样的情况称为竞争条件（race condition）。

#### 14.5.1 竞争条件的一个例子

为了避免多线程引起的对共享数据的讹误，必须学习如何同步存取。在本节中，会举例没有使用同步会发生什么。在下一节中，将演示如何同步数据存取。

我们模拟一个有若干账户的银行。随机地生成在这些账户之间转移钱款的交易。每一个账户有一个线程。每一笔交易中，会从线程所服务的账户中随机转移一定数目的钱款到另一个随机账户。

```java
public class Bank {
    private final double[] accounts;

    /**
     * Constructs the bank
     * @param n
     * @param initialBalance
     */
    public Bank(int n, double initialBalance) {
        accounts = new double[n];
        Arrays.fill(accounts, initialBalance);
    }

    /**
     * Transfers money from one account to another
     * 使用 Bank 类的 transfer 方法，将一个账户转移一定数目的钱款到另一个账户
     * @param from
     * @param to
     * @param amout
     */
    public void transfer(int from, int to, double amout) {
        if (accounts[from] < amout) {
            return ;
        }
        System.out.print(Thread.currentThread());
        accounts[from] -= amout;
        System.out.printf(" %10.2f from %d to %d", amout, from, to);
        accounts[to] += amout;
        System.out.printf("Total Balance: %10.2f%n", getTotalBalance());
    }

    /**
     * Gets the sum of all account balances.
     * @return
     */
    public double getTotalBalance() {
        double sum = 0;
        for (double account : accounts) {
            sum += account;
        }
        return sum;
    }

    /**
     * Gets the number of accounts in the bank.
     * @return
     */
    public int size() {
        return accounts.length;
    }
}
```

使用 Runnable 类的 run 方法，每次随机选择一个目标账户和随机账户，调用 transfer 方法，然后睡眠。

```java
public class UnsynchBankTest {
    public static final int NACCOUNTS = 100;
    public static final double INITIAL_BALANCE = 1000;
    public static final double MAX_AMOUT = 1000;
    public static final int DELAY = 10;

    public static void main(String[] args) {
        Bank bank = new Bank(NACCOUNTS, INITIAL_BALANCE);
        for (int i = 0; i < NACCOUNTS; i++) {
            int fromAccount = i;
            Runnable r = () -> {
                try {
                    while (true) {
                        int toAccount = (int) (bank.size() * Math.random());
                        double amount = MAX_AMOUT * Math.random();
                        bank.transfer(fromAccount, toAccount, amount);
                        Thread.sleep((int)(DELAY * Math.random()));
                    }
                } catch (InterruptedException e) {

                }
            };
            Thread t = new Thread(r);
            t.start();
        }
    }
}
```

在程序运行时，我们虽然不知道某个银行账户有多少钱，但是所有账户的总金额应该是不变的，因为转账操作不会是金额减少。

但是程序的输出是这样的：

```
Total Balance: 1000000.00
Total Balance: 1000000.00
Total Balance: 1000000.00
Total Balance: 99883.85
Total Balance: 99883.85
Total Balance: 99688.77
```

可以看到在程序最初，总金额保持在 1000000，但是过了一段时间，余额出现了轻微变化，总金额变少了。

发生这样的原因是：随着线程的增多，会出现两个线程试图同时更新一个账户的时候，这时，余额要么增加，要么变少。

#### 14.5.2 竞争条件详解

上一节，我们知道总余额会发生增加或减少的原因，是因为有多个线程试图同时更新同一个账户导致的。

这里，我们假定两个线程同时执行指令

```java
accounts[0] += amount;
```

问题在于这不是原子操作。该指令可能被处理如下：

1）将 accounts[to] 加载到寄存器。

2）增加 amount。

3）将结果写回 accounts[to]。

现在，假如第1个线程执行步骤1和2，然后，它被剥夺了运行权。假定第2个线程被唤醒并修改了 accounts 数组中的同一项。然后，第1个线程被唤醒并完成其第3步。

这样，这一动作擦去了第二个线程所做的更新。于是，总金额不再正确。

![](http://images.csmaxwell.xyz/20200515195634.png)

出现这种讹误，主要是调度器在计算过程中剥夺了线程的运行权。对于这种问题，会不定出现，我们需要避免这样操作。

#### 14.5.3 锁对象

有两种机制防止代码块受并发访问的干扰。Java 提供了一个 synchronized 关键字达到这一目的，并且在 Java SE 5.0 引入了 ReentrantLock 类。 synchronized 关键字自动提供了一个锁以及相关的条件，对于大多数需要显式锁的情况，这是很便利的。

使用 ReentrantLock 保护代码块的基本结构如下：

```java
myLock.lock();
try {
    ...
} finall {
    myLock.unlock();
}
```

这一结构确保了任何时刻只有一个线程进入临界区。一旦一个线程封锁了锁对象，其他任何线程都无法通过 lock 语句。当其他线程调用 lock 时，它们被阻塞，直到第一个线程释放锁对象。

注：将解锁操作放在 finally 子句中，是非常重要的，如果临界区代码抛出异常，锁必须释放，否则，其他线程将永远阻塞。

如果使用锁，就不能使用带资源的 try 语句。

下面使用锁来保护 Bank 类的 transfer 方法。

```java
public void transfer(int from, int to, double amout) {
    if (accounts[from] < amout) {
        return ;
    }
    bankLock.lock();
    try {
        System.out.print(Thread.currentThread());
        accounts[from] -= amout;
        System.out.printf(" %10.2f from %d to %d", amout, from, to);
        accounts[to] += amout;
        System.out.printf("Total Balance: %10.2f%n", getTotalBalance());
    } finally {
        bankLock.unlock();
    }
}
```

现在一个线程调用 transfer，在执行结束前被剥夺了运行权。假定第二个线程也调用 transfer，由于第二个线程不能获得锁，将在调用 lock 方法时被阻塞。它必须等待第一个线程完成 transfer 方法的执行后才能再度被激活。当第一个线程释放锁时，那么第二个线程才能开始运行。

![](http://images.csmaxwell.xyz/20200515201443.png)

现在运行程序，总余额将一直保持在 1000000，每个 Bank 对象都有自己的 ReentrantLock 对象。如果两个线程试图访问同一个 Bank 对象，那么锁以串行方式提供服务。当两个线程访问不同的 Bank 对象，每一个线程得到了不同的锁对象，两个线程都不会发生阻塞。

锁是可重入的，因为线程可以重复地获取已经持有的锁。锁保持一个持有计数来跟踪对 lock 方法的嵌套调用。线程在每一次调用 lock 都要调用 unlock 来释放锁。由于这个特性，被一个锁保护的代码可以调用另一个使用相同的锁的方法。

例如，transfer 方法调用 getTotalBalance 方法，这也会封锁 bankLock 对象，此时 bankLock 对象的持有计数为 2.当 getTotalBalance 方法退出的时候，持有计数变回1。当 transfer 方法退出的时候，持有计数变为 0。线程释放锁。

通常，可能想要保护由若干个操作来更新或检查共享对象的代码块。要确保这些操作完成后，另一个线程才能使用相同对象。

注：要留心临界区中的代码，不要因为异常的抛出而跳出临界区。如果在临界区代码结束之前抛出了异常，finally 子句将释放锁，但可能使对象处于受损状态。

```java
void lock();
// 获取这个锁，如果锁同时被另外一个线程拥有则会发生阻塞
void unlock();
// 释放这个锁
ReentrantLock();
// 构建一个可以被用来保护临界区的可重入锁。
ReentrantLock(boolean fair);
// 构建一个带有公平策略的锁。一个公平锁偏爱等待时间最长的线程
// 这会大大降低性能，默认，锁没有强制为公平的
```

注：公平锁比常规锁要慢得多，只有当你确实了解自己要做什么，对于你要解决的问题有特定的理由必须使用公平锁，才使用公平锁。即使使用公平锁，也无法确保线程调度器是公平的。如果线程调度器选择忽略一个线程，则没有机会公平地处理这个锁。

#### 14.5.4 条件对象

通常，线程进入临界区，却发现在某一条件满足之后它才能执行。要使用一个条件对象来管理那些已经获得了一个锁但是却不能做有用工作的线程。在这一节里，我们介绍 Java 库中条件对象的实现。（条件对象常被称为条件变量(conditional variable) ）。

现在我们来细化银行的模拟程序。我们要避免选择没有足够资金的账户作为转出账户。避免下面这样的代码：

```java
if (bank.getBalance(from) >= amount) {
    bank.transfer(from, to, amount);
}
```

线程完全有可能在成功通过 if 语句，在调用 transfer 方法前被中断，当线程再次运行时，账户余额可能已经低于提款金额。必须确保没有其他线程在检查余额与转账活动之间修改余额。通过使用锁来保护检查与转账动作来做到这一点：

```java
public void transfer(int from, int to, int amount) {
    bankLock.lock();
    try {
        while (accounts[from] < amount) {
            ...
        }
        ...
    } finally {
        bankLock.unlock();
    }
}
```

现在，当账户中没有足够的余额时，只有等待另一个线程向账户注入资金。但是，这一线程刚刚获得了 bankLock 的排它性访问，因此别的线程没有进行存款操作的机会。这就是需要条件对象的原因。

一个锁对象可以有一个或多个相关的条件对象。你可以用 newCondition 方法获得一个条件对象。

```java
class Bank {
    private Condition sufficientFunds;
    
    public Bank() {
        ...
        sufficientFunds = bankLock.newCondition();
    }
}
```

如果 transfer 方法发现余额不足，它调用

```java
sufficientFunds.await();
```

当前线程现在被阻塞了，并放弃了锁。这样我们可以使用另外一个线程进行增加余额的操作。

等待获得锁的线程和调用 await 方法的线程存在本质上的不同。一旦一个线程调用 await 方法，它进入该条件的等待集。当锁可用时，该线程不能马上解除阻塞。相反，它处于阻塞状态，直到另一个线程调用同一条件上的 signalAll 方法时为止。

当另一个线程转账时，它应该调用

```java
sufficientFunds.signalAll();
```

这一调用重新激活因为这一条件而等待的所有线程。当这些线程从等待集当中移出时，它们再次成为可运行的，调度器将再次激活它们。同时，它们将试图重新进入该对象。一旦锁成为可用的，它们中的某个将从 await 调用返回，获得该锁并从阻塞的地方继续执行。

此时，线程应该再次测试该条件。由于无法确保该条件被满足——signalAll 方法仅仅是通知正在等待的线程：此时有可能已经满足条件，值得再次去检测该条件。

注：通常，对 await 的调用应该在如下形式的循环体中

```java
while (!(ok to proceed)) {
    condition.await();
}
```

至关重要的是最终需要某个其他线程调用 signalAll 方法。当一个线程调用 await 时，它没有办法重新激活自身。它寄希望于其他线程。如果没有其他线程来重新激活等待的线程，它就永远不再运行了。这将导致死锁（deadlock）现象。如果所有其他线程被阻塞，最后一个活动线程在解除其他线程的阻塞状态之前就调用 await 方法，那么它也被阻塞。没有任何线程可以解除其他线程的阻塞，那么该程序就挂起了。

应该何时调用 signalAll，从经验上说，对象的状态有利于等待线程的方向改变时调用 signalAll。例如，当一个账户余额发生改变时，等待的线程应该有机会检查余额。

```java
// 当完成了转账时，调用 signalAll 方法
public void transfer(int from, int to, int mount) {
    bankLock.lock();
    try {
        while (accounts[from] < amount) {
            sufficientFunds.await(); 
        }
        ...
        sufficientFunds.signalAll();
    } finally {
        bankLock.unlock();
    }
}
```

注意调用 signalAll 不会立即激活一个等待线程。它仅仅解除等待线程的阻塞，以便这些线程可以在当前线程退出同步方法之后，通过竞争实现对对象的访问。

另一个方法 signal，则是随机解除等待集中某个线程的阻塞状态。这比解除所有线程的阻塞更加有效，但也存在危险。如果随机选择的线程发现自己仍然不能运行，那么它再次被阻塞。如果没有其他线程再次调用 signal，那么系统就死锁了。

当一个线程拥有某个条件的锁时，它仅仅可以在该条件上调用 await、signalAll 或 signal 方法。

#### 14.5.5 synchronzied 关键字

在前面，我们介绍了 Lock 和 Condition 对象。总结一下锁与条件的关键之处：

- 锁用来保护代码片段，任何时刻只能有一个线程执行被保护的代码。
- 锁可以管理试图进入被保护代码段的线程。
- 锁可以拥有一个或多个相关的条件对象。
- 每个条件对象管理那些已经进入被保护的代码段但还不能运行的线程。

Lock 和 Condition 接口为程序设计人员提供了高度的锁定控制。然而，大多数情况下，并不需要那样的控制，并且可以使用一种嵌入到 Java 语言内部的机制。从 1.0 开始，Java 中每一个对象都有一个内部锁。如果一个方法用 synchronized 关键字声明，那么对象的锁将保护整个方法。也就是说，要调用该方法，线程必须获得内部的对象锁。

```java
public synchronized void method() {
    method body
}
// 等价于
public void method() {
    this.intrinsicLock.lock();
    try {
        method body
    } finally {
        this.intrinsicLock.unlock();
    }
}
```

例如，可以简单地声明 Bank 类的 transfer 方法为 synchronized，而不是使用一个显式的锁。

内部对象锁只有一个相关条件。wait 方法添加一个线程到等待集中，notifyAll/ notify 方法解除等待线程的阻塞状态。换句话说，调用 wait 或 notifyAll 等价于 

```java
intrinsicCondition.await();
intrinsicCondition.signalAll();
```

注：wait、notifyAll 以及 notify 方法是 Object 类的 final 方法。Condition 方法必须被命令为 await、signalAll 和 signal 以便它们不会与那些方法发生冲突。

```java
// 实现 Bank 类
class Bank {
    private double[] accounts;
    
    public synchronized void transfer(int from, int to, int amount) throws InterruptedException {
        while (accounts[from] < amount) {
            wait();
        }
        accounts[from] -= amount;
        accounts[to] += amount;
        notifyAll();
    }
    
    public synchronized double getTotalBalance() {
        ...
    }
}
```

可以看到，使用 synchronized 关键字来编写代码要简介得多。当然，要理解这一代码，你必须了解每一个对象有一个内部锁，并且该锁有一个内部条件。有锁管理那些试图进入 synchronized 方法的线程，由条件来管理那些调用 wait 的线程。

将静态方法声明为 synchronized 也是合法的。如果调用这种方法，该方法获得相关的类对象的内部锁。例如，如果 Bank 类有一个静态同步的方法，那么当该方法被调用时，Bank.class 对象的锁被锁住。因此，没有其他线程可以调用同一个类的这个或任何其他的同步静态方法。

内部锁与条件存在一些局限。包括：

- 不能中断一个正在试图获得锁的线程。
- 试图获得锁时不能设定超时。
- 每个锁仅有单一的条件，可能是不够的。

在代码中应该使用哪一种？Lock 和 Condition 对象还是同步方法？

- 最好既不使用 Lock/Condition 也不使用 synchronized 关键字。很多情况可以使用 java.util.concurrent 包中的一种机制，它会为你处理所有的加锁。在 14.6 节，你会看到如何使用阻塞队列来同步完成一个共同任务的线程。
- 如果 synchronized 关键字适合你的程序，那么请尽量使用它，这样可以减少编写的代码数量，减少出错的几率。
- 如果特别需要 Lock/Condition 结构提供的独有特性时，才使用 Lock/Condition。

#### 14.5.6 同步阻塞

每一个 Java 对象有一个锁。线程可以通过调用同步方法获得锁。还有另一种机制可以获得锁，通过进入一个同步阻塞。当线程进入下面形式的阻塞：

```java
// 获得 obj 锁
synchronized (obj) {
    critical section
}
```

使用“特殊的”锁：

```java
public class Bank {
    private double[] accounts;
    private Object lock = new Object();
    ...
    public void transfer(int from, int to, int amount) {
        synchronized (lock) {
            accounts[from] -= amount;
            accounts[to] += amount;
        }
        System.out.println(...);
    }
}
```

lock 对象为每个 Java 对象持有的锁。

使用一个对象的锁来实现额外的原子操作，这种操作称为客户端锁定。

客户端锁定非常脆弱的，通常不推荐使用。

#### 14.5.7 监视器概念

锁与条件是线程同步的强大工具，但是他们不是面向对象的。对于保证多线程安全，最成功的解决方案是——监视器（monitor）,监视器具有以下特性：

- 监视器是只包含私有域的类。
- 每个监视器类的对象有一个相关的锁。
- 使用该锁对所有的方法进行加锁。换句话说，如果客户端调用 obj.method()，那么 obj 对象的锁在方法调用开始时自动获得，并且当方法返回时自动释放该锁。因为所有的域都是私有的，这样的安排确保了一个线程在对对象操作时，没有其他线程能访问该域。
- 该锁可以有任意多个相关条件。

Java 的设计者以不是很精确的方式采用了监视器概念，Java 中每个对象都有一个内部的锁和内部的条件。如果一个方法用 sychronized 关键字声明，那么，它表现的就像一个监视器方法。通过调用 wait/notifyAll/notify 来访问条件变量。

但是，Java对象与监视器又有所不同，导致线程的安全下降：

- 域可以不是 private
- 方法可以不为 synchronized
- 内部锁对客户是可用的

#### 14.5.8 Volatile 域

在现代的处理器与编译器上，不使用同步，可能会发现错误，主要原因是：

- 多处理器的计算机能够暂时在寄存器或本地内存缓冲区中保存内存中的值，但是，运行在不同处理器上的线程也许在同一个内存位置取到不同的值。
- 编译器可以改变指令执行的顺序以使吞吐量最大化。这种顺序不会改变代码的语义，但是编译器假定内存的值仅仅在代码中有显式的修改指令时才会改变。然鹅，内存的值可以被另一个线程改变！

使用锁来保护多个线程访问的代码，就不用考虑这种问题。编译器被要求通过在必要的时候刷新本地缓存来保持锁的效应，并且不能不正当地重新排序指令

> Brian Goetz 给出了下述“同步格言”：如果向一个变量写入值，而这个变量接下来可能会被另一个线程读取。或者，从一个变量读值，而这个变量可能是之前被另一个线程写入的，此时必须使用同步。

而 volatile 关键字为实例域的同步访问提供了一种免锁机制。声明一个域为 volatile，那么编译器和虚拟机就知道该域可能被另一个线程并发更新的。

例如，假定一个对象有一个布尔标记 done，它的值被一个线程设置却被另一个线程查询，如同我们讨论过的那样，你可以使用锁：

```java
private boolean done;
public synchronized boolean isDone() {
    return done;
}
public synchronized void setDone() {
    done = true;
}
```

或许使用内部锁不是个好主意。如果另一个线程已经对该对象加锁，isDone 和 setDone 方法可能阻塞。如果注意到这个方面，一个线程可以为这一变量使用独立的 Lock。但是，这也会带来许多麻烦。

这种情况下，将域声明为 volatile 是合理的：

```java
private volatile boolean done;
public boolean isDone() {
    return done;
}
public void setDone() {
    done = true;
}
```

Volatile 变量不能提供原子性。例如，方法

```java
public void flipDone() {
    done = !done;
}
```

不能确保翻转域中的值。不能保证读取、翻转和写入不被中断。

#### 14.5.9 final 变量

上一节我们已经了解到，除非使用锁或 volatile 修饰符，否则无法从多个线程安全地读取一个域。

还有一种情况可以安全地访问一个共享域，即这个域声明为 final 时。考虑下面这个声明：

```java
final Map<String, Double> accounts = new HashMap<>();
```

其他线程会在构造函数完成构造之后才看到这个 accounts 变量。

如果不使用 final，就不能保证其他线程看到的是 accounts 更新后的值，它们可能都只是看到 null，而不是新构造的 HashMap。

当然，对这个映射表的操作并不是线程安全的。如果多个线程在读写这个映射表，仍然需要进行同步。

#### 14.5.10 原子性

假设对共享变量除了赋值之外并不完成其他操作，那么可以将这些共享变量声明为 volatile。

`java.util.concurrent.atomic` 包中有很多类使用了很高效的机器级指令来保证其他操作的原子性。例如，AtomicInteger 类提供了方法 incrementAndGet 和 decrementAndGet，它们分别以原子方式将一个整数自增或自减。

#### 14.5.11 死锁

锁和条件不能解决多线程中的所有问题。考虑下面的情况：

```
账户1：$200
账户2：$300
线程1：从账户1转移$300到账户2
线程2：从账户2转移$400到账户1
```

运行这个程序，会发现线程1和线程2都被阻塞了，因为两个账户的余额都不足以进行转账。

有可能会因为每一个线程要等待更多的钱存入而导致所有的线程都被阻塞。这样的状态被称为死锁（deadlock）

Java 中没有任何东西可以避免或打破这种死锁现象。必须仔细设计程序，以确保不会出现死锁。

#### 14.5.12 线程局部变量

前面几节中，我们讨论了在线程间共享变量的风险。有时可能要避免共享变量，使用 ThreadLocal 辅助类为各个线程提供各自的实例。例如，SimpleDateFormat 类不是线程安全的。假设有一个静态变量：

```java
public static final SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");
```

如果两个线程都执行以下操作：

```java
String dateStamp = dateFormat.format(new Date());
```

结果可能很混乱，因为 dateFormat 使用的内部数据结构可能会被并发的访问所破坏。当然可以使用同步，但开销很大；或者也可以在需要时构造一个局部 SimpleDateFormat 对象，不过也太浪费了。

要为每个线程构造一个实例，可以使用以下代码：

```java
public static final ThreadLocal<SimpleDateFormat> dateFormat = 
    ThreadLocal.withInitial(() -> new SimpleDateFormat("yyyy-MM-dd"));
```

要访问具体的格式化方法，可以调用：

```java
String dateStamp = dateFormat.get().format(new Date());
```

在一个给定线程中首次调用 get 时，会调用 initialValue 方法。在此之后，get 方法会返回属于当前线程的那个实例。

在多个线程中生成随机数也存在类似的问题。`java.util.Random` 类是线程安全的。但是如果多个线程需要等待一个共享的随机数生成器，这会很低效。

可以使用 ThreadLocal 辅助类为各个线程提供一个单独的生成器，不过在 Java SE 7 中提供了一个便利类。只需要做以下调用：

```java
int random = ThreadLocalRandom.current().nextInt(upperBound);
```

ThreadLocalRandom.current() 调用会返回特定于当前线程的 Random 类实例。

#### 14.5.13 锁测试与超时

线程在调用 lock 方法来获得另一个线程所持有的锁的时候，很可能发生阻塞。

可以使用 tryLock 方法试图申请一个锁，成功获得锁返回 try，否则立即返回 false，线程可以立即离开去做其他事情。

```java
if (myLock.tryLock()) {
    ...
    try {
        ...
    } finally {
        myLock.unlock();
    }
} else {
    ...
}
```

在调用 tryLock 时，可以使用超时参数：

```java
if (myLock.tryLock(100, TimeUnit.MILLISECONDS))
```

TimeUnit 是一个枚举类型，可以取：SECONDS、MILLISECONDS、MICROSECONDS 和 NANOSECONDS。

lock 方法不能被中断。如果一个线程在等待获得一个锁时被中断，中断的线程在获得锁之前一直处于阻塞状态。如果出现死锁，那么，lock 方法就无法终止。

而使用带有超时参数的 tryLock，如果线程在等待期间被中断，将抛出 InterruptedException 异常。这允许程序打破死锁。

也可以调用 lockInterruptibly 方法。它就相当于一个超时设为无限的 tryLock 方法。

在等待一个条件时，也可以提供一个超时：

```java
myCondition.await(100, TimeUnit.MILLISECONDS)
```

如果一个线程被另一个线程通过调用 signalAll 或 signal 激活，或者超时时限已达到，或者线程被中断，那么 await 方法将返回。

如果等待的线程被中断，await 方法将抛出一个 InterruptedException 异常。在你希望出现这种情况时线程继续等待，可以使用 awaitUninterruptibly 方法替代 await。

#### 14.5.14 读/写锁

`java.util.concurrent.locks` 包定义了两个锁类，我们已经讨论的  ReentrantLock 类和 ReentrantReadWriteLock 类。如果很多线程从一个数据结构读取数据而很少线程修改其中数据的话，后者是十分有用的。在这种情况下，允许对读者线程共享访问是合适的。当然，写者线程依然是互斥访问的。

读/写锁的步骤：

1）构造一个 ReentrantReadWriteLock 对象：

```java
private ReentrantReadWriteLock rwl = new ReentrantReadWriteLock();
```

2）抽取读锁和写锁：

```java
private Lock readLock = rwl.readLock();
private Lock writeLock = rwl.writeLock();
```

3）对所有的获取方法加读锁：

```java
public double getTotalBalance() {
    readLock.lock();
    try {
        ...
    } finally {
        readLock.unlock();
    }
}
```

4）对所有的修改方法加写锁：

```java
public void transfer(...) {
    writeLock.lock();
    try {
        ...
    } finally {
        writeLock.unlock();
    }
}
```

#### 14.5.15 为什么弃用 stop 和 suspend 方法

在初始的 Java 版本定义了一个 stop 方法用来终止一个线程，以及一个 suspend 方法用来阻塞一个线程直至另一个线程调用 resume。stop 和 suspend 方法有一些共同点：都试图控制一个给定线程的行为。

stop、suspend 和 resume 方法已经弃用。stop 方法天生就不安全，经验证明 suspend 方法会经常导致死锁。

首先是 stop 方法，该方法会终止所有未结束的方法，包括 run 方法。当线程被终止，立即释放被它锁住的所有对象的锁。这会导致对象处于不一致的状态。例如，假定 TransferThread 在从一个账户向另一个账户转账的过程中被终止，钱款已经转出，却没有转入目标账户，现在银行对象就被破坏了。因为锁已经被释放，这种破坏会被其他尚未停止的线程观察到。

当线程要终止另一个线程时，无法知道什么时候调用 stop 方法是安全的，什么时候导致对象被破坏。因此，该方法被弃用了。在希望停止线程的时候应该中断线程，被中断的线程会在安全的时候停止。

在来看看 suspend 方法，与 stop 不同，suspend 不会破坏对象。但是，如果用 suspend 挂起一个持有一个锁的线程，那么，该锁在恢复之前是不可用的。如果调用 suspend 方法的线程试图获得同一个锁，那么程序死锁：被挂起的线程等着恢复，而将其挂起的线程等待获得锁。

### 14.6 阻塞队列