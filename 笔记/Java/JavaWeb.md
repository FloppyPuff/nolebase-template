# HTTP 协议

## 概念

*Hyper Text Transfer Protocol*，超文本传输协议，规定了浏览器和服务器之间数据传输的规则。

## 特点

1. **基于 TCP 协议** ：面向连接，安全。
2. **基于请求-响应模型** ：一次请求对应一次响应。
3. **HTTP 协议是无状态的协议** ：对于事务处理没有记忆能力。每次请求-响应都是独立的。
    - **缺点** ：多次请求间不能共享数据。
    - **优点** ：速度快。

## 请求数据格式

![Pasted image 20250612201835](assests/Pasted%20image%2020250612201835.png)

![Pasted image 20250612201852](assests/Pasted%20image%2020250612201852.png)

- *GET*:请求参数在请求行中，没有请求体，如：`/brand/findAll?name=OPPO&status=1`GET请求的大小是有限制的
- *POST*:请求参数在请求体中，POST请求大小是没有限制的

## 响应格式

![Pasted image 20250612203303](assests/Pasted%20image%2020250612203303.png)



![Pasted image 20250612203709](assests/Pasted%20image%2020250612203709.png)

![Pasted image 20250612204531](assests/Pasted%20image%2020250612204531.png)

## 协议解析

# 请求响应

![Pasted image 20250612215244](assests/Pasted%20image%2020250612215244.png)

## 请求

### PostMan

![Pasted image 20250612215655](assests/Pasted%20image%2020250612215655.png)

---
### 简单参数

1. 使用`HttpServletRequest`来获取参数
```java
@RestController  
public class RequestController {  
    @RequestMapping("/simpleParam")  
    public String simpleParam(HttpServletRequest request){  
        String name = request.getParameter("name");  
        String intStr = request.getParameter("age");  
        int age = Integer.parseInt(intStr);  
        System.out.println(name + ':' + age);  
        return "OK";  
    }  
}
```
2. 使用`SpringBoot`方式
```java
    @RequestMapping("/simpleParam")  
    public String simpleParam(String name,int age){  
       System.out.println(name + ':' + age);  
        return "OK";  
    }
```
3. 如果方法形参名称与请求参数名称不匹配，可以使用`@RequestParam`完成映射
```java
@RequestMapping("/simpleParam")  
public String simpleParam(@RequestParam(name = "name")String userName ,int age){  
    System.out.println(userName + ':' + age);  
    return "OK";  
}
```
- `@RequestParam`中的`required`属性默认为`true`，代表请求参数必须传递，如果不传递将报错。如果该参数是可选的，可以将其值设置为`false`，也可以设置默认值`defaultValue = "param"`
---
### 实体参数

1. 简单实体对象：请求参数名与形参对象属性名相同，定义POJO(Plain Old Java Object)接收即可
```java
@RequestMapping("/simplePojo")  
public String simplePojo(User user){  
    System.out.println(user);  
    return "OK";  
}
```
2. 复杂实体对象：请求参数名与形参对象属性名相同，按照对象层次结构关系即可接收嵌套POJO属性参数
```java
@RequestMapping("/complexPojo")  
public String complexPojo(User user){  
    System.out.println(user);  
    return "OK";  
}
```
---
### 数组集合参数

1. 数组参数：请求参数名与形参数组名称相同且请求参数为多个，定义数组类型形参即可接收参数
```java
@RequestMapping("/arrayParam")  
public String arrayParam(String[] hobby){  
    System.out.println(Arrays.toString(hobby));  
    return "OK";  
}
```
2. 集合参数：请求参数名与形参集合名称相同且请求参数为多个，`@RequestParam`绑定参数关系
```java
@RequestMapping("/listParam")  
public String listParam(@RequestParam List<String> hobby){  
    System.out.println(hobby);  
    return "OK";  
}
```
- 使用集合参数时须在参数名前加上`@RequestPram`来将参数映射到`hobby`上

### 日期参数

- 使用`@DateTimeFormat`注解完成日期参数格式转换
```java
@RequestMapping("/dateParam")  
public String dateParam(@DateTimeFormat(pattern = "yyyy-MM-dd HH:mm:ss") LocalDateTime updateTime){  
    System.out.println(updateTime);  
    return "OK";  
}
```

### Json 参数

- JSON参数：JSON数据键名与形参对象属性名相同，定义POJO类型形参即可接收参数，需要使用`@RequestBody`标识
```java
@RequestMapping("/jsonParam")  
public String jsonParam(@RequestBody User user){  
    System.out.println(user);  
    return "OK";  
}
```

### 路径参数

- 路径参数：通过请求URL直接传递参数，使用{...}来标识路径参数，需使用`@PathVariable`获取路径参数
```java
@RequestMapping("/path/{id}")  
public String pathParam(@PathVariable Integer id){  
    System.out.println(id);  
    return "OK";  
}
```
```java
@RequestMapping("/path/{id}/{name}")  
public String pathParam(@PathVariable Integer id,@PathVariable String name){  
    System.out.println(id+" "+name);  
    return "OK";  
}
```

## 响应

### ResponseBody

- **类型** ：方法注解、类注解
- **位置** ：Controller 方法上 / 类上
- **作用** ：将方法返回值直接响应，如果返回值类型是实体对象 / 集合，将会转换为 JSON 格式响应。
- **说明** ：`@RestController = @Controller + @ResponseBody`
```java
@RequestMapping("/getAddr")  //返回对象
public Address getAddr(){  
    Address addr = new Address();  
    addr.setCity("杭州");  
    addr.setProvince("浙江省");  
    return addr;  
}
```
```json
{
        "province": "浙江省",
        "city": "杭州市"
    }
```
```java
@RequestMapping("listAddr")  //返回list数组
public List<Address> listAddr(){  
    List<Address> list = new ArrayList<>();  
  
    Address addr1 = new Address();  
    addr1.setProvince("浙江省");  
    addr1.setCity("杭州市");  
    Address addr2 = new Address();  
    addr2.setProvince("浙江省");  
    addr2.setCity("衢州市");  
    list.add(addr1);  
    list.add(addr2);  
    return list;
```
```json
[
    {
        "province": "浙江省",
        "city": "杭州市"
    },
    {
        "province": "浙江省",
        "city": "衢州市"
    }
]
```
---
### 统一响应结果

```java
@RequestMapping("/getAddr")  //统一方法返回值为Result对象
public Result getAddr(){  
    Address addr = new Address();  
    addr.setCity("杭州");  
    addr.setProvince("浙江省");  
    return Result.success(addr);  
}  
@RequestMapping("listAddr")  
public Result listAddr(){  
    List<Address> list = new ArrayList<>();  
  
    Address addr1 = new Address();  
    addr1.setProvince("浙江省");  
    addr1.setCity("杭州市");  
    Address addr2 = new Address();  
    addr2.setProvince("浙江省");  
    addr2.setCity("衢州市");  
    list.add(addr1);  
    list.add(addr2);  
    return Result.success(list);  
}  
  
@RequestMapping("/hello")  
public Result hello(){  
    System.out.println("hello,world");  
    return Result.success();  
}
```
- Result类
```java
package com.fujunhao.springbootwebreqresp.pojo;  
/**  
 * 统一响应结果封装类  
 */  
public class Result {  
    private Integer code ;//1 成功 , 0 失败  
    private String msg; //提示信息  
    private Object data; //数据 data  
    public Result() {  
    }  
    public Result(Integer code, String msg, Object data) {  
        this.code = code;  
        this.msg = msg;  
        this.data = data;  
    }  
    public Integer getCode() {  
        return code;  
    }  
    public void setCode(Integer code) {  
        this.code = code;  
    }  
    public String getMsg() {  
        return msg;  
    }  
    public void setMsg(String msg) {  
        this.msg = msg;  
    }  
    public Object getData() {  
        return data;  
    }  
    public void setData(Object data) {  
        this.data = data;  
    }  
    public static Result success(Object data){  
        return new Result(1, "success", data);  
    }  
    public static Result success(){  
        return new Result(1, "success", null);  
    }  
    public static Result error(String msg){  
        return new Result(0, msg, null);  
    }  
  
    @Override  
    public String toString() {  
        return "Result{" +  
                "code=" + code +  
                ", msg='" + msg + '\'' +  
                ", data=" + data +  
                '}';  
    }  
}
```

### 分层解耦

```java
@RestController  
public class EmpController {  
    @RequestMapping("/listEmp")  
    public Result list(){  
        //加载并解析XML  
        String file = this.getClass().getClassLoader().getResource("emp.xml").getFile();  
        System.out.println(file);  
        List<Emp> empList = XmlParserUtils.parse(file, Emp.class);  
        //对数据转换  
        empList.stream().forEach(emp -> {  
            String gender = emp.getGender();  
            if ("1".equals(gender)){  
                emp.setGender("男");  
            }else if("2".equals(gender)){  
                emp.setGender("女");  
            }  
            String job = emp.getJob();  
            if ("1".equals(job)){  
                emp.setJob("讲师");  
            }else if ("2".equals(job)){  
                emp.setJob("班主任");  
            }else if ("3".equals(job)){  
                emp.setJob("就业指导");  
            }  
        });  
        //响应数据  
        return Result.success(empList);  
    }  
}
```

以上的代码存在三层架构：数据访问、逻辑处理、接受请求并响应数据

- `controller`:控制层，接受前端发送的请求，对请求进行处理，并响应数据
- `service`:业务层，处理具体的业务逻辑
- `dao`:数据访问层（Data Access Object 持久层），负责数据访问操作，包括数据的增、删、改、查

![Pasted image 20250613201549](assests/Pasted%20image%2020250613201549.png)



![Pasted image 20250613201834](assests/Pasted%20image%2020250613201834.png)

分别创建dao、service、controller包，在dao和service创建接口，最后在包内创建impl包，在impl包内创建实现接口的类

#### 内聚

- 软件中各个功能模块内部的功能联系

#### 耦合

- 衡量软件中各个层/模块之间的依赖、关联的程度

![Pasted image 20250613215732](assests/Pasted%20image%2020250613215732.png)

![Pasted image 20250613220557](assests/Pasted%20image%2020250613220557.png)

![Pasted image 20250613220602](assests/Pasted%20image%2020250613220602.png)

若新增了一个`EmpServiceB`的类，只需将`EmpServiceA`中的`@Component`注解删除

#### IOC

![Pasted image 20250616161341](assests/Pasted%20image%2020250616161341.png)

![Pasted image 20250616162201](assests/Pasted%20image%2020250616162201.png)

- `@SpringBootApplication`具有包扫描作用，默认扫描当前包及其子包

#### DI

- 通过`@Autowired`注解，默认是按照**类型**机型，如果存在多个相同类型的bean，将会报错
可通过以下几种注解来解决：
- `@Primary`
- `@Qualifier`
- `@Resource`

```java
@Service  
@Primary  
public class EmpServiceB implements EmpService {  
    ...
}
```

```java
@RestController  
public class EmpController {  
    @Qualifier("empServiceA")  
    @Autowired //运行时，IOC容器会提供该类型的bean对象，即依赖注入  
    ...
}
```

```java
@RestController  
public class EmpController {  
    @Resource(name = "empServiceB")  
    private EmpService empService;  
    ...
}
```

![Pasted image 20250616164135](assests/Pasted%20image%2020250616164135.png)

![Pasted image 20250616164234](assests/Pasted%20image%2020250616164234.png)

# MyBatis

## 简介

- MyBatis 是一个基于 Java 的**持久层**框架，通过 XML 或注解实现 SQL 与 Java 对象的灵活映射，简化数据库操作并提升开发效率。

## JDBC

![Pasted image 20250616222722](assests/Pasted%20image%2020250616222722.png)

![Pasted image 20250616222730](assests/Pasted%20image%2020250616222730.png)

## 数据库连接池

![Pasted image 20250616223519](assests/Pasted%20image%2020250616223519.png)

![Pasted image 20250616223746](assests/Pasted%20image%2020250616223746.png)


## 删除数据

```java
@Mapper  
public interface EmpMapper {  
    @Delete("delete from emp where id = #{id}")  //sql语句
    public void delete(Integer id);  //接口方法
}
```
![Pasted image 20250617124618](assests/Pasted%20image%2020250617124618.png)

![Pasted image 20250617131013](assests/Pasted%20image%2020250617131013.png)

`#{}` 是预编译占位符，安全高效，应优先使用；`${}` 是直接字符串替换，容易引发 SQL 注入，只在必要时谨慎使用。

## 新增数据

```java
@Mapper  
public interface EmpMapper {  
    @Delete("delete from emp where id = #{id}")  
    public int delete(Integer id);  
    @Insert("insert into emp(username, name, gender, image, job, entrydate, dept_id, create_time, update_time) " +  
            "VALUES (#{username},#{name},#{gender},#{image},#{job},#{entrydate},#{deptId},#{createTime},#{updateTime})") //sql语句 
    public void insert(Emp emp);  
}
```

- 单元测试
```java
@Test  
public void testInsert(){  
    Emp emp = new Emp();  
    emp.setUsername("Tom");  
    emp.setName("汤姆");  
    emp.setImage("1.jpg");  
    emp.setGender((short)1);  
    emp.setCreateTime(LocalDateTime.now());  
    emp.setEntrydate(LocalDateTime.now());  
    emp.setUpdateTime(LocalDateTime.now());  
    emp.setDeptId(1);  
    empMapper.insert(emp);  
}
```

## 新增(主键返回)

![Pasted image 20250617134756](assests/Pasted%20image%2020250617134756.png)

```java
@Options(useGeneratedKeys = true,keyProperty = "id")  //使用生成的主键并且赋值给Emp对象的id字段
@Insert("insert into emp(username, name, gender, image, job, entrydate, dept_id, create_time, update_time) " +  
        "VALUES (#{username},#{name},#{gender},#{image},#{job},#{entrydate},#{deptId},#{createTime},#{updateTime})")  
public void insert(Emp emp);
```

## 更新

```java
//更新员工  
@Update("update emp set username = #{username}, name = #{name}," +  
        " gender = #{gender}, image = #{image}," +  
        "job = #{job}, entrydate= #{entrydate}," +  
        " dept_id = #{deptId},update_time = #{updateTime} where id = #{id}")  
public void update(Emp emp);
```

## 查询

```java
//查询  
@Select("select * from emp where id = #{id}")  
public Emp getById(Integer id);
```

![Pasted image 20250617140708](assests/Pasted%20image%2020250617140708.png)


解决方法：
1. 给字段起别名，让字段与实体类属性名一致
```java
//查询  
@Select("select id, username, password, name, gender," +  
        " image, job, entrydate, dept_id deptId, create_time createTime," +  
        " update_time updateTime from emp where id = #{id}")  
public Emp getById(Integer id);
```
2. 通过mybatis中的两个注解：`@Results`和`@Result`手动映射封装
```java
@Results({  
        @Result(column = "dept_id",property = "deptId"),  
        @Result(column = "create_time",property = "createTime"),  
        @Result(column = "update_time",property = "updateTime")  
})  
@Select("select * from emp where id = #{id}")  
public Emp getById(Integer id);
```
3. 开启mybatis的驼峰命名自动映射
```properties
#开启mybatis的驼峰命名自动映射  
mybatis.configuration.map-underscore-to-camel-case=true
```

## 条件查询

```java
//条件查询  
    @Select("select * from emp where name like '%${name}%' " +  //在字符串中需使用${}，但是会造成sql注入以及低性能
            "                    and gender = #{gender}" +  
            "                    and entrydate between #{begin} and #{end}" +  
            "                  order by update_time desc")  
    public List<Emp> list(String name, short gender, LocalDate begin,LocalDate end);  
```

- 解决方案(使用concat()函数)
```java
@Select("select * from emp where name like concat('%',#{name},'%')\n" +  
        "                    and gender = 1\n" +  
        "                    and entrydate between '2010-01-01' and '2020-01-01'\n" +  
        "                  order by update_time desc")  
public List<Emp> list(String name, short gender, LocalDate begin,LocalDate end);
```

![Pasted image 20250617143557](assests/Pasted%20image%2020250617143557.png)

## XML映射文件

![Pasted image 20250617143951](assests/Pasted%20image%2020250617143951.png)

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE mapper  
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"  
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">  
<mapper namespace="com.itheima.mapper.EmpMapper">  
    <select id="list" resultType="com.itheima.pojo.Emp">  
        select * from emp where name like concat('%',#{name},'%')                            and gender = 1                            and entrydate between '2010-01-01' and '2020-01-01'                          order by update_time desc    
    </select>  
</mapper>
```

## 动态SQL

### if

![Pasted image 20250617150735](assests/Pasted%20image%2020250617150735.png)

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<!DOCTYPE mapper  
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"  
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">  
<mapper namespace="com.itheima.mapper.EmpMapper">  
    <select id="list" resultType="com.itheima.pojo.Emp">  
        select *
        from emp        
        <where>  
            <if test="name != null">  
                name like concat('%', #{name}, '%')                           </if>  
            <if test="gender != null">  
                and gender = 1            
            </if>  
            <if test="begin != null and end != null">  
                and entrydate between '2010-01-01' and '2020-01-01'
            </if>  
        </where>  
        order by update_time desc    
    </select>  
</mapper>
```

- 动态更新
```java
<update id="update2">  
    update emp    
    <set>  
        <if test="username != null">  
            username = #{username},        
        </if>  
        <if test="name != null">  
            name = #{name},        
        </if>  
        <if test="gender != null">  
            gender = #{gender},        
        </if>  
        <if test="image != null">  
            image = #{image},        
        </if>  
        <if test="job != null">  
            job = #{job},        
        </if>  
        <if test="entrydate != null">  
            entrydate= #{entrydate},        
        </if>  
        <if test="deptId != null">  
            dept_id = #{deptId},        
        </if>  
        <if test="updateTime != null">  
            update_time = #{updateTime}        
        </if>  
    </set>  
    where id = #{id}</update>
```
使用`<set>`标签来去除多余逗号
![Pasted image 20250617155813](assests/Pasted%20image%2020250617155813.png)
### foreach

![Pasted image 20250617160722](assests/Pasted%20image%2020250617160722.png)

```xml
<delete id="deleteByIds">  
    delete    
    from emp    
    where id in    
    # collection:遍历的集合  
    # item:遍历出来的元素  
    # seperator:分隔符  
    # open:遍历开始前拼接的SQL片段  
    # close:遍历结束后拼接的SQL片段  
    <foreach collection="ids" item="id" separator="," close=")" open="(">  
        #{id}    
    </foreach>  
</delete>
```

### sql&include

![Pasted image 20250617161808](assests/Pasted%20image%2020250617161808.png)
- 抽取SQL片段
```xml
<sql id="commonSelect">  
    select id,           
    username,           
    password,           
    name,           
    gender,           
    image,           
    job,           
    entrydate,           
    dept_id,           
    create_time,           
    update_time    
    from emp</sql>
```
- 注入SQL片段
```xml
<select id="list" resultType="com.itheima.pojo.Emp">  
    <include refid="commonSelect"></include>  
    <where>  
        <if test="name != null">  
            name like concat('%', #{name}, '%')        
        </if>  
        <if test="gender != null">  
            and gender = 1        
        </if>  
        <if test="begin != null and end != null">  
            and entrydate between '2010-01-01' and '2020-01-01'            </if>  
    </where>  
    order by update_time desc
</select>
```

![Pasted image 20250618220344](assests/Pasted%20image%2020250618220344.png)


# Lombok

![Pasted image 20250616224857](assests/Pasted%20image%2020250616224857.png)

# PageHelper

- 使用PageHelper实现自动分页

```java
@Override  
public PageBean page(Integer page, Integer pageSize) {  
    PageHelper.startPage(page, pageSize); // 分页参数设置  
    List<Emp> empList = empMapper.list(); // 查询数据  
    Page<Emp> p = (Page<Emp>) empList;// 封装分页信息  
    return new PageBean(p.getTotal(), p.getResult());  
}
```
流程：
1. 先调用`PageHelper.startPage(page,pageSize)`来设置分页参数，其原理是拦截下一条SQL语句，在其后加上`limit (page-1)*pageSize,pageSize`
2. 再调用Mapper层的查询全部数据的方法，此时这条SQL被PageHelper拦截
3. 再使用Page类封装分页信息
4. 最后将调用getTotal()和getResult()方法获取数据并将数据封装为PageBean

# 文件上传

```java
public class UploadController {  
    @PostMapping("/upload")  
    public Result upload(String username, Integer age, MultipartFile image) throws IOException {  
        log.info("文件上传：{},{},{}",username,age,image);  
        //获取原始文件名  
        String originalFileName = image.getOriginalFilename();  
        //构造唯一文件名 UUID        
        int index = originalFileName.lastIndexOf(".");  
        String suffix = originalFileName.substring(index);  
        String newFileName = UUID.randomUUID().toString()+substring;  
        log.info("新的文件名："+newFileName);  
        //将文件存储在服务器磁盘中  
        image.transferTo(new File("D:\\DesktopFolder\\JAVA\\"+newFileName));  
        return Result.success();  
    }  
}
```

1. 调用`MultipartFile.getOriginalFilename()`获取文件原始名
2. 根据原始名后缀和UUID构造唯一的文件名
3. 调用`MultipartFile.transferTo()`将文件存储在磁盘中

配置上传文件大小限制：
```properties
spring.servlet.multipart.max-file-size=50MB  //单个文件最大大小
spring.servlet.multipart.max-request-size=100MB //单次请求最大大小
```


# 配置文件

![Pasted image 20250627134714](assests/Pasted%20image%2020250627134714.png)
![Pasted image 20250627140600](assests/Pasted%20image%2020250627140600.png)

可以使用`@ConfigurationProperties`自动配置属性

```java
@Component  
@Data  
@ConfigurationProperties(prefix = "aliyun.oss")  //指定前缀
public class AliOSSUtils {  
    private String endpoint ;  
    private String accessKeyId ;  
    private String accessKeySecret ;  
    private String bucketName ; 
}
```

![Pasted image 20250627143014](assests/Pasted%20image%2020250627143014.png)

# 登录认证

![Pasted image 20250627151404](assests/Pasted%20image%2020250627151404.png)

![Pasted image 20250627153319](assests/Pasted%20image%2020250627153319.png)

  ![Pasted image 20250627153608](assests/Pasted%20image%2020250627153608.png)
![Pasted image 20250627154651](assests/Pasted%20image%2020250627154651.png)

![Pasted image 20250627155146](assests/Pasted%20image%2020250627155146.png)

## JWT
![Pasted image 20250627155855](assests/Pasted%20image%2020250627155855.png)

![Pasted image 20250627161100](assests/Pasted%20image%2020250627161100.png)
- 生成JWT
```java
Map<String, Object> claims = new HashMap<>();  
claims.put("id",1);  
claims.put("name","tom");  
String jwt = Jwts.builder()  
        .signWith(SignatureAlgorithm.HS256,"fujunhao")//设置签名算法和密钥  
        .setClaims(claims)//自定义内容（有效载荷）  
        .setExpiration(new Date(System.currentTimeMillis() + 3600*1000))//设置有效期为1h 
        .compact();  
System.out.println(jwt);
```
- 校验JWT
```java
Claims claims = Jwts.parser()  
        .setSigningKey("fujunhao")  
        .parseClaimsJws("eyJhbGciOiJIUzI1NiJ9.eyJuYW1lIjoidG9tIiwiaWQiOjEsImV4cCI6MTc1MTAxNjIxNn0.KkDuc66b39uW8R5w9QmdAoHcAHMdIQNXJf97jHtITj8")  
        .getBody();  
System.out.println(claims);
```

![Pasted image 20250627163343](assests/Pasted%20image%2020250627163343.png)

## Filter 过滤器

![Pasted image 20250627171818](assests/Pasted%20image%2020250627171818.png)

```java
@WebFilter(urlPatterns = "/*")  
@Slf4j  
public class DemoFilter implements Filter {  
    @Override //初始化方法，只调用一次  
    public void init(FilterConfig filterConfig) throws ServletException {  
        log.info("init called!");  
    }  
  
    @Override //拦截请求都会调用  
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {  
        log.info("intercepting...");  
        filterChain.doFilter(servletRequest,servletResponse);  
    }  
  
    @Override  
    public void destroy() {  
        log.info("destroy called!");  
    }  
}
```
- 还需要在SpringBoot启动类中添加`@ServletComponentScan`注解

![Pasted image 20250627185044](assests/Pasted%20image%2020250627185044.png)

![Pasted image 20250627190241](assests/Pasted%20image%2020250627190241.png)

## Interceptor 拦截器

![Pasted image 20250627200053](assests/Pasted%20image%2020250627200053.png)

![Pasted image 20250627200217](assests/Pasted%20image%2020250627200217.png)

- 拦截器
```java
@Component  
public class LoginCheckInterceptor implements HandlerInterceptor {  
    @Override //目标资源方法运行前运行，如果为TRUE，放行，反之不放行  
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {  
        System.out.println("preHandle...");  
        return true;  
    }  
  
    @Override //目标资源方法运行后运行  
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {  
        System.out.println("postHandle...");  
    }  
  
    @Override //视图渲染完毕后运行  
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {  
        System.out.println("afterCompletion...");  
    }  
}
```

- 拦截器注册
```java
@Configuration  
public class WebConfig implements WebMvcConfigurer {  
    @Autowired  
    private LoginCheckInterceptor loginCheckInterceptor;  
    @Override  
    public void addInterceptors(InterceptorRegistry registry) {  
        registry.addInterceptor(loginCheckInterceptor).addPathPatterns("/**");  
    }  
}
```

![Pasted image 20250627210014](assests/Pasted%20image%2020250627210014.png)

![Pasted image 20250627211351](assests/Pasted%20image%2020250627211351.png)

# 异常处理

```java
@RestControllerAdvice  
public class GlobalExceptionHandler {  
    @ExceptionHandler(Exception.class)  
    public Result ex(Exception ex){  
        ex.printStackTrace();  
        return Result.error("对不起，操作失败，请联系管理员");  
    }  
}
```
- `@RestControllerAdvice`=`@ControllerAdvice`+`@ResponseBody`

# Spring事务管理

![Pasted image 20250628141322](assests/Pasted%20image%2020250628141322.png)

![Pasted image 20250628142341](assests/Pasted%20image%2020250628142341.png)

![Pasted image 20250628142720](assests/Pasted%20image%2020250628142720.png)

![Pasted image 20250628145456](assests/Pasted%20image%2020250628145456.png)

# AOP

![Pasted image 20250628150845](assests/Pasted%20image%2020250628150845.png)

```java
@Component  
@Aspect  
@Slf4j  
public class TimeAspect {  
    @Around("execution(* com.fujunhao.springaop.service.*.*(..))") //切入点表达式  
    public Object recordTime(ProceedingJoinPoint joinPoint) throws Throwable {  
        //1.记录开始时间  
        long begin = System.currentTimeMillis();  
        //2.调用原始方法  
        Object result = joinPoint.proceed();  
        //3.记录结束时间，计算耗时  
        long end = System.currentTimeMillis();  
        log.info(joinPoint.getSignature() + "方法执行耗时：{}ms",end - begin);  
        return result;  
    }  
}
```

![Pasted image 20250628163335](assests/Pasted%20image%2020250628163335.png)

![Pasted image 20250628165024](assests/Pasted%20image%2020250628165024.png)

![Pasted image 20250628165427](assests/Pasted%20image%2020250628165427.png)

![Pasted image 20250628171251](assests/Pasted%20image%2020250628171251.png)

```java
@Slf4j  
@Component  
@Aspect  
public class MyAspect1 {  
  
    //抽取切入点表达式  
    @Pointcut("execution(* com.fujunhao.springaop.service.impl.DeptServiceImpl.*(..))")  
    private void pointCut(){}  
    @Before("pointCut()")  
    public void before(){  
        log.info("before...");  
    }  
  
    @Around("execution(* com.fujunhao.springaop.service.impl.DeptServiceImpl.*(..))")  
    public Object around(ProceedingJoinPoint joinPoint) throws Throwable {  
        log.info("around before ...");  
        Object result = joinPoint.proceed(); //调用原始方法执行  
        log.info("around after ...");  
        return result;  
    }  
  
    @After("execution(* com.fujunhao.springaop.service.impl.DeptServiceImpl.*(..))")  
    public void after(){  
        log.info("after...");  
    }  
    @AfterReturning("execution(* com.fujunhao.springaop.service.impl.DeptServiceImpl.*(..))")  
    public void afterReturning(){  
        log.info("after returning...");  
    }  
    @AfterThrowing("execution(* com.fujunhao.springaop.service.impl.DeptServiceImpl.*(..))")  
    public void afterThrowing(){  
        log.info("after throwing...");  
    }  
}
```

![Pasted image 20250628171926](assests/Pasted%20image%2020250628171926.png)



![Pasted image 20250628181037](assests/Pasted%20image%2020250628181037.png)

## 切入点表达式

![Pasted image 20250628181429](assests/Pasted%20image%2020250628181429.png)
![Pasted image 20250628201044](assests/Pasted%20image%2020250628201044.png)

![Pasted image 20250628202354](assests/Pasted%20image%2020250628202354.png)

![Pasted image 20250628205015](assests/Pasted%20image%2020250628205015.png)

![Pasted image 20250628205653](assests/Pasted%20image%2020250628205653.png)
- 注解
```java
@Retention(RetentionPolicy.RUNTIME)  
@Target(ElementType.METHOD)  
public @interface MyLog {  
}
```
- 切面类
```java
@Component  
@Aspect  
@Slf4j  
public class MyAspect2 {  
    @Pointcut("@annotation(com.fujunhao.springaop.aop.MyLog)")  
    public void pt(){}  
  
    @Before("pt()")  
    public void before(){  
        log.info("MyAspect2 ... before ...");  
    }  
}
```

## 连接点

![Pasted image 20250628205947](assests/Pasted%20image%2020250628205947.png)

```java
@Aspect  
@Slf4j  
@Component  
public class MyAspect3 {  
    @Pointcut("@annotation(com.fujunhao.springaop.aop.MyLog)")  
    public void pt(){}  
  
    @Around("pt()")  
    public Object around(ProceedingJoinPoint proceedingJoinPoint) throws Throwable {  
        log.info("MyAspect3 around before...");  
        //1.获取目标对象类名  
        String name = proceedingJoinPoint.getTarget().getClass().getName();  
        log.info("目标对象的类名：{}",name);  
        //2.获取目标方法的方法名  
        String methodName = proceedingJoinPoint.getSignature().getName();  
        log.info("目标方法的方法名：{}",methodName);  
        //3.获取方法运行时传入的参数  
        Object[] args = proceedingJoinPoint.getArgs();  
        log.info("目标方法运行时传入的参数：{}", Arrays.toString(args));  
        //4.放行目标方法执行  
        Object result = proceedingJoinPoint.proceed();  
        //5.获取目标对象的返回值  
        log.info("目标方法运行的返回值：{}",result);  
        log.info("MyAspect3 around after...");  
        return result;  
    }  
}
```

# Bean

## 作用域

![Pasted image 20250628224456](assests/Pasted%20image%2020250628224456.png)

- `@Lazy`:懒加载，在需要bean的时候才加载bean对象

![Pasted image 20250628225031](assests/Pasted%20image%2020250628225031.png)

## 第三方bean
![Pasted image 20250628225936](assests/Pasted%20image%2020250628225936.png)

![Pasted image 20250628230946](assests/Pasted%20image%2020250628230946.png)


![Pasted image 20250628231114](assests/Pasted%20image%2020250628231114.png)

# SpringBoot 自动配置

![Pasted image 20250629165152](assests/Pasted%20image%2020250629165152.png)

![Pasted image 20250629165200](assests/Pasted%20image%2020250629165200.png)

## 条件配置

![Pasted image 20250629170716](assests/Pasted%20image%2020250629170716.png)

## 自定义starter

![Pasted image 20250629205131](assests/Pasted%20image%2020250629205131.png)

# Maven

## 继承


![Pasted image 20250630110402](assests/Pasted%20image%2020250630110402.png)
![Pasted image 20250630110409](assests/Pasted%20image%2020250630110409.png)
![Pasted image 20250630110503](assests/Pasted%20image%2020250630110503.png)

## 版本锁定

![Pasted image 20250630111748](assests/Pasted%20image%2020250630111748.png)

![Pasted image 20250630112606](assests/Pasted%20image%2020250630112606.png)

