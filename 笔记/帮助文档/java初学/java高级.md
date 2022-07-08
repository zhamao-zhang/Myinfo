

# 拔高小知识:

## lombok插件

用于生成 实体类的 getset 等等方法的插件.  

只需要在实体类上添加几个注解就行. 

偷懒神器





使用方法 

1.IDEA安装lombok插件

2.MAVEN导入jar包

3.重启IDEA





## 进制思想

进制其实 就是查数, 就是逢几进一

那么 这个 几到底是啥呢   他可以是 123456789sagavsfewrwa 中的任何数  ,甚至 可以是 @$$#$%$^%#^%# 这些 号  甚至可以是 图片  ,这需要你自己去定义.   你可以定义@为1  $为2

@+@=$  这些规则 都是要 自己去定义  .  

然后根据自己去定义好的规则 去制作自己的   乘法表 和 加法表.



![image-20210426001349674](F:\图像\typora图像保存位置\image-20210426001349674.png)

## this

this 关键字返回 当前对象的引用  

如果在对象方法中   调用同类对象的方法, 那么这个被调用的方法前面 大可不必加 this .  编译器会优先调用同类中的这个方法.

我们可以在 return  语句中 这样写.   					

```java
return this;
```

这样 会返回 当前对象的引用.   下面是一个小demo 帮助你理解.

```java
public class Dog{
	int age;
	public Dog yearAdd(){
		age++;
		return this;
	}

}


main(){
	Dog d1 = new Dog();
	d1.yearAdd().yearAdd().yearAdd().yearAdd();
}//age = 4;
```

当我们在 一个方法中 返回当前对象的引用时, 方法返回值类型 必须是一个类.

这样做 就可以很容易的做到 在一条语句中调用多个方法. 非常的便捷.



this可以将当前对象 传递给其他方法使用

如果我也能随心所欲的写出这种格式的代码 至少月薪也得两万吧. 

这么清晰的逻辑, 这么简洁的代码.   用最少的代码 干逻辑做清晰的事, 复用性还高.   

我炸毛愿称这种格式为最强.  这就是面向对象的天花板吗.

```java
public class Dog {
    public void sleep(Bed bed){
        Bed b1 = bed.getpeople();
        System.out.println("睡着了");
    }
}

public class Bed {
    public  Bed getpeople(){
        return People.makeTheBed(this);
    }
}

public class People {
    public static Bed makeTheBed(Bed bed){
        return bed;
    }
}
public void test2(){
        Dog d1 = new Dog();
        d1.sleep(new Bed());
    }
```

啊~ 被大佬叨叨了   果然是我太菜了.   随便见识一点没见过的.   其实都是大佬们看不上的.  啊 菜逼  加把劲吧. 



## lambda表达式

![image-20210424131400390](F:\图像\typora图像保存位置\image-20210424131400390.png)



lambda表达式 不是一个函数 ,而是一种方式,   先要使用此方式需要的前置条件 那就是   你想要通过 lambda表达式实现的方法 必须是一个函数式接口,   可以带参数哦

```java
 接口实现类 = ( int a , int b )->{
    //写你的代码
}; //注意这里的分号哦

接口实现类.函数式接口(参数);
```



## 关键字

final

 用于属性

1.  如果引用为基本数据类型，则该引用为常量，该值无法修改；
2.  如果引用为引用数据类型，比如对象、数组，则该对象、数组本身可以修改，但指向该对象或数组的地址的引用不能修改。
3.  如果引用时类的成员变量，则必须当场赋值，否则编译会报错

当使用final修饰方法时，这个方法将成为最终方法，无法被子类重写。但是，该方法仍然可以被继承。

用来修饰类时 ， 就不能被继承了



# 内部类

## 成员内部类

成员内部类 要定义在一个类里面 ,成员内部类可以共享  外部类的所有属性和方法.   

但是当成员内部类的属性或方法与外部类 的成员或方法同名时,调用的是成员内部类的方法或属性.    如果需要使用外部类的  则需要   

```
外部类.this.属性(方法)
```

外部类想要调用内部类的方法 需要由内部类提供相对应的函数方法,



创建实例对象时 也是需要通过方法来 ==new== 或者通过外部类 来==new==







## 局部内部类

2.局部内部类

　　局部内部类是定义在一个方法或者一个作用域里面的类，它和成员内部类的区别在于局部内部类的访问仅限于方法内或者该作用域内。

```java
class People{
    public People() {
         
    }
}
 
class Man{
    public Man(){
         
    }
     
    public People getWoman(){
        class Woman extends People{   //局部内部类
            int age =0;
        }
        return new Woman();
    }
}
```

　　注意，局部内部类就像是方法里面的一个局部变量一样，是不能有public、protected、private以及static修饰符的。



# 多线程

## 创建一个线程

### 方法一:

创建一个子类 继承Thread类

在子类中创建run方法

![image-20201126171941879](F:\图像\typora图像保存位置\image-20201126171941879.png)

在run方法中 写该线程要跑的代码.

### 方法二

创建一个子类 接通Runnable接口, 

重写接口中的run方法.

在主程序中 实例化一个子类.  

实例化一个Thread类 ,将子类传进Thread类中. 



## 线程使用方法

### 1.**start();**

根据创建的线程子类 来实例化对象    调用实例化对象中的start方法来启动线程.

### 2.currentThread(); 

返回当前代码的线程

### 3.getName();

返回当前线程的名字

### 4.setName();

设置当前线程的名字

### 5.yield();

释放当前CPU的执行权, 然后线程们再重新争夺. 有可能还抢到了,有可能被夺去

### 6.join();

在线程a中调用线程b的join(),此时线程a就会进入阻塞状态, 知道线程b完全执行完以后,线程a才会结束阻塞状态

### 7.stop(); 已过时

调用此方法直接让该线程去世.  当场就gg了 非常惨.

### 8.sleep(Long  milltime); 

让当前线程睡眠指定的毫秒数. 在睡眠时间内,该线程的状态为 **阻塞**

### 9.isAlive();

判断当前线程是否存活.

### 10.setdaemon();

设置是否为守护线程,  true  or  false

守护线程不需要等到他执行结束.

## 线程的优先级

最高优先级: MAX_PRIORITY :10

最低优先级:MIN_PRIORITY:1

默认优先级:NORM_PRIORITY:5



优先级的高低,其实只是概率问题 并不绝对 ,并不是说 你优先级高就一定先执行你, 只是执行你的概率比较大.   实质线程们还是在抢cpu执行权.



## 线程的生命周期

看图不多bb, 详细了解就去看书.

![image-20201126212614879](F:\图像\typora图像保存位置\image-20201126212614879.png)







## 线程的安全问题

### 实现线程的暂停

```java
/*
	我们一般会提供一个 方法     这个方法会将线程的运行条件 给更改 从而达到 暂停线程的效果.
*/


```

### 线程的状态

![image-20210424192802214](F:\图像\typora图像保存位置\image-20210424192802214.png)





### 线程同步监视器

```java
synchronized(放入要被锁的对象){

	//放入要执行的代码

}
//我们一般会锁住 需要操作的对象,  也就是这个对象中的数据需要进行 增删改的时候. 我们就要锁了.
synchronized 
//也可以添加在函数声明时, 这样这个对象就会被锁住.

```



synchronized是一个关键字 ,添加了这个关键字的方法会成为同步方法, 也就是同一时间 只有一个对象可以执行该方法.

![image-20210425130925430](F:\图像\typora图像保存位置\image-20210425130925430.png)

使用同步监视器会降低线程的性能.

### 死锁

死锁就是两个人 互相锁着对方下一步需要使用的资源, 导致程序无法向下进行 ,僵持在原地了.

这里要注意几个误区,    对方要使用的资源 一定要是同一个资源.  

例如下图中的代码所示,    两个女生都要使用同一个口红 和 同一个镜子   但是如果他们使用的如果分别是 口红1 口红2    就无法造成冲突.    

 

![image-20210425132630098](F:\图像\typora图像保存位置\image-20210425132630098.png)





### 生产者消费者问题

解决问题思路: 

生产者是一个类, 消费者是一个类 , 

 如果再由一个缓冲区 供生产者生产,消费者消费 就可以很简单的解决问题.

![image-20210425204903424](F:\图像\typora图像保存位置\image-20210425204903424.png)







![image-20210425202141904](F:\图像\typora图像保存位置\image-20210425202141904.png)

有时间去了解 下面这三个 包     貌似 object 已经不用了

![img](F:\图像\typora图像保存位置\Q_H%UL86`9MZ@WZAOPLO$AA.jpg)





```java
//缓冲区类
public class huanchongqu {
    private fangbianmian[] fangbianmians = new fangbianmian[9];
    private int jishuqi=0;

    //生产方便面的方法
    public synchronized void shengchan(fangbianmian fangbianmian){
        //判断缓冲区是否已满.
        if (jishuqi==fangbianmians.length)
        {
            try {
                //满了之后,通知生产者等待.
                this.wait();//释放锁,
//                this.notifyAll();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        //生产者存放方便面
        fangbianmians[jishuqi] = fangbianmian;
        jishuqi++;

        //通知消费者消费   让调用了 wait()方法的类重新获得锁
        this.notifyAll();

    }


    //消费方便面的方法
    public synchronized fangbianmian pop(){
        if (jishuqi==0){
            try {
                this.wait();
//                this.notifyAll();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        jishuqi--;
        fangbianmian fangbianmian = fangbianmians[jishuqi];

        //吃完了,通知生产者生产
        this.notifyAll();
        return fangbianmian;

    }
}





//------------生产者 
public class shengchanzhe extends Thread {
    huanchongqu hcq;

    public shengchanzhe(huanchongqu hcq) {
        this.hcq = hcq;
    }

    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println("生产了"+i+"只包方便面");
            hcq.shengchan(new fangbianmian(i));

        }
    }
}
//------------消费者 
public class xiaofeizhe extends Thread {
    huanchongqu hcq;

    public xiaofeizhe(huanchongqu hcq) {
        this.hcq = hcq;
    }

    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            System.out.println("消费了第"+hcq.pop().getID()+"包方便面");
        }
    }
}


//-----------test
    public class test {
    public static void main(String[] args) {
        huanchongqu hcq =new huanchongqu();
        new shengchanzhe(hcq).start();
        new xiaofeizhe(hcq).start();
    }
}

```



























































































# 常用类

## String类(不可变的)

### String类基本概念

1.是一个final类,代表内容不可变. 也就是说 String定义的是常量.

2.String对象的字符内容是存储在一个字符数组(char) value[]中的

**去你妈的 查看api帮助文档去  老子不写了.**

## StringBuffer类(可变的,线程安全的,效率底)

### 概念

是一个可变的字符序列类,

## 方法

### int lastindexof()

返回这个字符所在的**数组**索引下标,

###  String substring() 

开始索引(包括),结束索引(不包括);

传入一个下标,从这个下标开始往后截.







## System类

```
//利用System 获取时间戳  返回现在距1970年1月1日0时0分0秒时间差的毫秒数.
    public void p(){
        long a = System.currentTimeMillis();
        System.out.println(a);
    }
```

































# 泛型

## 泛型语法: 

### 定义基本的泛型类

```java
class Pair<T> {
    private T first;//属性
    private T second;

    public Pair() {
        first = null;
        second = null;
    }

    public Pair(T first, T second) {
        this.first = first;
        this.second = second;
    }

    public T getFirst() {
        return first;
    }

    public void setFirst(T first) {
        this.first = first;
    }

    public T getSecond() {
        return second;
    }

    public void setSecond(T second) {
        this.second = second;
    }
}
```

### 定义泛型方法

```java
//泛型方法  类型变量放在修饰符后面 ,返回类型前面. 类型变量可以通过extends关键字来限制传入参数.''
    public static <T extends Comparable> Pair minmax(T[] a)
    {
        if (a == null || a.length == 0) return null;
        T min = a[0];
        T max = a[0];
        for (int i = 1; i < a.length; i++) {
            if(min.compareTo(a[i])>0)//compareTo 按字段顺序比较字符串 , 如果当前字符串 比  参数字符串 靠后 则为正整数.
//                                      反之, 则返回一个负整数.  如果两个字符串相等则返回零
                min = a[i];
            if(max.compareTo(a[i])<0)
                max = a[i];
        }
        return new Pair<>(min,max);
    }
```

```java
<T extends Comparable & String> 
//限制条件可以是多个 中间用'&'符连接
```



## (个人) 深入理解泛型

```java
/**
 * @author: 炸毛
 * @date: 2020/12/4 14:35
 * @exception: 类作用:java核心技术卷一  p332~p333 程序清单 8-2(并不)   我自己突发奇想自己玩了一会儿.下面 写一下思想过程
 *设计一个可以返回泛型数组的最大值,与最小值的泛型方法,并测试
 * 我操尼玛 有点难啊.
 *
 * 试着传进int类型 但是想到 只能穿进去一个类, 于是设计了一个包含int类型变量的类.
 * 接着发现无论如何int1类也不能作为minmax函数的参数   ,就想到了 限制条件限制参数必须有Comparable接口.
 * 再添加了Comparable接口后 , 在输出会输出类的地址. 于是又重写了int1类的 toString方法. 这才能输出值.
 * 但是 我发现输出的值并不准确.
 *
 * 总结:设计思想一开始就出现了错误,  如果只是基本类型,只需要设计更简单的方法就行了么必要搞这么复杂.
 *      此方法终究是将两个对象作为比较的,而不是比较基本数据类型.
 *      运行结果不理想 一定与重写的 toString方法有关 , 也与compareTo方法有关.
 * 反思:从错误的角度出发 只会是问题变得更复杂, 或许我深究之后可以找到解决问题的办法,但是就目前来看 以我的技术 还不足以
 *      支撑我的奇思妙想.  所以在实际开发中 一定要用正确的思路来设计方法和类.
 *
 */
public class PairTest2 {
    public static void main(String[] args) {
        int1[] a1 = {new int1(262),new int1(156),new int1(65461),new int1(23),new int1(24),new int1(9),new int1(65),new int1(941)};
        Pair<int1> mm = ArrayAlg1.minmax(a1);
        System.out.println("mm.getFirst() = " + mm.getFirst());
        System.out.println("mm.getSecond() = " + mm.getSecond());

    }
}
class ArrayAlg1{
    public static <T extends Comparable> Pair <T>minmax(T[] a )
    {
        if (a.length == 0 || a==null) return null;
        T min = a[0];
        T max = a[0];
        for (int i = 1; i<a.length;i++)
        {
            if (min.compareTo(a[i])>0) min = a[i];//其实这里是吧a[i]的toString 赋值给了min max
            if (max.compareTo(a[i])<1) max = a[i];
        }       //new 一个Pair对象 new的同时 调用的 Pair的带参构造函数.
        return  new Pair <> (min,max);//这样构造出来的函数, 里面的属性 实质上还是 String类型
    }


}
```

```java
//这是上面代码中的 int1 类 源代码
public class int1 implements Comparable{
    private int a;

    public int1(int a) {
        this.a = a;
    }


    @Override
    public int compareTo(Object o) {
        return a;
    }

    @Override
    public String toString() {
        return "int1{" +
                "a=" + a +
                '}';
    }
}
```



























































































# I/O流

## 缓冲区传输文件

```java
        //4.获取文件下载流
        FileInputStream in = new FileInputStream(file);
        //5.设置缓冲区
        int len = 0;
        byte[] buffer = new byte[1024];
        //6.获取输出流对象
        ServletOutputStream out = resp.getOutputStream();
        //7.将文件输入流的数据 用 servlet输出流输出
        while((len=in.read(buffer))>0)
        {
            out.write(buffer,0,len);
        }
```









# JDBC

## 环境搭建

引入对应数据库的 .jar包,  里面有对应的jdbc实现类.



## 实现连接

```java
//下面三个 静态变量是 URL : 链接数据库地址
// 				   USER: 用户名
//				   PASSWORD: 用户密码
public static final String URL = "jdbc:mysql://localhost:3306/student";
    public static final String USER = "root";
    public static final String PASSWORD = "255740";
    public static void main(String[] args) throws Exception{
       //此为固定格式, 表明下面将要链接mysql数据库
        Class.forName("com.mysql.jdbc.Driver");
        //用一个 connection 接受 数据库的地址,用户,密码  正式建立连接
        Connection connection = DriverManager.getConnection(URL,USER,PASSWORD);
        //从建立的连接中获取操作数据对象
        Statement statement = connection.createStatement();
        //接受数据对象查询到的数据.    
        				
        ResultSet resultSet =statement.executeQuery("SELECT * FROM  info");//这个函数接受一个String类型参数, 内容为SQL查询语句.
        while (resultSet.next())
        {
            int id = resultSet.getInt(1);
            String name = resultSet.getString(2);
            int age = resultSet.getInt(3);
            System.out.println("ID:"+id+" 名字:"+name+" 年龄:"+age);
        }
```

​	





## 优化(封装)

配置 配置文件 aa.properties

```properties
url=jdbc:mysql://localhost:3306/student?characterEncoding=utf8
user=root
password=255740
driver=com.mysql.jdbc.Driver
```



```java
public class JDBCpackage {
    private static String driver;
    private static String url;
    private static String user;
    private static String password;
    static {
        try {
            //输入流读取配置文件内容
            BufferedReader bufferedReader = new BufferedReader(new FileReader("E:\\projact\\java\\java_IDEA\\java进阶\\java核心技术练习\\Frank练习\\src\\com\\zhamao\\jdbc\\db.properties"));
//            InputStream in = JDBCpackage.class.getClassLoader().getResourceAsStream("E:\\projact\\java\\java_IDEA\\java进阶\\java核心技术练习\\Frank练习\\src\\com\\zhamao\\jdbc\\db.properties");
            //我也不知道为什么 反正就是不通过 不管了 反射之类的玩意儿俺玩不懂.
            Properties properties = new Properties();
            properties.load(bufferedReader);//将字节流加载到 porperties类中
            driver = properties.getProperty("driver");//getProperty方法 查找对应的键对值并返回.
            url = properties.getProperty("url");
            user = properties.getProperty("user");
            password = properties.getProperty("password");
//            System.out.println("静态代码块加载!");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static void test(){
        System.out.println("测试!");
    }
    //  通过单例模式 , 设计与数据库建立链接的方法.
    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection(url,user,password);
    }
    //关闭链接方法.
    public static void close(Connection connection, PreparedStatement preparedStatement) throws SQLException {
        if (preparedStatement != null) {
            preparedStatement.close();
        }
        if (connection!= null) {
            connection.close();
        }
    }
    public static void close(Connection connection, PreparedStatement preparedStatement, ResultSet resultSet) throws SQLException {
        if (resultSet!= null){
            resultSet.close();
        }
        if (preparedStatement != null) {
            preparedStatement.close();
        }
        if (connection!= null) {
            connection.close();
        }
    }
}
```





```java
    public static Connection connection;
    public static PreparedStatement preparedStatement;

    public static ArrayList<Student> selectAll() {
        ArrayList<Student> arrayList = new ArrayList<>();
        try {
            // JDBCUtils.getConnection(),会返回一个数据库链接   这里我们要用此类的connection接受获取得到的数据库链接
            connection = JDBCUtils.getConnection();

            String sql = "select * from info";
            /* connection.prepareStatement(sql)方法会加载一条sql语句, 并且返回一个 prepareStatement 类
               我们需要用一个 prepareStatement 类来接受 这次加载,
               
               ResultSet	接受数据库sql语句执行完毕的返回结果.
               
            */
            preparedStatement = connection.prepareStatement(sql);
							//prepareStatement有各种sql语句的执行方法,调用对应方法可以执行已经加载的sql语句
            ResultSet res = preparedStatement.executeQuery();
```



```java
			String sql = "delete from info where id=?";
			preparedStatement = connection.prepareStatement(sql);
//			这里解释一下这种类型方法,  这个 1  值得是上面 sql语句里的第几个问号, id是一个int类型的值,  因为代码我没有截取完整 其实这个id一个int类型的变量.       如果我们要把?变成指定的字符串等类型的值,    只需要在该方法的第二个参数位置,传进对应的值就行了.
			preparedStatement.setInt(1, id);   
```







## 根据用户输入操作数据

这里引入?的概念,  在事先准备到的sql语句中写入?

然后用preparedStatement.setInt();  把?改成对应的int类型值

​		   preparedStatement.setString();  改为对应的String值

两个方法来改变sql语句中?所代表的值.

```java
  connection = JDBCpackage.getConnection();
            String sql = "select * from info where id=?" ;
            preparedStatement = connection.prepareStatement(sql);
//注:这条语句一定要在 下面这条语句的上面 ,否则程序会报错
            preparedStatement.setInt(1,id);
            resultSet = preparedStatement.executeQuery();
```





# 网络编程

## 客户端

客户端上传文件 代码

```java
import java.io.*;
import java.net.Socket;

/**
 * @author: 炸毛
 * @date: 2021/1/16 10:19
 * @exception: 类作用:
 */
public class Clinet {
    public static void run() throws IOException {
        //要上传的文件地址
        FileInputStream file = new FileInputStream("E:\\projact\\java\\java_IDEA\\java进阶\\java核心技术练习\\Frank练习\\file\\123.jpg");
        // 新建一个客户端,  网络地址为本机地址, 端口号为 9999
        Socket s = new Socket("127.0.0.1",9999);
        //创建一个输出流, 获取  客户端的网络输出流中的信息
        OutputStream os = s.getOutputStream();
        //缓冲流
        int a = 0;
        byte[] bytes = new byte[1024];
        // 读取,文件输入流中的信息,   直到读取到文件结尾标记
        while ((a = file.read(bytes))!= -1){
            //注意 while 判定条件是 文件输入流是否读取到文件结尾标记,如果读取到就终止循环
            //读取到之后, 输出流 并不会吧文件结尾标记 也写入输出流中, 所以 该缓冲流输出内容 没有文件结尾标记
            //所以会发生,文件阻塞现象.  服务器那边 将会出现文件输入流读取不到 文件结尾标记  而一直读取的死循环.
            os.write(bytes,0,a);
        }
        // 告诉服务器 已经上传结束了.  给出输出流添加一个文件上传结束标记.
        s.shutdownOutput();//有了这个 就可以避免文件阻塞现象的发生.

        file.close();
        s.close();
    }
}
```



## 服务器

接受客户端上传文件 代码

```java
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.Random;

/**
 * @author: 炸毛
 * @date: 2021/1/16 10:19
 * @exception: 类作用:
 */
public class Server {
    public static void main(String[] args) throws IOException {
        //新建一个服务器, 端口号为9999
        ServerSocket server = new ServerSocket(9999);

        new Thread(new Runnable() {
            @Override
            public void run() {
               try{ while (true) {
                   // 获取一个客户端信息
                    Socket socket = server.accept();
                    // 获取该客户端 的网络输入流.  
                    InputStream is = socket.getInputStream();
                    //判断该文件夹是否存在 不存在就创建
                    File file = new File("F:\\ServerFile\\imp");
                    if (!file.exists()) {
                        file.mkdir();
                    }
                    // 一个文件输出流 , 输出地址为 文件地址+当前时间戳+一个六位随机数+后缀名
                    FileOutputStream fos = new FileOutputStream(file + "\\" + System.currentTimeMillis() + new Random().nextInt(999999) + ".jpg");
                    // 缓冲流  读取输入流 内的 客户端网络输入流中的信息   并 用文件输出流 进行输出.
                    byte[] bytes = new byte[1024];
                    int a = 0;
                    while ((a = is.read(bytes)) != -1) {
                        fos.write(bytes);
                    }
                    //文件上传完毕 , 关闭资源.
                    fos.close();
                    socket.close();
                }
            } catch (IOException e){
                e.printStackTrace();
               }
            }
        }).start();


    }
}
```



















































# 一些类

## Runtime

runtime类可以告诉我们程序运行 消耗了多少内存.

totalMemory()   告诉我们总内存大小.

freeMemory()	告诉我们剩余内存大小.





























































































































































































































































































