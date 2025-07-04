```properties
spring:
  application:
    name: demo1  # 设置当前应用的名称，用于注册中心或日志中标识该应用
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver  # 指定MySQL数据库驱动类
    url: jdbc:mysql://localhost:3306/tlias  # 数据库连接地址，指向本地的 tlias 数据库
    username: root  # 数据库登录用户名
    password: fjh15057036235.  # 数据库登录密码
  servlet:
    multipart:
      max-file-size: 50MB  # 单个上传文件的最大大小限制
      max-request-size: 100MB  # 整个请求中上传数据的总大小限制（多个文件总和）
mybatis:
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl  # 使用标准输出打印 MyBatis 的 SQL 日志
    map-underscore-to-camel-case: true  # 自动将数据库下划线命名字段映射为 Java 中的驼峰命名属性
aliyun:
  oss:
    endpoint: "https://oss-cn-hangzhou.aliyuncs.com"  # 阿里云OSS服务的访问域名
    accessKeyId: "LTAI5tMjhby5aX76uLnfeqYT"  # 阿里云API访问的密钥ID
    accessKeySecret: "yt1MS7l96zGUPVCe9qc05E7toqD6HU"  # 阿里云API访问的密钥Secret
    bucketName: "2871629928"  # OSS中存储资源的Bucket名称
logging:
  level:
    org.springframework.jdbc.support.JdbcTransactionManager: debug  # 开启事务管理器的debug级别日志

```