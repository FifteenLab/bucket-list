## 基本使用

### SQL日志输出

mybatis配置文件添加日志输出前缀

~~~xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    
    <settings>
        <setting name="logPrefix" value="MybatisSql2Logback."/>
    </settings>
</configuration>
~~~

logback.xml 配置文件定义日志输出等级及路径

~~~xml
<logger name="MybatisSql2Logback" level="DEBUG">
    <!--打印至控制台-->
    <appender-ref ref="console" />
</logger>
~~~

