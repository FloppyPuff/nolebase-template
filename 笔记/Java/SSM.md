# 核心概念

![Pasted image 20250701142715](assests/Pasted%20image%2020250701142715.png)
![Pasted image 20250701142724](assests/Pasted%20image%2020250701142724.png)

# IOC

![Pasted image 20250701145140](assests/Pasted%20image%2020250701145140.png)

![Pasted image 20250701145145](assests/Pasted%20image%2020250701145145.png)

![Pasted image 20250701145157](assests/Pasted%20image%2020250701145157.png)

# DI

![Pasted image 20250701150403](assests/Pasted%20image%2020250701150403.png)

![Pasted image 20250701150410](assests/Pasted%20image%2020250701150410.png)

- `name`属性是类中变量名，而`ref`属性是在XML文件中已定义的bean

# bean

## 别名

![Pasted image 20250701151106](assests/Pasted%20image%2020250701151106.png)

## 作用范围

![Pasted image 20250701151435](assests/Pasted%20image%2020250701151435.png)

## 实例化

![Pasted image 20250701152531](assests/Pasted%20image%2020250701152531.png)

![Pasted image 20250701153123](assests/Pasted%20image%2020250701153123.png)
- `class`属性是工厂类类名

![Pasted image 20250701154246](assests/Pasted%20image%2020250701154246.png)

## 生命周期

![Pasted image 20250701155745](assests/Pasted%20image%2020250701155745.png)

![Pasted image 20250701155755](assests/Pasted%20image%2020250701155755.png)

![Pasted image 20250701155821](assests/Pasted%20image%2020250701155821.png)

![Pasted image 20250701160048](assests/Pasted%20image%2020250701160048.png)

# 依赖注入

![Pasted image 20250702144941](assests/Pasted%20image%2020250702144941.png)
![Pasted image 20250702144954](assests/Pasted%20image%2020250702144954.png)
![Pasted image 20250702145003](assests/Pasted%20image%2020250702145003.png)
![Pasted image 20250702145011](assests/Pasted%20image%2020250702145011.png)

# 自动装配

![Pasted image 20250702145520](assests/Pasted%20image%2020250702145520.png)
![Pasted image 20250702150148](assests/Pasted%20image%2020250702150148.png)
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">  
  
    <bean class="com.itheima.dao.impl.BookDaoImpl"/>  
    <!--autowire属性：开启自动装配，通常使用按类型装配-->  
    <bean id="bookService" class="com.itheima.service.impl.BookServiceImpl" autowire="byType"/>  
  
</beans>
```

# 加载properties文件

![Pasted image 20250702153316](assests/Pasted%20image%2020250702153316.png)
![Pasted image 20250702194134](assests/Pasted%20image%2020250702194134.png)

# 容器


![Pasted image 20250702194822](assests/Pasted%20image%2020250702194822.png)

![Pasted image 20250702195536](assests/Pasted%20image%2020250702195536.png)

![Pasted image 20250702195936](assests/Pasted%20image%2020250702195936.png)

![Pasted image 20250702200021](assests/Pasted%20image%2020250702200021.png)

![Pasted image 20250702200202](assests/Pasted%20image%2020250702200202.png)

# 注解开发

![Pasted image 20250702202433](assests/Pasted%20image%2020250702202433.png)

![Pasted image 20250702203335](assests/Pasted%20image%2020250702203335.png)

## bean管理

### 作用范围

![Pasted image 20250702203754](assests/Pasted%20image%2020250702203754.png)

### 生命周期

![Pasted image 20250702203805](assests/Pasted%20image%2020250702203805.png)

## 依赖注入

![Pasted image 20250702205208](assests/Pasted%20image%2020250702205208.png)

![Pasted image 20250702205317](assests/Pasted%20image%2020250702205317.png)

![Pasted image 20250702205738](assests/Pasted%20image%2020250702205738.png)

## 第三方bean管理

![Pasted image 20250702210733](assests/Pasted%20image%2020250702210733.png)

![Pasted image 20250702210809](assests/Pasted%20image%2020250702210809.png)

![Pasted image 20250702211315](assests/Pasted%20image%2020250702211315.png)

![Pasted image 20250702211325](assests/Pasted%20image%2020250702211325.png)

![Pasted image 20250702211804](assests/Pasted%20image%2020250702211804.png)

