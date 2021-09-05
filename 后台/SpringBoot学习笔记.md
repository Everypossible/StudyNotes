#  1、SpringBoot特点

## 1、依赖管理

### 1、SpringBoot依赖管理原理

- 需要编写 的代码

    ```xml
    <!--引入一个父项目-->
    <!--该父项目的作用：做依赖管理-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.4.RELEASE</version>
    </parent>
    <!--引入场景启动器-->
    <dependencies>
    	<dependency>
        	<groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
    ```

    

- 代码原理（不需要手写）

    ```xml
    <!--引入的父项目的父项目-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-dependencies</artifactId>
        <version>2.3.4.RELEASE</version>
    </parent>
    ```

    

    

### 2、开发步骤：

依赖特点：

- 几乎声明了开发中常用的依赖的版本号

- 开发导入starter场景启动器

- 无需关注版本号，自动版本仲裁

- 可以手动修改版本号

    如：

    ```xml
    <!--引入版本号-->
    <properties>
    	<mysql.version>5.1</mysql.version>
    </properties>
    ```

    



## 2、自动配置

- 自动配好Tomcat、SpringMVC、Web常见功能（如：字符编码问题）
- 默认的包结构
    - **主程序**所在包及其子包里面的组件都会默认被扫描
    - 无需配置以前的包扫描了
    - 若想手动修改包扫描可使用注解**@SpringBootApplication(scanBasePackages="com.heima")**
- 各种配置拥有默认值
    - 配置文件的值最终会绑定在某个类上，这个类会在容器中创建对象
- 按需加载所有自动配置项 
    - 引入了哪些starter那个场景才会开启
    - SpringBoot所有的自动配置功能都在 spring-boot-autoconfigure 包里面







# 2、容器功能（容器内添加组件）



### 1、@Configuration（中文：配置）

#### 1、功能：

- 在一个类上使用
- 告诉SpringBoot这是一个配置类，等同于spring的配置文件
- **@Bean**注解相当于spring的bean标签

#### 2、注意：

- Full模式和Lite模式 @Configuration(proxyBeanMethods = false)
    - 配置类组件之间无依赖用Lite模式（proxyBeanMethods = false），这样容器启动速度会更快，减少判断
    - 配置类组件之间有依赖用Full模式（proxyBeanMethods = true），方法会被调用得到之前的单实例组件



### 2、@import（中文：导入）

#### 1、使用方法：

- 在组件注解的上面
- @Input() 括号内是数组，如@import({User.class,DBHelper.class})

#### 2、功能：

- 给容器中自动创建出这两个类型的组件



### 3、@Conditional（中文：条件的）

#### 1、使用方法：

- 

#### 2、功能：

- 条件装配：满足Conditional指定的条件，则进行组件注入



### 4、@ImportResource（中文：引入文件）

#### 1、使用方法：

- 在配置类的上面的上面使用@ImportResource("classpath:beans.xml")用于引入beans.xml文件

#### 2、功能：

- 导入资源 



### 5、@ConfigurationProperties（中文：配置绑定）

#### 1、使用方法：

#### 2、功能：

- 使用Java读取到properties文件中的内容，并且把它封装到JavaBean中，以供随时使用。







# 3、自动配置原理入门

## 1、引导加载自动配置类







## 2、按需开启自动配置项

1. 虽然我们127个场景的所有配置启动的时候会默认全部加载。
2. 但是是按照条件装配规则，最终按需装配。





## 3、定制化修改自动配置

## 4、最佳实践







# 4、开发SpringBoot应用步骤：

1. 引入场景依赖

    场景在以下文档

    https://docs.spring.io/spring-boot/docs/current/reference/html/using.html#using.build-systems.starters

2. 查看自动配置了哪些（选做）

    - 自己分析，引入场景对应的自动配置一般都生效了
    - 配置文件（application.properties）中 debug = true 开启自动配置报告。（Negative表示不生效，positive表示生效）

3. 是否需要修改

    1. 参照文档修改配置项

        https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#application-properties

    2. 自定义加入或替换组件\

    3. 自定义器（xxxCustomizer）









# 5、简化开发的小技巧

## 1、Lombok简化Javabean开发

### 1、SpringBoot中如何使用Lombok：

1. 在pom.xml中引入Lombok依赖

    ```xml
    <!-- springBoot已经约定好了版本号 -->
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
    </dependency>
    ```

2. 在IDEA的插件市场中安装插件（**编译时**自动生成getter和setter方法，所以源代码会很整洁）

3. 编写实体类时只需要编写属性（在类上添加注解实现编译时自动生成哪些代码）

    1. @Data  --------------------  生成getter和setter方法
    2. @ToString  ----------------  生成toString方法
    3. @AllArgsConstructor  -----  生成全参构造器
    4. @NoArgsConstructor  -----  生成无参构造器
    5. @EqualsAndHashCode ----  重写equals和hashcode方法



## 2、dev-tools实现热更新

### 1、SpringBoot中如何使用Developer Tools：

1. 引入devtools依赖

    ```xml
    <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
            <optional>true</optional>
        </dependency>
    ```

    

2.  CTRL + F9  ----  重新编译项目      就能使代码生效





## 3、Spring Initailizr实现快速创建SpringBoot项目

- Spring InitialIzr（项目初始化向导）帮我们创建好了项目目录，添加好了依赖，创建好了主程序类（@SpringBootApplication），创建好了全局配置文件（application.properties）









# 6、SpringBoot核心功能

## 1、配置文件

### 1、配置文件类型



#### 1、properties

1. 同以前的properties用法

    

#### 2、yaml

1. yaml相较于xml有更简洁的语法以及更省资源

2. YAML是“YAML Ain't Markup Language”(YAML不是一种标记语言)的递归缩写。在开发的这种语言时，YAML的意思其实是：“Yet Another Markup Language”(仍是一种标记语言)。

    

3. 非常适合用来做以数据为中心的配置文件

    

4. 基本语法：

    - key: value；kv之间有空格

    - 大小写敏感

    - 使用缩进表示层级关系

    - 缩进不允许使用tab，只允许空格

    - 缩进的空格数不重要，只要相同层级的元素左对齐即可

    - ‘#'表示注释

    - 字符串无需加引号，如果要加，“（单引号）与 ""（双引号）表示字符串内容会被 转义 / 不转义（如 '\n'会以 \n 字符串输出，"\n" 会以换行输出）

        

5. 数据类型

    - 字面量：单个的、不可再分的值。date、boolean、string、number、null

        ```yaml
        k: v
        #注意kv之间要空格
        ```

    - 对象：键值对的集合。map、hash、set、object

        ```yaml
        行内写法：	k: {k1: v1,k2: v2,k3: v3}
        #或
        K:
          k1: v1
          k2: v2
          k3: v3
        ```

    - 数组：一组按次序排列的集合。array、list、queue

        ```yaml
        行内写法： k: [v1,v2,v3]
        #或
        k:
         - v1
         - v2
         - v3
        ```

        

### 2、自定义类绑定的配置提示

- 在pom.xml中引入配置处理器就会在写yaml时有提示

    ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-configuration-processor</artifactId>
        <optional>true</optional>
    </dependency>
    ```

- 在打包插件中会自动去除打包配置处理器

    

    





## 2、Web开发

### 1、Web开发内容

![image-20210815144638712](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210815144638712.png)

### 2、SpringMVC自动配置 



### 3、简单功能分析

#### 1、静态资源访问

1. 静态资源目录可以为：类路径下：/static（或 /public 或 /resources 或 /META-INF/resources），此时访问这些目录下的文件只需要访问：当前项目根路径（ 即 / ）+ 静态资源名

2. 原理：静态映射 /**

    请求进来后，先去找Controller看能不能处理。不能处理的所有请求又都交给静态资源处理器，若静态资源也找不到则报404.

3. 访问前缀：

    1. 默认是 / （即无前缀）

    2. 可自定义，如：

        ```yaml
        spring:
          mvc:
            static-path-pattern: /res/**
        ```

        此时访问路径应为：当前项目 + static-path-pattern + 静态资源名

    3. 自定义资源访问路径如，如：

        ```yaml
        spring:
          resources:
            static-locations: [classpath:/haha/]
        ```

        

    

#### 2、欢迎页支持

有两种方式设置静态页：

- 静态资源路径下 index.html 

    - 可以配置静态资源路径

    - 但是不可以配置静态资源的访问前缀，否则会导致 index.html不能被默认访问

        如：

        ```yaml
        spring:
        #  mvc:
        #    static-path-pattern: /res/**	这个会导致welcome page功能失效而且会影响favicon功能失效
          resources:
            static-locations: [classpath:/haha/]
        ```

        

- Controller能处理 /index





#### 3、自定义Favicon（网址小图标）

- 怎么自定义网站小图标：
    - 将图标图片命名为favicon.ico然后放在静态资源路径下即可



#### 4、静态资源配置原理

- SpringBoot启动默认加载 xxxAutoConfiguration 类（自动配置类）

- SpringMVC功能的自动配置类主要是 WebMvcAutoConfiguration，须确认生效

- 在WebMvcAutoConfiguration类中看看给容器中配了什么

- 看看配置文件的相关属性和xxx进行了绑定（这里主要是WebMvcProperties(和spring.mvc进行绑定）和ResourceProperties(和spring.properties进行绑定)）

- 可以通过application.yaml禁用所有静态资源规则

    ```yaml
    spring:
      resources:
        add-mapping: false
    ```

    







### 4、请求参数处理

#### 1、请求映射

- @xxxMapping

- Rest风格支持（使用HTTP请求方式动词来表示对资源的操作）

    - 以前：/getUser 获取用户 /deleteUser 删除用户 /editUser 修改用户  /saveUser保存用户

    - 现在：/user    GET-获取用户     DELETE-删除用户      PUT-修改用户     POST-保存用户

        如：

        ```java
        @RequestMapping(value = "/user",method = RequestMethod.GET)
        public String getUser(){
            return "GET-zhangsan";
        }
        
        @RequestMapping(value = "/user",method = RequestMethod.POST)
        public String saveUser(){
            return "POST-zhangsan";
        }
        ```

    - 核心Filter：    HiddenHttpMethodFilter

        - 用法：表单method=post，隐藏域_method=put

        - 表单提交要使用REST时的原理

            application.yaml中手动开启REST风格提交支持（默认是false）

            ```yaml
            spring:
              mvc:
                hiddenmethod:
                  filter:
                    enabled: true
            ```

            表单页面使用隐藏域提交方式

            注意：使用post方式提交，使用_method设置DELETE (这里不区分大小写) 或者其他REST其他方法

            ```html
            <form action="/user" method="post">
                <input name="_method" type="hidden" value="DELETE"/>
                <input value="REST-DELETE 提交" type="submit"/>
            </form>
            ```

            

#### 2、请求映射原理

- SpringBoot自动配置欢迎页的HandlerMapping。访问能访问到的index.html
- SpringBoot自动配置了默认的 RequestMappingHandlerMapping
- 请求进来，挨个尝试所有的 HandlerMapping 看是否有请求信息
    - 如果有就找到这个请求对应的 Handler
    - 如果没有就是下一个HandlerMapping
- 如果我们需要一些自定义的映射处理，我们也可以自己给容器中放 HandlerMapping



#### 3、常用参数注解使用

- 基本参数注解：

    - @PathVariable(路径变量)

        应用注解使用样例：

        ```java
        @RestController
        public class ParamterTestController {
            //	car/2/owner/zhangsan
            @GetMapping("/car/{id}/owner/{username-}")
            public Map<String, Object> getCar(@PathVariable("id") Integer id,
                                             @PathVariable("username") String name,
                                             @PathVariable Map<String,String> pv) {
                Map<String,Object> map = new HashMap<>();
                
                map.put("id", id);
                map.put("name", name);
                map.put("pv", pv);
                
                return
            }
        }
        ```

    - 还有以下基本参数注解（用法类似）
    
        ![image-20210815225106697](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210815225106697.png)
    
    - 







## 3、数据访问

## 4、单元测试

## 5、指标监控

## 6、原理解析









