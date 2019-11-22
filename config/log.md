# 日志

quickdao采用了slf4j作为日志门面框架,您可以自由选择日志实现层(logback,log4j等等).

quickdao在debug级别下会输出SQL日志,在trace级别下会输出批量操作的sql日志和count方法日志.

以下是以logback作为样例

## 导入logback

```xml
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.2.3</version>
</dependency>
```

## 配置logback.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration scan="true">
    <appender name="stdout" class="ch.qos.logback.core.ConsoleAppender">
        <Target>System.out</Target>
        <encoder>
            <pattern>%-5level %d{yyyy-MM-dd HH:mm:ss.SSS} %c{10}:%L %m %n</pattern>
        </encoder>
    </appender>
    
    <!--改成INFO级别则不会输出SQL日志-->
    <logger name="cn.schoolwow.quickdao" level="DEBUG" additivity="false">
        <appender-ref ref="stdout"/>
    </logger>

    <root level="DEBUG">
        <appender-ref ref="stdout" />
    </root>
</configuration>
```
