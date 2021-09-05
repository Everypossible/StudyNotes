# 记录

## 1、开发流程

### 1、开发顺序

1. Conroller再到service再到dao层



### 2、通用功能

#### 1、统一异常处理

![image-20210817103558455](C:\Users\RS\AppData\Roaming\Typora\typora-user-images\image-20210817103558455.png)











## 2、附加知识

### 1、注解

1. @ControllerAdvice
    - 用处：对加了@Controller注解的方法进行拦截处理   AOP实现
2. @ExceptionHandler(Exception.class)
    - 用处：进行异常处理，处理Exception.class的异常





### 2、Java代码

#### 1、时间问题

- 将MySQL的时间戳转换成标准时间格式：from_unixtime(create_date/1000)