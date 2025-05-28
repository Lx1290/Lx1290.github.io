# 生成数据库文档配置
```
<plugin>  
    <groupId>cn.smallbun.screw</groupId>  
    <artifactId>screw-maven-plugin</artifactId>  
    <version>1.0.5</version>  
    <dependencies>        <!-- HikariCP -->  
        <dependency>  
            <groupId>com.zaxxer</groupId>  
            <artifactId>HikariCP</artifactId>  
            <version>3.4.5</version>  
        </dependency>  
        <!--mysql driver-->  
        <dependency>  
            <groupId>mysql</groupId>  
            <artifactId>mysql-connector-java</artifactId>  
            <version>8.0.20</version>  
        </dependency>  
    </dependencies>  
    <configuration>        <!--username-->  
        <username>dfzquser</username>  
        <!--password-->  
        <password>Dfzq1234.,</password>  
        <!--driver-->  
        <driverClassName>com.mysql.cj.jdbc.Driver</driverClassName>  
        <!--jdbc url-->  
        <jdbcUrl>jdbc:mysql://10.98.61.14:3306/dfzq_ppr_app</jdbcUrl>  
        <!--生成文件类型-->  
        <fileType>WORD</fileType>  
        <!--打开文件输出目录-->  
        <openOutputDir>false</openOutputDir>  
        <!--生成模板-->  
        <produceType>freemarker</produceType>  
        <!--文档名称 为空时:将采用[数据库名称-描述-版本号]作为文档名称-->  
        <fileName>价格预测系统数据库文档</fileName>  
        <!--描述-->  
        <description>价格预测系统数据库文档</description>  
        <!--版本-->  
        <version>1.0</version>  
        <!--标题-->  
        <title>价格预测系统数据库文档</title>  
    </configuration>  
    <executions>        <execution>  
            <phase>compile</phase>  
            <goals>                <goal>run</goal>  
            </goals>  
        </execution>  
    </executions>  
</plugin>
```