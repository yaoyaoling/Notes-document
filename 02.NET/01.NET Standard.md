# 一. 值类型和引用类型

**1. 前言**

- 分类

　　值类型包括：布尔类型、浮点类型(float、double、decimal、byte)、字符类型(char)、整型（int、long、short等）、枚举(entum)、结构体(struct)。

　　引用类型：数组、字符串(string)、类、接口、委托(delegate)。 

- 内存存储

　　值类型数据存放在栈stack中， 引用类型地址存放栈stack中，数据存放在堆heap中。

　　值类型变量声明后，不管是否赋值，都会在在栈中分配内存空间。引用类型声明时，只在栈中分配内存，用于存放地址，并没有在堆上分配内存空间。

**2. 对象的传递**

- 将值类型的变量赋值给另一个变量，会执行一次赋值，赋值变量包含的值。

- 将引用类型的变量赋值给另一个引用类型变量，它复制的是引用对象的内存地址，在赋值后就会多个变量指向同一个引用对象实例。

  **示例代码**

  ```c#
  Console.WriteLine("------------------------下面是值类型和引用类型赋值-----------------------------");
  //值类型赋值
  int a = 0;
  int b = a;
  Console.WriteLine($"默认值： a={a},b={b}");
  a = 1;
  Console.WriteLine($"修改a的值后： a={a},b={b}");
  b = 2;
  Console.WriteLine($"修改b的值后： a={a},b={b}");
  
  //引用类型赋值
  Student stu1 = new Student();
  stu1.age = 20;
  Student stu2 = stu1;
  Console.WriteLine($"默认值： stu1.age={ stu1.age}, stu2.age={stu2.age}");
  stu1.age = 30;
  Console.WriteLine($"修改stu1.age的值后：stu1.age={ stu1.age}, stu2.age={stu2.age}");
  stu2.age = 40;
  Console.WriteLine($"修改stu2.age的值后： stu1.age={ stu1.age}, stu2.age={stu2.age}");
  ```

**3. 参数按值传递**

- 对于值类型(age)，传递的是该值类型实例的一个副本，因此原本的值age并没有改变。

- 对于引用类型(Student stu)，传递是变量stu的引用地址（即stu对象实例的内存地址）拷贝副本，因此他们操作都是同一个stu对象实例。

  **示例代码**

  ```c#
  {
      Console.WriteLine("------------------------下面是参数按值传递-----------------------------");
      //值类型按值传递
      int age1 = 60;
      Utils.AddAge1(age1);
      Console.WriteLine($"age={age1}");
  
      //引用类型按值传递
      Student stu2 = new Student();
      stu2.age = 100;
      Utils.ReduceAge1(stu2);
      Console.WriteLine($"age={stu2.age}");
  }
  public class Utils
  {
      public static void ReduceAge1(Student stu)
      {
          stu.age -= 10;
          Console.WriteLine($"ReduceAge  age={stu.age}");
      }
      public static void AddAge1(int age)
      {
          age += 10;
          Console.WriteLine($"AddAge age ={age}");
      }
      public static void ReduceAge2(ref Student stu)
      {
          stu.age -= 10;
          Console.WriteLine($"ReduceAge  age={stu.age}");
      }
      public static void AddAge2(ref int age)
      {
          age += 10;
          Console.WriteLine($"AddAge age ={age}");
      }
  }
  ```


**4. 参数按引用类型传递**

- 不管是值类型还是引用类型，可以使用ref或out关键字来实现参数的按引用传递。ref或out关键字告诉编译器，方法传递的是参数地址，而非参数本身。在按引用传递时，方法的定义和调用都必须显式的使用ref或out关键字，不可以省略，否则会引起编译错误。

  **代码分享：**

  ```c#
  {
      Console.WriteLine("------------------------下面是参数按引用传递-----------------------------");
      //值类型按值传递
      int age1 = 60;
      Utils.AddAge2(ref age1);
      Console.WriteLine($"age={age1}");
  
      //引用类型按值传递
      Student stu2 = new Student();
      stu2.age = 100;
      Utils.ReduceAge2(ref stu2);
      Console.WriteLine($"age={stu2.age}");
  }
  public class Utils
  {
      public static void ReduceAge1(Student stu)
      {
          stu.age -= 10;
          Console.WriteLine($"ReduceAge  age={stu.age}");
      }
      public static void AddAge1(int age)
      {
          age += 10;
          Console.WriteLine($"AddAge age ={age}");
      }
      public static void ReduceAge2(ref Student stu)
      {
          stu.age -= 10;
          Console.WriteLine($"ReduceAge  age={stu.age}");
      }
      public static void AddAge2(ref int age)
      {
          age += 10;
          Console.WriteLine($"AddAge age ={age}");
      }
  }
  ```

**5. string和其它引用类型的区别**

- 在string字符串，一开始s1地址指向是ypf，因为s2=s1，所以s2地址也同样指向ypf；当s1再次赋值lmr时，堆中就会开辟出数据lmr，而且ypf没有消失，没有被覆盖。s1地址就指向lmr，s2地址还是原来的ypf。

- 在引用类型数组上，一开始arry1和arry2的地址都指向{1,2,3}，当给arry1进行数据更改时，由于是引用类型，所以在{1,2,3}上面进行更改，就会对arry2进行覆盖。

  **示例代码：**

  ```c#
  {
      Console.WriteLine("------------------------下面是string和其它引用类型的区别-----------------------------");
      //string类型的测试
      string s1 = "ypf";
      string s2 = s1;
      Console.WriteLine($"s1={s1},s2={s2}");
      //修改s1的值
      s1 = "lmr";
      Console.WriteLine($"s1={s1},s2={s2}");
  
      //其它引用类型的测试
      int[] arry1 = new int[] { 1, 2, 3 };
      int[] arry2 = arry1;
      Console.WriteLine($"默认值：arry1[0]={arry1[0]},arry1[1]={arry1[1]},arry1[2]={arry1[2]}");
      Console.WriteLine($"默认值：arry2[0]={arry2[0]},arry2[1]={arry2[1]},arry2[2]={arry2[2]}");
  
      arry1[2] = 0;
      Console.WriteLine($"修改后：arry1[0]={arry1[0]},arry1[1]={arry1[1]},arry1[2]={arry1[2]}");
      Console.WriteLine($"修改后：arry2[0]={arry2[0]},arry2[1]={arry2[1]},arry2[2]={arry2[2]}");
  }
  ```

  **运行结果**

  ![image-20220424073648011](C:\Users\xzzha\AppData\Roaming\Typora\typora-user-images\image-20220424073648011.png)
  
  **string变化图如下：**
  
  ![image-20220424073824135](C:\Users\xzzha\AppData\Roaming\Typora\typora-user-images\image-20220424073824135.png)
  
  **Array类型变化图如下：**
  
  ![image-20220424073945737](C:\Users\xzzha\AppData\Roaming\Typora\typora-user-images\image-20220424073945737.png)

**6. 拆箱和装箱**

　装箱是值类型向引用类型转换时发生的，拆箱是引用类型向值类型转换时发生的。装箱是隐式的，拆箱是显式的

```c#
{
                    Console.WriteLine("------------------------下面是拆箱和装箱-----------------------------");
                    int a = 123;
                    object obj = a;  //装箱(隐式)
                    Console.WriteLine($"装箱后的结果obj={obj}");

                    int b = (int)obj; //拆箱(显式)
                    Console.WriteLine($"拆箱后的结果b={b}");
}
```

**7. 总结**

- 值类型有更好的效率，但不支持多态，适合用作存储数据的载体。而引用类型支持多态，适合用于定义程序的行为。

- 引用类型可以派生新的类型，而值类型不能。



# 二. 深拷贝和浅拷贝

**1.浅拷贝**

　创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。如果属性是值类型和string类型，拷贝的就是基本类型的值；如果属性是引用类型，拷贝的就是内存地址（string类型除外），所以修改其中一个对象，就会影响到另一个对象。

**2.深拷贝**

　将一个对象从内存中完整的拷贝一份出来,从堆内存中开辟一个新的区域存放新对象,且修改新对象和原对象的修改不会相互影响.

**3.二者区别**

​	最根本的区别在于是否真正获取一个对象的复制实体,而不是引用,假设B复制了A，修改A的时候，看B是否发生变化：

- 如果B跟着也变了，说明是浅拷贝，拿人手短！（修改堆内存中的同一个值）

- 如果B没有改变，说明是深拷贝，自食其力！（修改堆内存中的不同的值）

​	**简单的来说：**

​	如果拷贝的时候共享被引用的对象就是浅拷贝，如果被引用的对象也拷贝一份出来就是深拷贝。（深拷贝就是说重新new一个对象，然后把之前的那个对象的属性值在重新赋值给这个用户）

**4.总结**

- 对于浅拷贝：所有值类型和string这个引用类型修改其中一个对象的值,不相互影响; 除了string以外的引用类型都相互影响; 类属于引用类型,修改类中的一个属性值，被拷贝的另一个对象的属性值也会发生变化(与类中的属性值是什么类型没有关系).

- 对于深拷贝：无论是值类型还是引用类型, 修改其中一个对象的值都不会相互影响。

- 

# 三. virtual & abstract & Interface

**1.虚函数（Virtual），抽象函数（abstract）和接口的区别**

- virtual：允许被重写，但不强制要求。声明时提供其自身实现；

- abstract：强制要求其继承者重写。声明时不提供其自身的实现，抽象类不能被实例化；

- interface：接口就是协议，其声明的成员（属性，方法，事件和索引器）必须由其继承的类实现。接口不能直接被实例化。

  虚方法与抽象方法的区别在于，虚方法提供自身的实现，并且不强制要求子类重写；而抽象方法不提供自身的实现，并且强制子类重写。

  抽象类与接口很相似，但是思路不一样。接口是公开类的成员，而抽象类则是抽象类成员以要求子类继承并实现。

  **抽象类和接口**

  ```
  相同点：
  (1) 都可以被继承
  (2) 都不能被实例化
  (3) 都可以包含方法声明
  (4) 派生类必须实现未实现的方法
  区 别：
  (1) 抽象基类可以定义字段、属性、方法实现。接口只能定义属性、索引器、事件、和方法声明，不能包含字段。
  (2) 抽象类是一个不完整的类，需要进一步细化，而接口是一个行为规范。微软的自定义接口总是后带able字段，证明其是表述一类“我能做。。。”
  (3) 接口可以被多重实现，抽象类只能被单一继承
  (4) 抽象类更多的是定义在一系列紧密相关的类间，而接口大多数是关系疏松但都实现某一功能的类中
  (5) 抽象类是从一系列相关对象中抽象出来的概念， 因此反映的是事物的内部共性；接口是为了满足外部调用而定义的一个功能约定， 因此反映的是事物的外部特性
  (6) 接口基本上不具备继承的任何具体特点,它仅仅承诺了能够调用的方法    
  (7) 接口可以用于支持回调,而继承并不具备这个特点
  (8) 抽象类实现的具体方法默认为虚的，但实现接口的类中的接口方法却默认为非虚的，当然您也可以声明为虚的 
  (9) 如果抽象类实现接口，则可以把接口中方法映射到抽象类中作为抽象方法而不必实现，而在抽象类的子类中实现接口中方法
  ```

**2.应用场景实例：**
我们定义一个水果类和蔬菜类，其中水果类包含各种的水果，蔬菜类包含各种蔬菜。
问题：按照常理，卖水果的直接引用水果类，卖蔬菜的引用蔬菜类。当有家超市既卖水果又卖蔬菜。这时我们就需要用到接口来实现。
以下列出接口和抽象类代码例子：

- 抽象类：基类只能继承一个父类 （卖水果的只能卖水果，卖蔬菜的只能卖蔬菜。）

  ```c#
  public abstract  class IFruits
  {
      public abstract string apple();
  }
  public abstract class IVegetables
  {
      public abstract string potato();
  }
  public class Fruits : IFruits
  {
      public override string apple()
      {
          throw new NotImplementedException();
      }
  }
  public class Vegetables : IVegetables
  {
      public override string potato()
      {
          throw new NotImplementedException();
      }
  }
  ```

- 接口：类可以引用多个接口（一个商店可以同时可以卖蔬菜和水果。）

  ```c#
  public interface   IFruits
  {
      string apple();
  }
  public interface IVegetables
  {
      string potato();
  }
  public class Shop : IFruits, IVegetables
  {
      public string apple()
      {
          throw new NotImplementedException();
      }
      public string potato()
      {
          throw new NotImplementedException();
      }
  }
  ```
