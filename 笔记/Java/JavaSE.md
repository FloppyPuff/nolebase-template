# 权限修饰符
用来限制类中的成员（成员变量、成员方法、构造器）能够被访问的范围。

- `private`:只能本类访问
- `缺省`:本类、同一个包中的类
- `protected`:本类，同一个包中的类、子孙类中
- `public`:任意位置

| 修饰符       | 本类里 | 同一个包中的类 | 子孙类 | 任意类 |
| --------- | --- | ------- | --- | --- |
| private   | √   |         |     |     |
| 缺省        | √   | √       |     |     |
| protected | √   | √       | √   |     |
| public    | √   | √       | √   | √   |
# 子类构造器的特点

- 子类的全部构造器，都会*先调用父类的构造器，再执行自己的构造器*。
- *默认调用无参构造器*，如需指定有参构造器，需*显式声明*。

# 多态

- 多态的前提：有**继承/实现**关系；存在**父类引用子类**对象；存在**方法重写**。
- 多态的好处：1.对象是**解耦合**的，更便于**扩展和维护**。2.*父类类型*的变量作为参数，可接受*任意的子类对象*。
- 注意：1.多态是**对象、行为**的多态，Java中的**属性（成员变量）不谈多态**。2.*多态*下*不能直接调用子类的独有功能*。
- 如何解决多态不能直接调用子类的独有功能：进行强制类型转换。如`People p = new Teacher()`、`Teacher t = (Teacher) p`。
- 强制转换的注意事项：1.存在继承/实现关系就可以再编译阶段进行强制类型转换，编译阶段不会报错。2.运行时，如果发现对象的真是类型与强制转换后的类型不同，就会报类型转换异常的错误。3.可以使用`variable instanceof class`语句来判断对象的真实类型再进行强制转换。

# Lombok

Lombok技术可以实现为类自动添加getter、setter方法，无参数构造器、toString方法等

- 所有字段的 `getter`
- 所有非 `final` 字段的 `setter`
- `toString()`
- `equals()` 和 `hashCode()`
- `isEqualsAndHashCodeRequired()` 如果字段是非 `final` 的就会生成
- `@NoArgsConstructor`:生成一个**无参构造函数**。
- `@AllArgsConstructor`:生成一个**全参构造函数**。

# final 关键字

可以修饰：类、方法、变量

- 修饰类：该类为最终类，不能被继承。
- 修饰方法：该方法被称为最终方法，特点是不能被重写了。
- 修饰变量：改变量只能被赋值一次。

注意：
- final修饰基本类型的变量，变量存储的数据不能被改变。
- final修饰引用类型的变量，变量存储的地址不能被改变，但地址所指向对象的内容是可以被改变的。

# 变量类型

Java 中的变量分为两类：

- **基本类型（Primitive Types）**：如 `int`, `double`, `boolean`, `char` 等，不继承自 `Object`，不是对象；
- **引用类型（Reference Types）**：如 `String`, `Person`, `int[]`, `List<String>` 等，本质是对象的引用，继承自 `Object`，可以调用方法、赋值为 `null`。

# 单例设计模式

- 1.构造器私有化
- 2.定义一个静态变量，用于本类的唯一一个对象
- 3.定义一个静态方法，用于返回本类的唯一对象

# Interface 接口

Java提供了一个关键字interface定义接口

```java
public interface 接口名{
	//成员变量（常量）
	//成员方法（抽象方法）
}
```

- 接口**不能**创建对象
- 接口是用来**被类实现**的，实现接口的类被称为**实现类**，一个类可以同时实现**多个**接口
- 接口中的方法默认为`public abstract`，成员变量默认为`public static final`

```java
权限修饰符 class 实现类类名 implements 接口1,接口2,接口3...{
	//实现类实现多个接口，必须重写完全接口的全部抽象方法，否则实现类需定义成抽象类
}
```

接口的好处：
- 弥补了类单继承的不足，一个类可以同时实现多个接口，使类的角色更多，功能更强大
- 让程序可以面向接口编程，利于程序的解耦合

### 接口新增的三种方法

JDK 8 开始，接口新增了三种形式的方法：

以上新增的方法增强了接口的能力，更便于项目的扩展和维护。
```java
public interface A {

    /**
     * 1、默认方法（实例方法）：使用 `default` 修饰，默认会被加上 `public` 修饰。
     * 注意：只能使用接口的实现类对象调用。
     */
    default void test1() {
        // 方法体
    }

    /**
     * 2、私有方法：必须用 `private` 修饰（JDK 9 开始才支持）。
     */
    private void test2() {
        // 方法体
    }

    /**
     * 3、类方法（静态方法）：使用 `static` 修饰，默认会被加上 `public` 修饰。
     * 注意：只能用接口名来调用。
     */
    static void test3() {
        // 方法体
    }
}
```
# 代码块

- 静态代码块 1.格式：`static {}` 2.特点：**类加载时自动执行** 3.作用：完成类的初始化，例如：对**静态变量进行初始化**
  
- 实例代码块 1.格式：{} 2.特点：每次**创建对象时**，执行实例代码块，**并在构造器之前执行** 3.作用：和构造器一样，都是用来完成对象的初始化的，例如：对**实例变量进行初始化**
  

# 内部类

## 成员内部类

- 无static修饰，属于外部类的对象持有
- 初始化方法：`外部类名称.内部类名称 对象名 = new 外部类名称().new 内部类名称()`
- 成员内部类中可以直接访问外部类的静态成员和实例成员

## 静态内部类

- 有static修饰的内部类，属于外部类持有
- 初始化方法：`外部类名称.内部类名称 对象名 = new 外部类名称.内部类名称()`
- 静态内部类只能访问外部类的静态成员，不能访问实例成员

## 匿名内部类

- 程序员不需要为这个类声明名字，默认有个**隐藏**的名字
- 特点：本质是一个**子类**，并会**立即创建出一个子类对象**。
- 作用：更方便的创建一个子类对象

```java
new 类或接口(参数值...) {
    类体（一般是方法重写）;
};
```

```java
new Animal() {
    @Override
    public void cry() {
        // 方法体
    }
};
```

# Lambda 表达式

- 可以用于替代默写匿名内部类对象，让程序更简洁
- 只能替代函数式接口的匿名内部类

```java
(被重写方法的形参列表) -> {
    被重写方法的方法体代码。
}
```

省略规则：
- 类型参数可以不写
- 如果只有一个参数，省略类型参数的同时“()”也可以省略，但多个参数不可以省略“()”
- 如果lambda表达式只有一行代码，大括号可以不写，同时如果这行代码是return语句，也要去掉return

静态方法引用：
- 类名::静态方法
- 场景：如果某个lambda表达式里只是调用一个静态方法，并且“->”前后参数的形式一直，就可以使用静态方法引用

实例方法引用：
- 对象名::实例方法

特定类型的方法引用：
- 特定类的名称::方法
- 如果某个lambda表达式里只是调用一个特定类型的实例方法，并且前面参数列表中的第一个参数是作为方法的主调，后面的所有参数都是作为该实例方法的入参的，则此时就可以使用特定类型的方法引用

构造器引用：
- 类名::new
- 如果某个lambda表达式里只是在创建对象，并且“->”前后参数情况一直，就可以使用构造器引用
# 函数式接口

- 有且仅有一个抽象方法的接口
- 大部分函数式接口，上面都可能会有一个`@FunctionalInterface`的注解，该注解用于约束当前接口必须是函数式接口，即只能有一个抽象方法

# String

- 通过""初始化的字符串常量会被放在字符串常量池，如果已经存在相同的字符串常量，则不会新建对象，而是返回已有的引用
- 通过new初始化的字符串常量会被放在堆内存中，每次使用new都会在堆中创建一个新的对象
- `startsWith(String str)`:判断是否以str开头

# ArrayList

1. 方法：
- `add(int index)`:添加元素，若指定index，则插入到指定位置
- `size()`:返回长度
- `remove(int index)`:根据索引移除元素
- `remove(T obj)`:根据内容删除（只删除第一个匹配项）
- `get(int index)`:获取元素
- `boolean contains(T obj)`:是否存在元素
- `indexOf(T obj)`:该元素第一次出现的索引，没有则返回-1
- `lastIndexOf(T obj)`:该元素最后一次出现的索引
- `set(int index, T obj)`:把索引为index的元素改为obj
- `clear()`:清除集合
- `boolean isEmpty()`:判断是否为空 

2. ArrayList是非线程安全的，多线程环境下可能会出错

3. 扩容机制：
   - ArrayList内部基于数组实现，默认初始容量为10，超过会自动扩容
   - 扩容策略一般是以当前容量的1.5倍进行增长

# Exception 异常

- 运行时异常：RuntimeException及其子类，编译阶段不会出现错误提醒，运行时出现的异常（如：数组索引越界异常）
- 编译时异常：编译阶段就会出现错误的异常（如：日期解析异常）

# 泛型

1. 定义类、接口、方法时，同时声明了一个或者多个类型变量，称为泛型类、泛型接口、泛型方法，它们统称为泛型
2. 
```java
public class ArrayList<E> {
    ...
}
```

1. 作用：泛型提供了在编译阶段约束所能操作的数据类型，并进行自动检查的能力。这样可以避免类型强制转换，及可能出现的异常
2. 泛型的本质：把具体的数据类型作为参数传给类型变量

## 泛型类

```java
修饰符 class 类名<类型变量,类型变量,...>{

}
```

## 泛型接口

```java
修饰符 interface 接口名<类型变量,类型变量,...>{

}
```

## 泛型方法

```java
修饰符 <类型变量,类型变量,...> 返回值类型 方法名(形参列表){

}
```

## 通配符

1. 就是"?"，可以在使用泛型的时候代表一切类型
2. 泛型的上下限：
   - 泛型上限：`? extends Car`:?能接受的必须是Car或者其子类
   - 泛型下限：`? super Car`:?能接受的必须是Car或者其父类

## 泛型支持的类型

1. 泛型不支持基本类型，只能支持对象类型（引用数据类型）
### 基本数据类型与对应的包装类（引用数据类型）

| 基本数据类型    | 对应的包装类（引用数据类型） |
| --------- | -------------- |
| `byte`    | `Byte`         |
| `short`   | `Short`        |
| `int`     | `Integer`      |
| `long`    | `Long`         |
| `char`    | `Character`    |
| `float`   | `Float`        |
| `double`  | `Double`       |
| `boolean` | `Boolean`      |
1. 包装类新增的功能
   - `toString()`:转换成字符串
   - `parseInt()`:转换为整型
   - `valueOf()`:取值

# 集合


## Collection 集合特点

1. List系列集合：
   - 添加的元素是有序、可重复、有索引
   - `ArrayList`、`LinkedList`
1. Set系列集合：
   - 添加的元素是无序、不重复、无索引
   - `HashSet`:无序、不重复、无索引
   - `LinkedHashSet`:有序、不重复、无索引
   - `TreeSet`:按照大小默认升序排序、不重复、无索引

| 方法名                                   | 说明                |
| ------------------------------------- | ----------------- |
| `public boolean add(E e)`             | 把给定的对象添加到当前集合中。   |
| `public void clear()`                 | 清空集合中所有的元素。       |
| `public boolean remove(E e)`          | 把给定的对象在当前集合中删除。   |
| `public boolean contains(Object obj)` | 判断当前集合中是否包含给定的对象。 |
| `public boolean isEmpty()`            | 判断当前集合是否为空。       |
| `public int size()`                   | 返回集合中元素的个数。       |
| `public Object[] toArray()`           | 把集合中的元素存储到数组中。    |

## Collection 的遍历

1. 迭代器遍历：
```java
Iterator<String> it = list.iterator();
while (it.hasNext){
	String ele = it.next();
	System.out.println(ele);
}
```

- Java 的 `Iterator` 初始状态是在第一个元素“之前”，必须调用一次 `next()` 才能访问第一个元素

2. 增强for循环（只适合遍历，不适合遍历并修改的并发操作）
```java
for (String ele : names){
	System.out.println(ele);
}
```

3. lambda表达式
```java
names.forEach(s -> System.out.println(s));
```

```java
names.forEach(System.out::println) //方法调用
```

```java
list.sort(Comparator.naturalOrder()); // 默认自然顺序（如字母顺序）
```

```java
list.sort(Comparator.reverseOrder()); // 逆序排列
```


详情参考：[[java.util.Comparator#^3e5ba4|使用内置静态方法构建复杂排序逻辑]]

## LinkedList

1. 底层是基于双链表存储数据
2. 特点
   - 链表中的数据是一个一个独立的节点组成的，节点在内存中是不连续的，每个节点包含数据值和下一个节点的地址
   - 查询慢，无论查询哪个数据都要从头开始找
   - 增删速度相对较快

### 方法名称

| 方法名称                        | 说明                |
| --------------------------- | ----------------- |
| `public void addFirst(E e)` | 在该列表开头插入指定的元素。    |
| `public void addLast(E e)`  | 将指定的元素追加到此列表的末尾。  |
| `public E getFirst()`       | 返回此列表中的第一个元素。     |
| `public E getLast()`        | 返回此列表中的最后一个元素。    |
| `public E removeFirst()`    | 从此列表中删除并返回第一个元素。  |
| `public E removeLast()`     | 从此列表中删除并返回最后一个元素。 |

## Set 集合

## Set 系列集合特点

- **无序** ：添加数据的顺序和获取出的数据顺序不一致。
- **不重复** ：集合中不允许存储重复元素。
- **无索引** ：无法通过索引来访问集合中的元素。
### 具体集合的特点：

1. **HashSet** ：
    - 无序、不重复、无索引。
    - 底层基于哈希表实现，增删改查效率高。
2. **LinkedHashSet** ：
    - **有序** （保持插入顺序）、不重复、无索引。
    - 底层结合了哈希表和双链表的特性。
3. **TreeSet** ：
    - **排序** （默认按自然顺序或自定义比较器排序）、不重复、无索引。
    - 底层基于红黑树实现，支持自动排序。

HashSet集合的底层原理：基于哈希表存储数据

1. 哈希值：
   - Java中的所有对象，都可以调用object类提供的hashcode方法， 返回该对象自己的哈希值
   - 就是一个int类型的随机值，Java中每个对象都有一个哈希值
2. 对象哈希值的特点：
   - 同一个对象多次调用hashcode()方法返回的哈希值是相同的
   - 不同的对象，它们的哈希值大概率不相等，但也有可能会相等（哈希碰撞）
3. 哈希表：
   - JDK8之前的哈希表：数组+链表
   - JDK8之后的哈希表：数组+链表+红黑树

对于自定义的类的对象，必须重写对象的hashCode()和equals()方法才能在HashSet中实现去重

LinkedHashSet的底层原理：基于哈希表（数组、链表、红黑树）

1. 它的每个元素都额外多了一个双链表的机制记录它前后元素的位置

TreeSet集合：
1. 特点：不重复、无索引、可排序（默认升序排序，按照元素的大小，由小到大排序）
2. 底层是基于红黑树实现的排序

注意：
1. 对于数值类型：Integer,Double，默认按照属猪本身的大小进行升序排序
2. 对于字符串类型：默认按照首字符的编号升序排序
3. 对于自定义类型，TreeSet默认是无法直接排序的。如果要实现自动排序，须在自定义类中实现Comparable<>接口，并在类中重写compareTo方法或者集合自定义Comparator比较器对象，重写比较规则


## 集合选择指南

1. **如果希望记住元素的添加顺序，需要存储重复的元素，又要频繁地根据索引查询数据？**
    - **用 `ArrayList` 集合** （有序、可重复、有索引），底层基于数组实现。（常用）
2. **如果希望记住元素的添加顺序，且增删首尾数据的情况较多？**
    - **用 `LinkedList` 集合** （有序、可重复、有索引），底层基于双链表实现。
3. **如果不在意元素的顺序，也没有重复元素需要存储，只希望增删改查都快？**
    - **用 `HashSet` 集合** （无序、不重复、无索引），底层基于哈希表实现。（常用）
4. **如果希望记住元素的添加顺序，也没有重复元素需要存储，且希望增删改查都快？**
    - **用 `LinkedHashSet` 集合** （有序、不重复、无索引），底层基于哈希表和双链表。
5. **如果要对元素进行排序，也没有重复元素需要存储，且希望增删改查都快？**
    - **用 `TreeSet` 集合** ，基于红黑树实现。

# Map 集合

## Map 集合体系的特点

### 注意：

- **Map 系列集合的特点都是由键决定的，值只是一个附属品，值是不做要求的。**

### 特点：

- **HashMap（由键决定特点）** ：无序、不重复、无索引。（用的最多）
- **LinkedHashMap（由键决定特点）** ：有序、不重复、无索引。
- **TreeMap（由键决定特点）** ：按照大小默认升序排序、不重复、无索引。

## 方法名称

| 方法名称                                         | 说明                               |
| -------------------------------------------- | -------------------------------- |
| `public V put(K key, V value)`               | 添加元素。                            |
| `public int size()`                          | 获取集合的大小。                         |
| `public void clear()`                        | 清空集合。                            |
| `public boolean isEmpty()`                   | 判断集合是否为空，为空返回`true`，反之返回`false`。 |
| `public V get(Object key)`                   | 根据键获取对应值。                        |
| `public V remove(Object key)`                | 根据键删除整个元素。                       |
| `public boolean containsKey(Object key)`     | 判断是否包含某个键。                       |
| `public boolean containsValue(Object value)` | 判断是否包含某个值。                       |
| `public Set<K> keySet()`                     | 获取全部键的集合。                        |
| `public Collection<V> values()`              | 获取`Map`集合的全部值。                   |


Map的遍历方式：
1. 键找值：
```java
Map<String, Integer> map = new HashMap<>();  
map.put("张三", 18);  
map.put("李四", 19);  
map.put("王五", 20);  
map.put("赵六", 21);   
Set<String> keys = map.keySet();  
for (String key : keys) {  
    System.out.println(key + ":" + map.get(key));  
}
```

2. 键值对

```java
for (Map.Entry<String, Integer> entry : map.entrySet()) {  
    System.out.println(entry.getKey() + ":" + entry.getValue());  
}
```

3. forEach+lambda表达式

```java
map.forEach((k, v) -> System.out.println(k + ":" + v));
```

# Stream 流

1. 终结方法
## Stream 提供的常用终结方法

| 方法名称                                                | 说明             |
| --------------------------------------------------- | -------------- |
| `void forEach(Consumer action)`                     | 对此流运算后的元素执行遍历。 |
| `long count()`                                      | 统计此流运算后的元素个数。  |
| `Optional<T> max(Comparator<? super T> comparator)` | 获取此流运算后的最大值元素。 |
| `Optional<T> min(Comparator<? super T> comparator)` | 获取此流运算后的最小值元素。 |
- 调用min()方法的返回值是一个Optional容器对象，需要调用get()方法来获取容器中的数据

1. 收集Stream流：
## 收集 Stream 流

- **收集 Stream 流** ：就是把 Stream 流操作后的结果返回到集合或者数组中去。
- **Stream 流** ：方便操作集合/数组的手段；集合/数组：才是开发中的目的。

---

## Stream 提供的常用终结方法

| 方法名称                             | 说明                    |
| -------------------------------- | --------------------- |
| `R collect(Collector collector)` | 把流处理后的结果收集到一个指定的集合中去。 |
| `Object[] toArray()`             | 把流处理后的结果收集到一个数组中去。    |

---

## Collectors 工具类提供了具体的收集方式

| 方法名称                                                                      | 说明               |
| ------------------------------------------------------------------------- | ---------------- |
| `public static <T> Collector toList()`                                    | 把元素收集到`List`集合中。 |
| `public static <T> Collector toSet()`                                     | 把元素收集到`Set`集合中。  |
| `public static Collector toMap(Function keyMapper, Function valueMapper)` | 把元素收集到`Map`集合中。  |
# 方法中可变参数

1. 是一种特殊形参，定义在方法、构造器的形参列表里，格式是：数据类型... 参数名称
2. 实际上就是一个数组，可以通过`变量名[int index]`来获取元素

# Collections 工具类

- 用来操作集合的工具类

## 方法名称

| 方法名称                                                                       | 说明                             |
| -------------------------------------------------------------------------- | ------------------------------ |
| `public static <T> boolean addAll(Collection<? super T> c, T... elements)` | 给集合批量添加元素。                     |
| `public static void shuffle(List<?> list)`                                 | 打乱`List`集合中的元素顺序。              |
| `public static <T> void sort(List<T> list)`                                | 对`List`集合中的元素进行升序排序。           |
| `public static <T> void sort(List<T> list, Comparator<? super T> c)`       | 对`List`集合中元素，按照比较器对象指定的规则进行排序。 |
# File

- File对象既可以代表文件，也可以代表文件夹


# IOStream

## 文件字节输入输出流

### 输出流

- **以内存为基准** ，把内存中的数据以字节的形式写出到文件中去。

### 构造器

|构造器|说明|
|---|---|
|`public FileOutputStream(File file)`|创建字节输出流与源文件对象接通。|
|`public FileOutputStream(String filepath)`|创建字节输出流与源文件路径接通。|
|`public FileOutputStream(File file, boolean append)`|创建字节输出流与源文件对象接通，可追加数据。|
|`public FileOutputStream(String filepath, boolean append)`|创建字节输出流与源文件路径接通，可追加数据。|

---

### 方法名称

| 方法名称                                                 | 说明             |
| ---------------------------------------------------- | -------------- |
| `public void write(int a)`                           | 写一个字节出去。       |
| `public void write(byte[] buffer)`                   | 写一个字节数组出去。     |
| `public void write(byte[] buffer, int pos, int len)` | 写一个字节数组的一部分出去。 |
| `public void close() throws IOException`             | 关闭流。           |

### 输入流

- **以内存为基准** ，可以把磁盘文件中的数据以字节的形式读入到内存中去。

---

### 构造器

|构造器|说明|
|---|---|
|`public FileInputStream(File file)`|创建字节输入流与源文件接通。|
|`public FileInputStream(String pathname)`|创建字节输入流与源文件路径接通。|

---

### 方法名称

| 方法名称                             | 说明                                               |
| -------------------------------- | ------------------------------------------------ |
| `public int read()`              | 每次读取一个字节返回，如果发现没有数据可读会返回`-1`。                    |
| `public int read(byte[] buffer)` | 每次用一个字节数组去读取数据，返回字节数组读取了多少个字节，如果发现没有数据可读会返回`-1`。 |
|                                  |                                                  |

资源释放的方案：
1. `try-catch-finally`:
   - `finally`代码区的特点：无论try中的程序是正常执行了，还是出现了异常，最后一定会执行finally区，除非JVM终止
   - 作用：一般用于程序执行完成后进行资源的释放操作
1. `try-with-resource`:在try后加个(),()中放置资源对象，这样子会自动调用close()方法(因为InputStream和OutputStream都实现了Closeable接口)

## FileReader 文件字符输入流

### 作用
- **以内存为基准** ，可以把文件中的数据以字符的形式读入到内存中去。
### 构造器

| 构造器                                  | 说明               |
| ------------------------------------ | ---------------- |
| `public FileReader(File file)`       | 创建字符输入流与源文件接通。   |
| `public FileReader(String pathname)` | 创建字符输入流与源文件路径接通。 |

---

### 方法名称

| 方法名称                             | 说明                                               |
| -------------------------------- | ------------------------------------------------ |
| `public int read()`              | 每次读取一个字符返回，如果发现没有数据可读会返回`-1`。                    |
| `public int read(char[] buffer)` | 每次用一个字符数组去读取数据，返回字符数组读取了多少个字符，如果发现没有数据可读会返回`-1`。 |

示例：

```java
public class main {  
    public static void main(String[] args) throws IOException {  
        try (Reader fr = new FileReader("src/com/fujunhao/day12/IOStream/test.txt")) {  
            char[] chs = new char[1024];  // buffer
            int len; // 记录每次多少个字符  
            while ((len = fr.read(chs)) != -1) {  //读到文件末尾
                String str = new String(chs, 0, len);  //用char[] chs来初始化String str
                System.out.println(str);  //输出str
            }  
        } catch (Exception e) {  //使用了try-with-resource来自动释放文件
            e.printStackTrace();  
        }  
    }  
}
```


## FileWriter 文件字符输出流

| 构造器                                                  | 说明                     |
| ---------------------------------------------------- | ---------------------- |
| `public FileWriter(File file)`                       | 创建字节输出流与原文件对象接通。       |
| `public FileWriter(String filepath)`                 | 创建字节输出流与原文件路径接通。       |
| `public FileWriter(File file, boolean append)`       | 创建字节输出流与原文件对象接通，可追加数据。 |
| `public FileWriter(String filepath, boolean append)` | 创建字节输出流与原文件路径接通，可追加数据。 |

| 方法名称                                        | 说明         |
| ------------------------------------------- | ---------- |
| `void write(int c)`                         | 写一个字符      |
| `void write(String str)`                    | 写一个字符串     |
| `void write(String str, int off, int len)`  | 写一个字符串的一部分 |
| `void write(char[] cbuf)`                   | 写入一个字符数组   |
| `void write(char[] cbuf, int off, int len)` | 写入字符数组的一部分 |

字符输出流写出数据后，必须刷新流，或者关闭流，写出取得数据才能生效

```java
public class main2 {  
    public static void main(String[] args) {  
        try (  
                Writer fw = new FileWriter("src/com/fujunhao/day12/IOStream/test.txt"); // try-with-resource
        ) {  
            fw.write(98);  // 写出内容到文件
            fw.write('a');  
            fw.write('傅');  
            fw.flush(); // 刷新缓冲区，将缓冲区的数据全部写出去  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
    }  
}
```

# 缓冲流

## IO 流体系结构图

### 概述
- **IO 流体系** ：分为 **字节流** 和 **字符流** 两大类。
- **抽象类** ：`InputStream`、`OutputStream`、`Reader`、`Writer`。
- **实现类** ：具体实现的流类。
### 字节流
1. **字节输入流**
    - `InputStream`
    - `FileInputStream`
    - `BufferedInputStream`（缓冲字节输入流）
2. **字节输出流**
    - `OutputStream`
    - `FileOutputStream`
    - `BufferedOutputStream`（缓冲字节输出流）
### 字符流
1. **字符输入流**
    - `Reader`
    - `FileReader`
    - `BufferedReader`（缓冲字符输入流）
2. **字符输出流**
    - `Writer`
    - `FileWriter`
    - `BufferedWriter`（缓冲字符输出流）

## 缓冲字节流的特点

- **作用** ：可以提高字节输入/输出流读取数据的性能。
- **原理** ：缓冲字节输入流自带了 8KB 缓冲池；缓冲字节输出流也自带了 8KB 缓冲池。

## 构造器说明

| 构造器                                            | 说明                                   |
| ---------------------------------------------- | ------------------------------------ |
| `public BufferedInputStream(InputStream is)`   | 把低级的字节输入流包装成一个高级的缓冲字节输入流，从而提高读数据的性能。 |
| `public BufferedOutputStream(OutputStream os)` | 把低级的字节输出流包装成一个高级的缓冲字节输出流，从而提高写数据的性能。 |

## 缓冲字节流

示例：

```java
public class main3 {  
    public static void main(String[] args) {  
        copyFile("src/com/fujunhao/day12/IOStream/test.txt", "src/com/fujunhao/day12/IOStream/test2.txt");  
    }  
  
    public static void copyFile(String srcPath, String destPath) { // 定义方法 
        try (  
                InputStream fis = new FileInputStream(srcPath);  
                BufferedInputStream bfis = new BufferedInputStream(fis); //缓冲字节输入流
                OutputStream fos = new FileOutputStream(destPath);  
                BufferedOutputStream bfos = new BufferedOutputStream(fos);//缓冲字节输出流
        ) {  
            byte[] buffer = new byte[1024];  // buffer
            int len;  //buffer长度
            while ((len = bfis.read(buffer)) != -1) {  
                bfos.write(buffer, 0, len);  // 写出内容
            }  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
    }  
}
```


## 缓冲字符输入流

示例：

```java
public class main4 {  
    public static void main(String[] args) {  
        try (  
                Reader fr = new FileReader("src/com/fujunhao/day12/IOStream/test.txt");  
                BufferedReader bfr = new BufferedReader(fr);  
        ) {  
            char[] buffer = new char[1024];  
            int len;  
            while ((len = bfr.read(buffer)) != -1) {  
                String str = new String(buffer, 0, len);  
                System.out.println(str);  
            }  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
    }  
}
```

字符缓冲输入流新增的功能：按照行读取字符

- `public String readLine()`:读取一行数据返回，如果没有数据可读了，会返回`null`

## 缓冲字符输出流

示例：

```java
public class main5 {  
    public static void main(String[] args) {  
        try (  
                Writer fw = new FileWriter("src/com/fujunhao/day12/IOStream/test.txt");  
                BufferedWriter bfw = new BufferedWriter(fw);  
        ) {  
            bfw.write("这是一段测试案例");  
            bfw.newLine();  
            bfw.write("这还是一段测试案例");  
            bfw.newLine();  
        } catch (Exception e) {  
            e.printStackTrace();  
        }  
    }  
}
```

字符缓冲输出流新增的功能：
- `public void newLine()`:换行

缓冲字节流为什么提高了字节流读写数据的性能？
- 缓冲字节流通过减少频繁的系统调用（如 read/write），使用内存缓冲区批量处理数据，从而显著提升 I/O 性能。

## 字符输入转换流

- 解决不同编码时，字符流读取文本内容乱码的问题
- 解决思路：先获取文件的原始字节流，再将其按真是的字符集编码转成字符输入流，这样字符输入流中的字符就不乱码了

| 构造器                                                        | 说明                                                   |
| ---------------------------------------------------------- | ---------------------------------------------------- |
| `public InputStreamReader(InputStream is)`                 | 把原始的字节输入流，按照代码默认编码转换成字符输入流（与直接用 `FileReader` 的效果一样）。 |
| `public InputStreamReader(InputStream is, String charset)` | 把原始的字节输入流，按照指定字符集编码转换成字符输入流（重点）。                     |

```java
// 先提取文件的原始字节流
InputStream is = new FileInputStream("src");
// 指定字符集把原始字节流转换成字符输入流
Reader isr = new InputStreamReader(is, "GBK");
// 创建缓冲字符输入流包装低级的字符输入流
BufferedReader bisr = new BufferedReader(isr);
```

## 打印流

PrintStream/PrintWriter

- 打印流实现更方便、更高效的打印数据出去，能实现打印什么就是什么出去

| 构造器                                                                        | 说明                    |
| -------------------------------------------------------------------------- | --------------------- |
| `public PrintStream(OutputStream/File/String)`                             | 打印流直接通向字节输出流/文件/文件路径。 |
| `public PrintStream(String fileName, Charset charset)`                     | 可以指定写出去的字符编码。         |
| `public PrintStream(OutputStream out, boolean autoFlush)`                  | 可以指定实现自动刷新。           |
| `public PrintStream(OutputStream out, boolean autoFlush, String encoding)` | 可以指定实现自动刷新，并可指定字符的编码。 |

| 方法                                     | 说明           |
| -------------------------------------- | ------------ |
| `public void println(Xxx xx)`          | 打印任意类型的数据出去。 |
| `public void write(int/byte[]/byte[])` | 可以支持写字节数据出去。 |

## 特殊数据流

DataOutputStream/DataInputStream

| 构造器                                         | 说明                    |
| ------------------------------------------- | --------------------- |
| `public DataOutputStream(OutputStream out)` | 创建新数据输出流（基于基础的字节输出流）。 |

| 方法                                                           | 说明                              |
| ------------------------------------------------------------ | ------------------------------- |
| `public final void writeByte(int v) throws IOException`      | 将 `byte` 类型的数据写入基础的字节输出流。       |
| `public final void writeInt(int v) throws IOException`       | 将 `int` 类型的数据写入基础的字节输出流。        |
| `public final void writeDouble(Double v) throws IOException` | 将 `double` 类型的数据写入基础的字节输出流。     |
| `public final void writeUTF(String str) throws IOException`  | 将字符串数据以 UTF-8 编码成字节，写入基础的字节输出流。 |
| `public void write(int/bYTE[]/byte[])`                       | 支持写字节数据出去。                      |
## IO 框架

- Commons-io 是 Apache 开源基金组织提供的一组有关 IO 操作的小框架，目的是提高 IO 流的开发效率。

### FileUtils 类提供的部分方法展示

| 方法声明                                                                                            | 说明     |
| ----------------------------------------------------------------------------------------------- | ------ |
| `public static void copyFile(File srcFile, File destFile)`                                      | 复制文件。  |
| `public static void copyDirectory(File srcDir, File destDir)`                                   | 复制文件夹。 |
| `public static void deleteDirectory(File directory)`                                            | 删除文件夹。 |
| `public static String readToString(File file, String encoding)`                                 | 读取数据。  |
| `public static void writeStringToFile(File file, String data, String charname, boolean append)` | 写入数据。  |

# 多线程

1. 什么是线程？
   - 线程（Thread）是一个程序内部的一条执行流程
2. 什么是多线程？
   - 多线程是指从软硬件上实现的多条执行流程的技术（多条线程由CPU负责调度执行）
## 创建线程

### 多线程的创建方式一：继承 Thread 类

1. 定义一个子类 `MyThread` 继承线程类 `java.lang.Thread`，重写 `run()` 方法。
2. 创建 `MyThread` 类的对象。
3. 调用线程对象的 `start()` 方法启动线程（启动后还是执行 `run` 方法的）。

方式一优缺点：

- **优点**：编码简单。
- **缺点**：线程类已经继承 `Thread`，无法继承其他类，不利于功能的扩展。


### 多线程的创建方式二：实现 Runnable 接口

1. 定义一个线程任务类 `MyRunnable` 实现 `Runnable` 接口，重写 `run()` 方法。
2. 创建 `MyRunnable` 任务对象。
3. 把 `MyRunnable` 任务对象交给 `Thread` 处理。

#### Thread 类提供的构造器

| Thread 类提供的构造器 | 说明 |
|------------------------|------|
| `public Thread(Runnable target)` | 封装 Runnable 对象成为线程对象。 |

4. 调用线程对象的 `start()` 方法启动线程。

方式二的优缺点

- **优点**：任务类只是实现接口，可以继续继承其他类、实现其他接口，扩展性强。
- **缺点**：需要多一个 `Runnable` 对象。

匿名内部类的写法：

```java
new Thread(() -> {  // lambda表达式
    for (int i = 0; i < 5; i++) {  
        System.out.println(i);  
    }  
}).start();
```


示例：

```java
public class test2 {  
    public static void main(String[] args) throws ExecutionException, InterruptedException {  
        Callable<String> mc = new MyCallable(100);  
        FutureTask<String> f1 = new FutureTask<>(mc);  
        Thread t1 = new Thread(f1);  
        t1.start();  
        System.out.println(f1.get());  
    }  
}  
  
class MyCallable implements Callable<String> {  
    @Override  
    public String call() {  
        return "abc";  
    }  
  
    public MyCallable(int n) {  
        this.n = n;  
    }  
  
    private int n;  
}
```

### 多线程的创建方式三：FuturTask

#### FutureTask提供的构造器

| FutureTask提供的构造器 | 说明 |
|------------------------|------|
| `public FutureTask<>(Callable call)` | 把Callable对象封装成FutureTask对象。 |

#### FutureTask提供的方法

| FutureTask提供的方法 | 说明 |
|-----------------------|------|
| `public V get() throws Exception` | 获取线程执行call方法返回的结果。 |

线程创建方式三的优缺点

- **优点**：线程任务类只是实现接口，可以继续继承类和实现接口，扩展性强；可以在线程执行完毕后去获取线程执行的结果。
- **缺点**：编码复杂一点。

注意事项：
1. 直接调用run()方法会当成普通方法执行，此时相当于还是单线程执行
2. 只有调用start()方法才是启动一个新的线程执行
3. 不要把主线程任务放在启动子线程之前

## 线程的常用方法

Thread提供的常用方法

| 方法名称                                   | 说明                           |
| -------------------------------------- | ---------------------------- |
| `public void run()`                    | 线程的任务方法                      |
| `public void start()`                  | 启动线程                         |
| `public String getName()`              | 获取当前线程的名称，线程名称默认是`Thread-索引` |
| `public void setName(String name)`     | 为线程设置名称                      |
| `public static Thread currentThread()` | 获取当前执行的线程对象                  |
| `public static void sleep(long time)`  | 让当前执行的线程休眠多少毫秒后，再继续执行        |
| `public final void join()`             | 让调用当前这个方法的线程先执行完！            |
Thread提供的常见构造器

| 构造器                                           | 说明                           |
| --------------------------------------------- | ---------------------------- |
| `public Thread(String name)`                  | 可以为当前线程指定名称                  |
| `public Thread(Runnable target)`              | 封装`Runnable`对象成为线程对象         |
| `public Thread(Runnable target, String name)` | 封装`Runnable`对象成为线程对象，并指定线程名称 |
## 线程同步

方法一：同步代码块

- 作用：把访问共享资源的核心代码给上锁，以此保证线程安全
- 原理：每次只允许一个线程枷锁后进入，执行完毕后自动解锁，其他线程才可以执行
- 使用规范：建议使用共享资源作为锁对象，对于实例方法建议使用this作为锁对象，对于静态方法建议使用字节码（类名.class）对象作为锁对象

```java
synchronized (){
dosomething...
}
```

方法二：同步方法

- 作用：把访问共享资源的和新方法给上锁，以此保证线程安全
- 原理：每次只能一个线程进入，执行完毕以后自动解锁，其他线程才能来进行

```java
public synchronized void dosomething(){
dosomething...
}
```

方法三：Lock锁

- Lock锁是从JDK5开始引入的新锁定机制，相较于传统的`synchronized`关键字，它提供了更灵活、强大的加锁和解锁操作。比如可以实现公平锁、可中断锁等功能。
- `Lock`是一个接口，无法直接实例化。实际开发中，常使用其实现类`ReentrantLock` （可重入锁）来创建锁对象。

| 构造器                      | 说明                                 |     |
| ------------------------ | ---------------------------------- | --- |
| `public ReentrantLock()` | 用于获取`Lock`接口的实现类`ReentrantLock`的对象 |     |
Lock的常用方法

| 方法名称            | 说明  |
| --------------- | --- |
| `void lock()`   | 获得锁 |
| `void unlock()` | 释放锁 |
- 锁对象建议使用`final`修饰，防止被别人篡改
- 释放锁对象的操作放到`finally`代码块中，保证锁对象一定会被解锁

## 线程池

1. 什么是线程池？
   - 线程池就是一个可以复用线程的技术
2. 为什么要使用线程池？
   - 用户每发起一个请求，后台就需要创建一个新线程来处理，创建线程的开销是很大的，并且请求过多时，肯定会产生大量的线程出来，这样会严重影响系统的性能
3. 如何创建线程池？
   - 方式一：使用ExecutorService（接口）的实现类ThreadPoolExecutor创建一个线程池对象
   - 方式二：使用Executors（线程池的工具类）调用方法返回不同特点的线程池对象
- 
方式一：通过 `ThreadPoolExecutor` 创建线程池

```java
public ThreadPoolExecutor(int corePoolSize,
                         int maximumPoolSize,
                         long keepAliveTime,
                         TimeUnit unit,
                         BlockingQueue<Runnable> workQueue,
                         ThreadFactory threadFactory,
                         RejectedExecutionHandler handler)
```

参数说明

| 参数名称              | 作用       |
| ----------------- | -------- |
| `corePoolSize`    | 核心线程数    |
| `maximumPoolSize` | 最大线程数    |
| `keepAliveTime`   | 临时线程存活时间 |
| `unit`            | 存活时间单位   |
| `workQueue`       | 任务队列     |
| `threadFactory`   | 线程工厂     |
| `handler`         | 任务拒绝策略   |
ExecutorService 的常用方法

| 方法名称                                 | 说明                                   |
| ------------------------------------ | ------------------------------------ |
| `void execute(Runnable command)`     | 执行`Runnable`任务。                      |
| `Future<T> submit(Callable<T> task)` | 执行`Callable`任务，返回未来任务对象，用于获取线程返回的结果。 |
| `void shutdown()`                    | 等全部任务执行完毕后，再关闭线程池！                   |
| `List<Runnable> shutdownNow()`       | 立刻关闭线程池，停止正在执行的任务，并返回队列中未执行的任务。      |

什么时候开始创建临时线程？
- 新任务提交时发现核心线程都在忙，任务队列也满了，并且还可以创建临时线程，此时才会创建临时线程
什么时候会拒绝新任务？
- 核心线程和临时线程都在忙，任务队列也满了，新的任务过来就会被拒绝

任务拒绝策略

| 策略                                         | 说明                                            |
| ------------------------------------------ | --------------------------------------------- |
| `ThreadPoolExecutor.AbortPolicy()`         | 丢弃任务并抛出`RejectedExecutionException`异常。是默认的策略。 |
| `ThreadPoolExecutor.DiscardPolicy()`       | 丢弃任务，但是不抛出异常。这是不推荐的做法。                        |
| `ThreadPoolExecutor.DiscardOldestPolicy()` | 抛弃队列中等待最久的任务，然后把当前任务加入队列中。                    |
| `ThreadPoolExecutor.CallerRunsPolicy()`    | 由主线程负责调用任务的`run()`方法，从而绕过线程池直接执行。             |
通过 `Executors` 创建线程池

- 是一个线程池的工具类，提供了很多静态方法用于返回不同特点的线程池对象。

| 方法名称                                                                              | 说明                                            |
| --------------------------------------------------------------------------------- | --------------------------------------------- |
| `public static ExecutorService newFixedThreadPool(int nThreads)`                  | 创建固定线程数量的线程池。如果某个线程因执行异常而结束，那么线程池会补充一个新线程替代它。 |
| `public static ExecutorService newSingleThreadExecutor()`                         | 创建只有一个线程的线程池对象。如果该线程出现异常而结束，那么线程池会补充一个新线程。    |
| `public static ExecutorService newCachedThreadPool()`                             | 线程数量能随着任务增加而增加，如果线程任务执行完毕且空闲了 60 秒，会被回收掉。     |
| `public static ScheduledExecutorService newScheduledThreadPool(int corePoolSize)` | 创建一个线程池，可以实现在给定的延迟后运行任务，或者定期执行任务。             |
并发和并行：
- 并发：多个任务**交替执行**，看起来像是同时进行，但不一定真的同时。
- 并行：多个任务**真正同时执行**。

# 网络编程

## 基本的通信架构

基本的通信架构有两种形式：CS(Client/Server)架构、BS(Browser/Server)架构

## 网络通信三要素

### IP 地址

1. IP地址

- **设备在网络中的地址** ，是设备在网络中的唯一标识。

2. 端口

- **应用程序在设备中的唯一标识** 。

3. 协议

- **连接和数据在网络中传输的规则** 。

IP地址

- **IP（Internet Protocol）** ：全称“互联网协议地址”，是分配给上网设备的唯一标识。
- 目前，被广泛采用的 IP 地址形式有两种：IPv4、IPv6。

IPv4

- IPv4 是 **Internet Protocol version 4** 的缩写，它使用 32 位地址，通常以 **点分十进制** 表示。

IPv6

IPv6 是 **Internet Protocol version 6** 的缩写，它使用 128 位地址，号称可以为地球上的每一粒沙子编号。

IPv6 分成 8 段，每段每四位编码成一个十六进制位表示，每段之间用冒号（`:`）分开，将这种方式称为 **冒分十六进制** 。

InetAddress的常用方法

| InetAddress类的常用方法                                                             | 说明                             |
| ----------------------------------------------------------------------------- | ------------------------------ |
| `public static InetAddress getLocalHost()`throws UnknownHostException         | 获取本机IP，返回一个`InetAddress`对象     |
| `public String getHostName()`                                                 | 获取该IP地址对应的主机名。                 |
| `public String getHostAddress()`                                              | 获取该IP地址对象中的IP地址信息。             |
| `public static InetAddress getByName(String host)`throws UnknownHostException | 根据IP地址或者域名，返回一个`InetAddress`对象 |
| `public boolean isReachable(int timeout)`throws IOException                   | 判断主机在指定毫秒内与该IP对应的主机是否能连通       |
### 端口

用来标记正在计算机设备上运行的应用程序，被规定为一个16位的二进制，范围是0~65535

1. 端口分类：
   - 周知端口：0~1023，被预先定义的知名应用占用（如：HTTP占用80，FTP占用21）
   - 注册端口：1024~49151，分配给用户进程或某些应用程序
   - 动态端口：49152~65530，之所以称为动态端口，是因为它一般不固定分配某种进程，而是动态分配

### 协议

网络上通信的设备，事先规定的连接规则，以及传输数据的规则被称为网络通信协议

OSI网络参考模型：全球网络互联标准
TCP/IP网络模型：事实上的国际标准

**OSI网络参考模型与TCP/IP网络模型对比**

| OSI网络参考模型 | TCP/IP网络模型 | 各层对应             | 面向操作                         |
| --------- | ---------- | ---------------- | ---------------------------- |
| 应用层       | 应用层        | HTTP、FTP、SMTP... | 应用程序需要关注的：浏览器、邮箱。程序员一般在这一层开发 |
| 表示层       |            | -                | -                            |
| 会话层       |            | -                | -                            |
| 传输层       | 传输层        | UDP、TCP...       | 选择使用的TCP、UDP协议               |
| 网络层       | 网络层        | IP...            | 封装源和目标IP                     |
| 数据链路层     | 数据链路层+物理层  | 比特流...           | 物理设备中传输                      |
| 物理层       |            | -                | -                            |

传输层的两个通信协议：
UDP(User Datagram Protocol):用户数据报协议
TCP(Transmission Control Protocol):传输控制协议

**UDP协议**

**特点：** 无连接、不可靠通信。

- 不事先建立连接，数据按照包发送，一包数据包含：自己的 IP、端口、目的地 IP、端口和数据（限制在 64KB 内）。
- 发送方不管对方是否在线，数据在中间丢失也不管，如果接收方收到数据也不返回确认，因此是不可靠的。

**TCP协议**

**特点：** 面向连接、可靠通信。

TCP的最终目的：要保证在不可靠的信道上实现可靠的数据传输。

TCP主要有三个步骤实现可靠传输：

1. **三次握手** 建立连接
2. 传输数据进行确认
3. **四次挥手** 断开连接

## UDP 通信

Java提供了一个`java.net.DatagramSocket`类来实现UDP通信

DatagramSocket：用于创建客户端、服务端

|构造器|说明|
|---|---|
|`public DatagramSocket()`|创建客户端的`Socket`对象，系统会随机分配一个端口号。|
|`public DatagramSocket(int port)`|创建服务端的`Socket`对象，并指定端口号。|

|方法|说明|
|---|---|
|`public void send(DatagramPacket dp)`|发送数据包|
|`public void receive(DatagramPacket p)`|使用数据包接收数据|
DatagramPacket：创建数据包

|构造器|说明|
|---|---|
|`public DatagramPacket(byte[] buf, int length, InetAddress address, int port)`|创建发出去的数据包对象|
|`public DatagramPacket(byte[] buf, int length)`|创建用来接收数据的数据包|
示例：

服务器端：

```java
public class UDPServer {  
    public static void main(String[] args) throws IOException {  
        // 创建接收端对象，注册端口  
        DatagramSocket socket = new DatagramSocket(8080);  
        // 创建一个数据包对象接受数据  
        byte[] buffer = new byte[1024 * 64];  
        DatagramPacket packet = new DatagramPacket(buffer, buffer.length);  
        // 接收数据  
        socket.receive(packet);  
        // 查看数据是否收到  
        int length = packet.getLength();  
        String data = new String(buffer, 0, length);  
        System.out.println(data);  
        // 获取对方的IP对象  
        String ip = packet.getAddress().getHostAddress();  
        int port = packet.getPort();  
        System.out.println("ip:" + ip);  
        System.out.println("port:" + port);  
    }  
}
```

客户端：

```java
public class UDPClient {  
    public static void main(String[] args) throws Exception {  
        DatagramSocket socket = new DatagramSocket();// 创建发送端对象  
        byte[] bytes = "This is a test line.".getBytes();// 创建数据包对象封装要发送的信息  
        /**  
         * Param1:发送的数据（字节数组）  
         * Param2:发送的字节长度  
         * Param3:目的地IP地址  
         * Param4:服务端程序的端口号  
         */  
        DatagramPacket packet = new DatagramPacket(bytes, bytes.length, InetAddress.getLocalHost(), 8080);  
        socket.send(packet); // 发送数据  
    }  
}
```

## TCP 通信

Java提供了一个`java.net.Socket`来实现TCP通信

|方法|说明|
|---|---|
|`public OutputStream getOutputStream()`|获得字节输出流对象|
|`public InputStream getInputStream()`|获得字节输入流对象|

| 构造器                                     | 说明                                            |
| --------------------------------------- | --------------------------------------------- |
| `public Socket(String host , int port)` | 根据指定的服务器 ip、端口号请求与服务端建立连接，连接通过，就获得了客户端 socket |
步骤：

1. 创建客户端的 `Socket` 对象，请求与服务端的连接。
2. 使用 `socket` 对象调用 `getOutputStream()` 方法得到字节输出流。
3. 使用字节输出流完成数据的发送。
4. 释放资源：关闭 `socket` 管道。

示例：

```java
public class Client {  
    public static void main(String[] args) throws IOException {  
        // 1.创建Socket管道对象，请求与服务端的Socket连接  
        Socket socket = new Socket("127.0.0.1", 9999);  
        // 2. 从Socket通信管道中得到一个字节输出流  
        OutputStream os = socket.getOutputStream();  
        // 3.创建特殊数据流  
        DataOutputStream dos = new DataOutputStream(os);  
        dos.writeInt(1); // 写出数据  
        dos.writeUTF("This is a test line.");  
        socket.close(); // 关闭  
    }  
}
```

服务端是通过`java.net`包下的`ServerSocket`类来实现的

构造器

| 构造器                     | 说明                   |
|----------------------------|------------------------|
| `public ServerSocket(int port)` | 为服务端程序注册端口 |

方法

| 方法                       | 说明                                               |
| ------------------------ | ------------------------------------------------ |
| `public Socket accept()` | 阻塞等待客户端的连接请求，一旦与某个客户端成功连接，则返回服务端这边的 `Socket` 对象。 |

步骤：

1. 创建 `ServerSocket` 对象，注册服务端端口。
2. 调用 `ServerSocket` 对象的 `accept()` 方法，等待客户端的连接，并得到 `Socket` 管道对象。
3. 通过 `Socket` 对象调用 `getInputStream()` 方法得到字节输入流，完成数据的接收。
4. 释放资源：关闭 `socket` 管道。

示例：

```java
public class Server {  
    public static void main(String[] args) throws IOException {  
        // 创建服务端ServerSocket对象，绑定端口号，监听客户端  
        ServerSocket ss = new ServerSocket(9999);  
        // 调用accept方法，阻塞等待客户端链接  
        Socket socket = ss.accept();  
        // 获取输入流，读取客户端发送的数据  
        InputStream is = socket.getInputStream();  
        // 把字节输入流包装成特殊数据输入流  
        DataInputStream dis = new DataInputStream(is);  
        // 读取数据  
        int i = dis.readInt();  
        String s = dis.readUTF();  
        System.out.println(i);  
        System.out.println(s);  
        System.out.println(socket.getInetAddress().getHostAddress());  
        System.out.println(socket.getPort());  
    }  
}
```

# 时间

时间的获取：

```java
Date date = new Date();  // 创建日期对象
System.out.println(date);  // 直接输出日期对象 Sun Jun 01 15:27:59 GMT+08:00 2025
SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss EEE a");  // 创建日期格式化对象
String result = sdf.format(date);  // 将格式化后字符串存在result中
System.out.println(result);// 2025年06月01日 15:27:59 周日 下午
```

JDK8 之后的方案：

```java
LocalDateTime now = LocalDateTime.now();  // 创建LocalDateTime对象
System.out.println(now);  // 2025-06-01T15:32:20.504079
System.out.println(now.getYear());  // 2025
System.out.println(now.getDayOfMonth());  // 1
System.out.println(now.getDayOfWeek());  // SUNDAY
System.out.println(now.getHour()); // 15
// 格式化now对象
DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss EEE a");  
String result2 = dtf.format(now);  // 2025-06-01 15:37:50 周日 下午
System.out.println(result2);
```

# StringBuilder

- StringBuilder代表可变字符串对象，相当于是一个容器，他里面装的字符串是可以改变的，就是用来操作字符串的
- 好处：StringBuilder比String更适合做字符串的修改操作，效率会更高，代码也会更简洁

### 构造器

| 构造器                                | 说明                      |
| ---------------------------------- | ----------------------- |
| `public StringBuilder()`           | 创建一个空白的可变字符串对象，不包含任何内容。 |
| `public StringBuilder(String str)` | 创建一个指定字符串内容的可变字符串对象。    |
### 方法名称

| 方法名称                                | 说明                                              |
| ----------------------------------- | ----------------------------------------------- |
| `public StringBuilder append(任意类型)` | 添加数据并返回`StringBuilder`对象本身。                     |
| `public StringBuilder reverse()`    | 将对象的内容反转。                                       |
| `public int length()`               | 返回对象内容长度。                                       |
| `public String toString()`          | 通过`toString()`就可以实现把`StringBuilder`转换为`String`。 |

# BigDecimal

- 用于解决浮点运算时，出现结果失真问题

### 构造器

| 构造器                                           | 说明                        |
| --------------------------------------------- | ------------------------- |
| `public BigDecimal(double val)`**注意：不推荐使用这个** | 将`double`转换为`BigDecimal`。 |
| `public BigDecimal(String val)`               | 把`String`转换成`BigDecimal`。 |
### 方法名

| 方法名                                                     | 说明                         |
| ------------------------------------------------------- | -------------------------- |
| `public static BigDecimal valueOf(double val)`          | 转换一个`double`成`BigDecimal`。 |
| `public BigDecimal add(BigDecimal b)`                   | 加法。                        |
| `public BigDecimal subtract(BigDecimal b)`              | 减法。                        |
| `public BigDecimal multiply(BigDecimal b)`              | 乘法。                        |
| `public BigDecimal divide(BigDecimal b)`                | 除法。                        |
| `public BigDecimal divide(另一个BigDecimal对象, 精确几位, 舍入模式)` | 除法，可以控制精确到小数几位。            |
| `public double doubleValue()`                           | 将`BigDecimal`转换为`double`。  |
```java
BigDecimal c = new BigDecimal("0.1");  // 创建BigDecimal对象
BigDecimal d = new BigDecimal("0.2");  
BigDecimal e = c.add(d);  // 执行加法
double f = e.doubleValue();  // 把BigDecimal转为Double
System.out.println(f); // 0.3
```

# Reflection 反射

- 加载类，并允许以编程的方式解剖类中的各种成分（成员变量、方法、构造器等）
---
## 反射的步骤

1. 获取类的字节码：Class对象
2. 获取类的构造器：Constructor对象
3. 获取类的成员变量：Field对象
4. 获取类的成员方法：Method对象

```java
// 1.获取类本身  
Class c1 = Student.class;  
System.out.println(c1);  //class com.fujunhao.day15.Reflection.Student
  
Class c2 = Class.forName("com.fujunhao.day15.Reflection.Student");  
System.out.println(c2);  //class com.fujunhao.day15.Reflection.Student
  
System.out.println(c1 == c2);  //true
  
Student student = new Student();  
Class c3 = student.getClass();  //class com.fujunhao.day15.Reflection.Student
System.out.println(c3);
```

## 反射获取类中的成分并操作


```java
Class c1 = Student.class;  // 获取类对象
Constructor con = c1.getDeclaredConstructor(); // 获取无参构造器  
System.out.println(con);  
Constructor[] cons = c1.getDeclaredConstructors();  //获取所有构造器
for (Constructor constructor : cons) {  
    System.out.println(constructor);  
}  
Constructor con2 = c1.getDeclaredConstructor(String.class, int.class);  // 获取指定参数构造器
System.out.println(con2);  
Field[] fields = c1.getDeclaredFields(); // 获取所有字段  
for (Field field : fields) {  
    System.out.println(field.getName() + ":" + field.getType().getName());  
}
```

详情请参考：[[反射]]

---
# 注解

## 概述

- Java中的特殊标记，让其他程序根据直接信息来决定怎么执行程序

自定义注解：

```java
public @interface A {  
    String name();  
  
    int age() default 18;  
  
    String[] address();  
}
```
---
## 元注解

### `@Target`
#### 作用

声明被修饰的注解只能在哪些位置使用。

```java
@Target(ElementType.TYPE)
```

#### `ElementType` 的常用值

1. **`TYPE`** ：类、接口。
2. **`FIELD`** ：成员变量。
3. **`METHOD`** ：成员方法。
4. **`PARAMETER`** ：方法参数。
5. **`CONSTRUCTOR`** ：构造器。
6. **`LOCAL_VARIABLE`** ：局部变量。
---
### `@Retention`

#### 作用

声明注解的保留周期。

```java
@Retention(RetentionPolicy.RUNTIME)

```
#### `RetentionPolicy` 的常用值

1. **`SOURCE`** ：
    - 只作用在源码阶段，字节码文件中不存在。
2. **`CLASS`（默认值）** ：
    - 保留到字节码文件阶段，运行阶段不存在。
3. **`RUNTIME`（开发常用）** ：
    - 一直保留到运行阶段。

---
## 注解的解析

- 就是判断类上、方法上、成员变量上是否存在注解，并把注解里的内容给解析出来
---
### 如何解析注解？

#### 指导思想：
- 要解析谁上面的注解，就应该先拿到谁。
#### 具体步骤：
1. **解析类上的注解** ：
    - 应该先获取该类的 `Class` 对象，再通过 `Class` 对象解析其上面的注解。
2. **解析成员方法上的注解** ：
    - 应该获取到该成员方法的 `Method` 对象，再通过 `Method` 对象解析其上面的注解。
#### 实现解析注解的能力：
- `Class`、`Method`、`Field`、`Constructor` 都实现了 `AnnotatedElement` 接口，它们都拥有解析注解的能力。
---

### `AnnotatedElement` 接口提供的解析注解的方法

| 方法名称                                                                    | 说明               |
| ----------------------------------------------------------------------- | ---------------- |
| `public Annotation[] getDeclaredAnnotations()`                          | 获取当前对象上面的注解。     |
| `public T getDeclaredAnnotation(Class<T> annotationClass)`              | 获取指定的注解对象。       |
| `public boolean isAnnotationPresent(Class<Annotation> annotationClass)` | 判断当前对象上是否存在某个注解。 |

详情参考[[注解]]

---

# 动态代理

详见[[代理]]
