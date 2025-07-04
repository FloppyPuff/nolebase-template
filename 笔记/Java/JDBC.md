# 简介

![Pasted image 20250630200728](assests/Pasted%20image%2020250630200728.png)

# 代码实现

```java
public class JDBCDemo {  
    public static void main(String[] args) throws Exception {  
        //1.加载驱动  
//        Class.forName("com.mysql.jdbc.Driver");  
        //2.获取连接  
        String url = "jdbc:mysql://127.0.0.1:3306/tlias";  
        String username = "root";  
        String password = "fjh15057036235.";  
        Connection conn = DriverManager.getConnection(url, username, password);  
        //3.定义SQL语句  
        String sql = "update account set money = 2000 where id = 1";  
        //4.获取执行SQL对象 Statement        Statement statement = conn.createStatement();  
        //5.执行SQL  
        int count = statement.executeUpdate(sql);//受影响行数  
        //6.处理结果  
        System.out.println(count);  
        //7.释放资源  
        statement.close();  
        conn.close();  
    }  
}
```
- 从 JDBC 4.0 开始，驱动会自动注册，**不需要手动调用 `Class.forName()`**

# JDBC API

## DriverManager

![Pasted image 20250630201547](assests/Pasted%20image%2020250630201547.png)

![Pasted image 20250630201554](assests/Pasted%20image%2020250630201554.png)

## Connection

![Pasted image 20250630202444](assests/Pasted%20image%2020250630202444.png)

## Statement

![Pasted image 20250630203134](assests/Pasted%20image%2020250630203134.png)

### ResultSet

![Pasted image 20250630204000](assests/Pasted%20image%2020250630204000.png)
- 遍历输出
```java
String url = "jdbc:mysql:///tlias";  
String username = "root";  
String password = "fjh15057036235.";  
Connection conn = DriverManager.getConnection(url, username, password);  
String sql = "select * from account";  
Statement statement = conn.createStatement();  
ResultSet resultSet = statement.executeQuery(sql);  
while (resultSet.next()) {  
    int id = resultSet.getInt(1);  
    String name = resultSet.getString(2);  
    int money = resultSet.getInt(3);  
    System.out.println(id);  
    System.out.println(name);  
    System.out.println(money);  
  
    System.out.println("-------------");  
}  
resultSet.close();  
statement.close();  
conn.close();
```
- 封装至POJO再输出
```java
String url = "jdbc:mysql:///tlias";  
String username = "root";  
String password = "fjh15057036235.";  
Connection conn = DriverManager.getConnection(url, username, password);  
String sql = "select * from account";  
Statement statement = conn.createStatement();  
ResultSet resultSet = statement.executeQuery(sql);  
List<Account> list = new ArrayList<>();  
while (resultSet.next()) {  
    Account account = new Account();  
    int id = resultSet.getInt("id");  
    String name = resultSet.getString("name");  
    int money = resultSet.getInt("money");  
    account.setId(id);  
    account.setName(name);  
    account.setMoney(money);  
    list.add(account);  
}  
System.out.println(list);  
resultSet.close();  
statement.close();  
conn.close();
```

### PreparedStatement

![Pasted image 20250630205734](assests/Pasted%20image%2020250630205734.png)

![Pasted image 20250630212015](assests/Pasted%20image%2020250630212015.png)

```java
String url = "jdbc:mysql:///tlias";  
String username = "root";  
String password = "fjh15057036235.";  
int id = 1;  
String name = "张三";  
try (Connection conn = DriverManager.getConnection(url, username, password);  
     Statement statement = conn.createStatement();  
) {  
    String sql = "select * from account where id = ? and name = ?";  
    PreparedStatement preparedStatement = conn.prepareStatement(sql);  
    //设置值  
    preparedStatement.setInt(1, id);  
    preparedStatement.setString(2, name);  
    ResultSet resultSet = preparedStatement.executeQuery();  
    if (resultSet.next()) {  
        System.out.println("登陆成功！");  
    } else {  
        System.out.println("登陆失败！");  
    }  
} catch (Exception e) {  
    e.printStackTrace();  
}
```

![Pasted image 20250630214116](assests/Pasted%20image%2020250630214116.png)

# 数据库连接池

## 简介

![Pasted image 20250630214535](assests/Pasted%20image%2020250630214535.png)

![Pasted image 20250630215016](assests/Pasted%20image%2020250630215016.png)

## 实现

```java
/**  
 * 数据库连接池  
 */  
public class DruidDemo {  
    public static void main(String[] args) throws Exception {  
        //加载配置文件  
        Properties properties = new Properties();  
        properties.load(new FileInputStream("src/main/resources/druid.properties"));  
        //获取连接池对象  
  
        DataSource dataSource = DruidDataSourceFactory.createDataSource(properties);  
        Connection connection = dataSource.getConnection();  
        System.out.println(connection); //com.mysql.cj.jdbc.ConnectionImpl@7c83dc97  
    }  
}
```

