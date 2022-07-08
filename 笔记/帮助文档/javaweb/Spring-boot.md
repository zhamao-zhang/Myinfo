# Spring-boot

## 版本 2.6.4

本笔记所写的所有内容,只代表当前版本, 可能将来源码有了改动后,就不再是这样了. 所以,源码代表了怎么样做才可以达到这样的效果.

而不是别人做的讲解,别人讲的知识.   注意锻炼读源码能力,而不是盲目的等别人教





## 遇到的一些问题

### 服务器启动不了

会爆这个错误

```java
	at com.zhamao.SpringbootApplication.main(SpringbootApplication.java:10) ~[classes/:na]
Caused by: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'tomcatServletWebServerFactory' defined in class path resource [org/springframework/boot/autoconfigure/web/servlet/ServletWebServerFactoryConfiguration$EmbeddedTomcat.class]: Initialization of bean failed; nested exception is java.lang.IllegalArgumentException: ContextPath must start with '/' and not end with '/'
	
```

解决方案

解析包路径忘记加"/"

```yaml
错误示例
server:
  servlet:
    context-path: zhamao
正确示例   
server:
  servlet:
    context-path: /zhamao
```



### Controller 返回原页面导致无法加载静态资源

![image-20220403151007865](F:\图像\typora图像保存位置\image-20220403151007865.png)这是目录环境

出问题代码

```html
		<link th:href="@{asserts/css/bootstrap.min.css}" rel="stylesheet">
		<!-- Custom styles for this template -->
		<link th:href="@{asserts/css/signin.css}" rel="stylesheet">
```

```java
@Controller
public class LoginController {

    @RequestMapping("/user/login")
    public String login(@RequestParam("username") String username, @RequestParam("password") String password, Model model){

        if(username.equals("2557402806")&&password.equals("123456")){
            User user=new User("1",username,password);

            if (user!=null){
                return "redirect:/main.html";
            }else {
                model.addAttribute("msg","该账户不存在,请从新登录.");
                return "index";
            }
        }else {

            model.addAttribute("msg","账号或密码有错,请检验输入.");
            return "index";
        }
    }
}
//------------------------------------------
@Configuration
public class MyMvcConfig implements WebMvcConfigurer {

    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        registry.addViewController("/").setViewName("index");
        registry.addViewController("/index.html").setViewName("index");
        registry.addViewController("/main.html").setViewName("dashboard");
        registry.addViewController("/list.html").setViewName("list");
    }
}
```

![image-20220403151138617](F:\图像\typora图像保存位置\image-20220403151138617.png)![image-20220403151159902](F:\图像\typora图像保存位置\image-20220403151159902.png)

出错原因, 静态资源出现404也就是找不到该资源的错误.  

原因是表单提交到 controller 导致访问路径变成 /user/login,  我们的th:表达式给静态资源配置的路径是相对路径 ,这样他就会去  /user/login目录下去找/静态资源, 上图中可以看到,资源并不在这个地方, 所以我们要把,th表达式中的相对路径 改成绝对路径.

![image-20220403151507837](F:\图像\typora图像保存位置\image-20220403151507837.png)

这样在url地址栏有变动的情况下, 仍旧可以精准获取到对应的静态资源.



我们也可以通过重定向![image-20220403151631502](F:\图像\typora图像保存位置\image-20220403151631502.png)来保证url栏没有变动, 但是这样也会导致我们失去传递的参数,达不到给用户提醒输入错误的效果.



## 初体验

### idea建立项目 

![image-20220324122756650](F:\图像\typora图像保存位置\image-20220324122756650.png)

![image-20220324122912656](F:\图像\typora图像保存位置\image-20220324122912656.png)



### 目录结构

![image-20220324123018048](F:\图像\typora图像保存位置\image-20220324123018048.png)



### 导包

```xml
<!--web支持-->
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-web</artifactId>
</dependency>
```



### application.properties

```properties
#更改服务端口号
server.port=4396
```

### banner.txt 更改启动logo

```txt
https://www.bootschool.net/ascii-art;bsid=B7D3171B4B289549478D59C0F775CF99
```







## 核心

### 多个配置文件加载优先级

这里的file  指的是项目的根目录  

​			classpath指的是 ![image-20220325164453461](F:\图像\typora图像保存位置\image-20220325164453461.png)这里

![image-20220325164415120](F:\图像\typora图像保存位置\image-20220325164415120.png)

yaml一个文件达成多个文件的效果  

使用 ---  来分隔文件  

```yml
spring:
	profiles: 文件名
		active: 选取的文件
```



​			



![image-20220325165450724](F:\图像\typora图像保存位置\image-20220325165450724.png)



### 解析@SpringBootApplication

```java
@SpringBootApplication	//标注到类上,表示他是一个SpringBoot应用
public class SpringbootApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootApplication.class, args);
    }

}
```



解析@SpringBootApplication

```java
@SpringBootApplication
	@SpringBootConfiguration
		@Configuration		//中文意思为  "配置"
			
	@EnableAutoConfiguration	//自动装配配置
		@AutoConfigurationPackage
			@Import({Registrar.class})//默认情况下，就是将主配置类（@SpringBootApplication）所在的包以及子包里的组件扫描到容器中。
		@Import({AutoConfigurationImportSelector.class})//自动配置导入选择器  里面有一个getAutoConfigurationEntry方法 (自动获取配置条目)   会在META-INF/spring.factories中寻找配置类  
```



AutoConfigurationImportSelector.class 类中 有一个 getAutoConfigurationEntry() 方法  这个方法调用了一大堆本类的加载器

![image-20220325011857627](F:\图像\typora图像保存位置\image-20220325011857627.png)

点开这个会发现  是这个方法返回了它要自重装配的 组件信息  SpringFactoriesLoader.loadFactoryNames() 点开这个方法我们会发现,它

```java
protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
    List<String> configurations = SpringFactoriesLoader.loadFactoryNames(this.getSpringFactoriesLoaderFactoryClass(), this.getBeanClassLoader());
    Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you are using a custom packaging, make sure that file is correct.");
    return configurations;
}
```

最终去扫描了这个路径下的配置文件信息![image-20220325012110810](F:\图像\typora图像保存位置\image-20220325012110810.png)

那么我们再回到 	这里	 看看他的两个传参

```java
SpringFactoriesLoader.loadFactoryNames(this.getSpringFactoriesLoaderFactoryClass(), this.getBeanClassLoader())
```

![image-20220325012516008](F:\图像\typora图像保存位置\image-20220325012516008.png)

而第二个参数 也是本类中所包含的静态资源 中文为 (bean类加载器)

![image-20220325012632414](F:\图像\typora图像保存位置\image-20220325012632414.png)

下面是spring.factories (注: 注意找对包 不同包下的 配置文件内容不同 这里我就找错了  图二才是对的)

![image-20220325013238274](F:\图像\typora图像保存位置\image-20220325013238274.png)

图二

![image-20220325014118441](F:\图像\typora图像保存位置\image-20220325014118441.png)





#### 提出疑问

为什么 配置文件里 这么多资源, 而我们在简单的 helloworld 测试时却什么都没有用到呢,   请看解析@ConditionalOnxxx

![image-20220325103655434](F:\图像\typora图像保存位置\image-20220325103655434.png)



流程图

![preview](https://segmentfault.com/img/bVcUUGz/view)



这个结论做的挺好的 拿来用一下

![image-20220325104940382](F:\图像\typora图像保存位置\image-20220325104940382.png)







### @ConditionalOnxxx

在一些需要加载的配置资源类上标注这个注释,  只有当注释条件全部满足时, 该配置类才会被加载.





### SpringApplication.run()  (持续更新)

先记住这个

![image-20220325111142817](F:\图像\typora图像保存位置\image-20220325111142817.png)





### 深化理解  

学过yaml再来理解

https://www.bilibili.com/video/BV1PE411i7CV?p=12

为什么 我们可以通过 yaml中的 一些属性设置,来设置端口号之类的玩意儿.  这个数据 是怎么传输给SpringBoot的呢?

![image-20220325171826491](F:\图像\typora图像保存位置\image-20220325171826491.png)



META-INF/spring.factories 文件下有大量的类,  我们随便点进去一个都会发现,他们是一个@Configuration() 表名这是一个配置类,  我们会发现他们基本上都会有 一个@EnableConfigurationProperties({WebFluxProperties.class, ServerProperties.class})自动装配xxxxx类,  我们点进去装配的类

![image-20220325172455231](F:\图像\typora图像保存位置\image-20220325172455231.png)

可以发现 这个类 会引入了 yaml中的 这个字段的值.   我们可以拿下图与上图做比较   ![image-20220325172628916](F:\图像\typora图像保存位置\image-20220325172628916.png)

你会发现我们在yaml中可以配置的值,其实就是这一个个类中的字段属性,  这些属性基本都有默认值, 如果我们没有在yaml中配置,他就是以默认值运行.





我们再结合最上面那张图的这两句话![image-20220325173024117](F:\图像\typora图像保存位置\image-20220325173024117.png) 马上就理解了 哈哈

![image-20220325173221883](F:\图像\typora图像保存位置\image-20220325173221883.png)

## 一些注解

```java
@Component	
//注册在pojo实体类上,让该类被SpringBoot托管

@Controller 控制器（注入服务）
 //用于标注控制层，相当于struts中的action层

@Service 服务（注入dao）
 //用于标注服务层，主要用来进行业务的逻辑处理

@Repository（实现dao访问）
 //用于标注数据访问层，也可以说用于标注数据访问组件，即DAO组件
@Autowired
//在测试时,注册在属性上,  与@Component配合使用 否则报错

```



### JSP303校验

https://www.jianshu.com/p/48725b7328c9	//帖子内更详细

```java
@Validated
//用在类上, 开启数据校验. 其下的所有注解 都需要有这个开启数据校验的时候才可以使用
    @Email(message="这不是邮箱弟弟")
    //验证这个字段的值是不是 邮箱,如果不是则提示message中的值

```



![image-20220325162430900](F:\图像\typora图像保存位置\image-20220325162430900.png)



## Yaml 语法

yaml在SpringBoot中代替properties 成为我们所使用的配置文件.  不不,把这玩意儿 当配置文件简直就是在侮辱它.  没想到竟然是 2006年的东西.



### 语法格式对比

```properties
key=value-properties
```

```yaml
key: value #父级     注意 key的冒号后面 必须要加上一个 空格分隔, 然后再写所对应的值
	keyy: value #子级
```



![image-20220325161012914](F:\图像\typora图像保存位置\image-20220325161012914.png)

### yaml体验 注意冒号后面的空格

```yaml
#键值对
key: value

#map	  我稍微调整一下 就好理解了
maps:
    tool: 
      name: 扩阴器
    tools:
      name: 丰乳膏
#      	key: value(省略了类名,直接给该类的属性赋值)
maps: {[tool: name: 扩阴器],[tools: name: 丰乳膏]}

#public class User {
#    private String username;
#    private String password;
#    private Map<String,Tools> maps; }
-----------------------------------------------------
#public class Tools {
#     private String name; }


#对象写法
user:
	username: xxxx
#对象行内写法
user: {username: xxxx,password: xxxx}


#List
List:
	- 我是傻逼
	- 你是傻逼
	- 他是傻逼
#List
List: [我是傻逼,你是傻逼,他是傻逼]

```



### 注解

@value("")	直接赋值

@value("${xxx.xxx.xxx}")		引用yaml中的 那个属性下的 什么什么





### EL表达式

{$random.int} 	一个int随机数   

{$xxx.xxx}	在注解 @value()中提到的yaml占位符 在yaml文件内 也可以使用









## 静态资源加载

在WebMvcAutoConfiguration类中, 有一个WebMvcAutoConfigurationAdapter内部类.  

它包含了加载静态资源的方法.addResourceHandlers().

![image-20220327171323169](F:\图像\typora图像保存位置\image-20220327171323169.png)

点开getStaticPathPattern()后![image-20220327171414507](F:\图像\typora图像保存位置\image-20220327171414507.png)根目录下的所有资源 都会被扫描

![image-20220327171643960](F:\图像\typora图像保存位置\image-20220327171643960.png)



现在我们知道了,为什么 被加载的静态资源为什么要放在哪里了.下面是偷懒截图. 

![image-20220327172410647](F:\图像\typora图像保存位置\image-20220327172410647.png)





## 模板引擎

### thymeleaf

#### maven

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```



#### 引用路径

```html
<link th:href="@{asserts/css/bootstrap.min.css}" rel="stylesheet">
<!--th:href="@{引用路径}"	th:src="@{引用路径}"-->
<link th:href="@{asserts/css/signin.css}" rel="stylesheet">
```



### 常用的语法

（1）常用表达式

- **${...}**：变量表达式。 
- ***{...}**：选择表达式。 
- **#{...}**：消息文字表达式。 
- **@{...}**：链接 **url** 表达式。 
- **#maps**：工具对象表达式。

（2）常用标签

- **th:action**：定义后台控制器路径。 

- **th:each**：循环语句。 

- **th:field**：表单字段绑定。 

- **th:href**：定义超链接。 

- **th:id**：**div** 标签中的 **ID** 声明，类似 **HTML** 标签中的归属性。 

- **th:if**：条件判断语句。 

	```yml
	<p th:text="${msg}" th:if="${not #strings.isEmpty(msg)}"></p>
	判断该字符串不为空
	```

	

- **th:include**：布局标签，替换内容到引入文件。 

- **th:fragment**：布局标签，定义一个代码片段，方便其他地方引用。 

- **th:object**：替换对象。 

- **th:src**：图片类地址引入。 

- **th:text**：显示文本。 

- **th:value**：属性赋值。

（3）常用函数

- **#dates**：日期函数。 
- **#lists**：列表函数。 
- **#arrays**：数组函数。 
- **#strings**：字符串函数。 
- **#numbers**：数字函数。 
- **#calendars**：日历函数。 
- **#objects**：对象函数。 
- **#bools**：逻辑函数。 






## 定义自己的视图解析器

https://www.bilibili.com/video/BV1PE411i7CV?p=18&spm_id_from=333.880.my_history.page.click

![image-20220329142931361](F:\图像\typora图像保存位置\image-20220329142931361.png)







## i18n国际化

这是必须要有的配置.   spring.messages.basename:  代表了i18n的配置文件地址.  填写错误则无法正确加载.    值为![image-20220402125851136](F:\图像\typora图像保存位置\image-20220402125851136.png)文件夹名, 加上这一套的配置文件名

```yml
spring:
  messages:
    basename: i18n.messages
  thymeleaf:
    cache: false
```





注意字符编码的问题, 如果文件的字符编码与,html的字符编码不匹配则无法正确显示对应字符.

#### 一些问题

自己配置的LocaleResolver 无法被spring容器托管, 

```java
@Configuration
public class MyMvcConfig implements WebMvcConfigurer {

    @Override
    public void addViewControllers(ViewControllerRegistry registry) {
        registry.addViewController("/").setViewName("index");
        registry.addViewController("/index.html").setViewName("index");
    }
//  我们需要在bean注解上 追加上,要扫描的方法名
    @Bean("localeResolver")
    public LocaleResolver LocaleResolver(){
        return new MyLocaleResolver();
    }
}
```

我们看这里,源码中使用的是localeResolver.  我们自己写的首字母大写了, 所以不会被容器检测到![image-20220402172812456](F:\图像\typora图像保存位置\image-20220402172812456.png)





草拟吗的 困扰了我三个小时的bug解决了.55555 下面是源码自己的解析器源码

```java
public class MyLocaleResolver implements LocaleResolver {

    @Override
    public Locale resolveLocale(HttpServletRequest request) {

        String language = request.getParameter("l");
//        System.out.println(language+"aaaaaa");
        Locale local = Locale.getDefault();

        if (!StringUtils.isEmpty(language)){

            String[] s = language.split("_");

            local = new Locale(s[0],s[1]);
        }
        return local;
    }
}
```









## Controller

什么是Controller  其实这个在springmvc中就已经用到了, 只不过急于学习springboot 忘记在那一部分笔记中做记录了.    Controller(康戳了儿) 其实就是一个servlet

```java
@Controller
public class LoginController {
	//这个注解就类似与servlet中的 映射路径,
    @RequestMapping("/user/login")
    					//这个注解表明被标注的属性的值 是 表单中的哪个参数传来的
    public String login(@RequestParam("username") String username, @RequestParam("password") String password, Model model){

        if(username.equals("2557402806")&&password.equals("123456")){
            User user=new User("1",username,password);

            if (user!=null){
                //表示重定向,url栏变化,会失去model中的传参
                return "redirect:/main.html";
            }else {
                model.addAttribute("msg","该账户不存在,请从新登录.");
                return "redirect:/index";
            }
        }else {

            model.addAttribute("msg","账号或密码有错,请检验输入.");
            //表示返回该名称的视图文件,但是url栏不会变化,也不会失去model中的传参.
            return "index";
        }
    }
}
```



