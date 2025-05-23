# xbatis-generator-maven-plugin

## xbatis maven代码生成插件

## xbatis官网文档：<strong style="color:red">http://xbatis.cn </strong> !!!

### 1. 快速开始

#### 1.1. 在pom中添加插件

```xml
<plugin>
    <groupId>cn.xbatis</groupId>
    <artifactId>xbatis-generator-maven-plugin</artifactId>
    <version>1.1.3</version>
    <!-- 添加相应的数据库驱动 -->
    <dependencies>
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <version>9.1.0</version>
        </dependency>
    </dependencies>
</plugin>
```

### 2. 相关配置 - 两种配置方式

#### 2.1. 在外部xml文件中配置(推荐)

` 注意除configurationFile和skip配置外，其他配置参数可以放到外部xml文件中, xml文件root为：`

```xml

<xbatis-generator>
    ...
</xbatis-generator>
```

##### 2.1.1. 配置maven插件

```xml

<plugin>
    <groupId>cn.xbatis</groupId>
    <artifactId>xbatis-generator-maven-plugin</artifactId>
    <version>最新版本</version>
    <!-- 添加相应数据库的驱动 -->
    <dependencies>
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <version>9.1.0</version>
        </dependency>
    </dependencies>
    <configuration>
        <!-- 指定xml配置文件的路径,可直接使用配置文件 -->
        <!-- 优先级， 配置文件的优先级大于 pom文件中的配置 -->
        <configurationFile>src/main/resources/xbatis-generator.xml</configurationFile>
    </configuration>
</plugin>
```

##### 2.1.2. 外部文件（xbatis-generator.xml）配置样例

` xbatis-generator.xml 可由自己指定文件名，和上面的 configurationFile配置一样即可 `

```xml

<xbatis-generator>
    <!-- 按照官方文档配置各对象 -->
    <author>trifolium</author>
    <fileCover>true</fileCover>
    <ignoreView>true</ignoreView>

    <dataSource>
        <username>xxx</username>
        <password>xxx</password>
        <jdbcUrl>jdbc:mysql://mysql.com:3306/db</jdbcUrl>
    </dataSource>

    <tableConfig>
        <tablePrefixes>
            <string>t_</string>
        </tablePrefixes>
        <includeTables>
            <string>t_admin</string>
            <string>t_admin_role</string>
        </includeTables>
    </tableConfig>

    <!--    <javaPath>src/main/java</javaPath>--><!-- 默认为src/main/java -->
    <!--    <resourcePath>src/main/resources</resourcePath>--><!-- 默认为src/main/resources -->

    <basePackage>com.company.app.test</basePackage>

    <entityConfig>
        <packageName>entity</packageName>
        <swagger>true</swagger>
        <lombok>true</lombok>
    </entityConfig>

    <mapperConfig>
        <packageName>mapper</packageName>
        <mapperAnnotation>false</mapperAnnotation>
    </mapperConfig>

    <mapperXmlConfig>
        <enable>true</enable>
        <packageName>mapper</packageName>
        <resultMap>true</resultMap>
        <columnList>true</columnList>
        <suffix>Mapper</suffix>
    </mapperXmlConfig>

    <daoConfig>
        <enable>false</enable>
    </daoConfig>
    <daoImplConfig>
        <enable>false</enable>
    </daoImplConfig>
    <serviceConfig>
        <enable>false</enable>
    </serviceConfig>
    <serviceImplConfig>
        <enable>false</enable>
    </serviceImplConfig>
    <actionConfig>
        <enable>false</enable>
    </actionConfig>
</xbatis-generator>
```

#### 2.2. 全部在pom文件中配置
```xml
<plugin>
    <groupId>cn.xbatis</groupId>
    <artifactId>xbatis-generator-maven-plugin</artifactId>
    <version>最新版本</version>
    <!-- 添加相应数据库的驱动 -->
    <dependencies>
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <version>9.1.0</version>
        </dependency>
    </dependencies>
    <configuration>
        <!-- 添加数据库配置 -->
        <dataSource>
            <username>xxx</username>
            <password>xxx</password>
            <jdbcUrl>jdbc:mysql://mysql.com:3306/db</jdbcUrl>
        </dataSource>
        <!-- 是否跳过生成,默认值false-->
        <skip>false</skip>
        <author>trifolium</author>
        <ignoreView>true</ignoreView>
<!--        <basePackage>com.xxx</basePackage>-->
        <!-- 按照官方文档配置各对象 -->
        <tableConfig>
            <tablePrefixes>
                <string>t_</string>
            </tablePrefixes>
            <includeTables>
                <string>t_admin</string>
                <string>t_admin_role</string>
            </includeTables>
        </tableConfig>
        <entityConfig>
            <packageName>com.xxx.entity</packageName>
            <swagger>true</swagger>
            <lombok>true</lombok>
        </entityConfig>
        <mapperConfig>
            <packageName>com.xxx.mapper</packageName>
            <mapperAnnotation>false</mapperAnnotation>
        </mapperConfig>
        <mapperXmlConfig>
            <enable>true</enable>
            <!-- 特殊的目录名称 -->
            <packageName>src/main/resources/mappers</packageName>
            <resultMap>true</resultMap>
            <columnList>true</columnList>
            <suffix>Mapper</suffix>
        </mapperXmlConfig>
        <daoConfig>
            <enable>false</enable>
        </daoConfig>
        <daoImplConfig>
            <enable>false</enable>
        </daoImplConfig>
        <serviceConfig>
            <enable>false</enable>
        </serviceConfig>
        <serviceImplConfig>
            <enable>false</enable>
        </serviceImplConfig>
        <actionConfig>
            <enable>false</enable>
        </actionConfig>
    </configuration>
</plugin>
```

### 3. 运行maven命令 `mvn xbatis-generator:generate` 即可

### 4. 更多配置，参考代码生成器xbatis-generator-core配置

> https://xbatis.cn/zh-CN/function/core/codeAutoCreate.html

### 5. 如需指定的xbatis-generator-core版本，请在插件plugin中添加依赖
```xml
<plugin>
    <groupId>cn.xbatis</groupId>
    <artifactId>xbatis-generator-maven-plugin</artifactId>
    <version>最新版本</version>
    <!-- 项目中需要添加驱动 -->
    <dependencies>
        <dependency>
            <groupId>cn.xbatis</groupId>
            <artifactId>xbatis-generator-core</artifactId>
            <version>指定版本</version>
        </dependency>
    </dependencies>
</plugin>
```

### 6. 注意事项
* 默认configurationFile是模块pom.xml文件目录同级下的xbatis-generator.xml文件
* 插件中 baseFilePath 默认为maven项目模块根目录(project.basedir)
* 其中skip和configurationFile参数，必须在pom中配置，其他参数可委托到配置文件
* 默认javaPath 为 src/main/java (project.build.sourceDirectory)
* 默认resourcePath 为 src/main/resources