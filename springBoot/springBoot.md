# springBoot 

## 项目部署

### idea热加载

1. 添加依赖

   ``` xml
   <!--SpringBoot热部署配置 -->
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-devtools</artifactId>
               <scope>runtime</scope>
               <optional>true</optional>
           </dependency>
   ```

   

2. 修改pom插件

   ``` xml
    <plugin>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-maven-plugin</artifactId>
        <configuration>
            <fork>true</fork>
            <addResources>true</addResources>
        </configuration>
   </plugin>
   ```

   

3. 配置自动编译

   ![Snipaste_2020-12-07_15-15-23](D:\桌面\springBoot_md_images\Snipaste_2020-12-07_15-15-23.png)

4. 配置idea的register

   - 按住 ctrl+shift+alt+/ 选择register

     ![Snipaste_2020-12-07_15-17-24](D:\桌面\springBoot_md_images\Snipaste_2020-12-07_15-17-24.png)

   - 选择 compiler.automake.allow.when.app.running

     ![Snipaste_2020-12-07_15-18-12](D:\桌面\springBoot_md_images\Snipaste_2020-12-07_15-18-12.png)

### 使用log4j2

1. 导入依赖

``` xml
<!-- 添加log4j2依赖 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-log4j2</artifactId>
        </dependency>
```

2. 排除依赖干扰

   - 父工程中含有 spring-boot-starter-logging 则需要排除依赖

     ![Snipaste_2020-12-07_15-29-45](D:\桌面\springBoot_md_images\Snipaste_2020-12-07_15-29-45.png)

   - 排除干扰

     ``` xml
     <exclusions>
         <exclusion>
             <groupId>org.springframework.boot</groupId>
             <artifactId>spring-boot-starter-logging</artifactId>
         </exclusion>
     </exclusions>
     ```

     

3. 在recourses目录下添加log4j2-spring.xml文件

   ``` xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <configuration>
       <!-- 定义所有的appender -->
       <appenders>
           <!-- 输出控制台的配置 -->
           <console name="Console" tatget="SYSTEM_OUT">
               <patternlayout pattern="[%p] %m %n"/>
           </console>
       </appenders>
   
       <loggers>
           <root level="DEBUG">
               <appender-ref ref="Console"/>
           </root>
           <logger name="org.springframework" level="ERROR" />
           <logger name="com.baomidou" level="ERROR"/>
           <logger name="org.hibernate" level="ERROR" />
           <logger name="com.alibaba.druid" level="ERROR"/>
           <logger name="org.springframework.boot.actuate.autoconfigure.CrshAutoConfiguration"
                   level="warn"/>
           <logger name="org.springframework.boot.actuate.endpoint.jmx" level="warn"/>
       </loggers>
   
   </configuration>
   ```

   