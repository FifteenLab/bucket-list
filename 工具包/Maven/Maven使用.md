[TOC]

## Maven 基本使用

### 配置中央仓库镜像地址

在setting.xml 文件`mirrors` 下添加镜像地址。如下：

~~~xml
<mirrors>
    <mirror>
        <id>aliyunmaven</id>
        <mirrorOf>central</mirrorOf>
        <name>aliyun pulbic repository</name>
        <url>https://maven.aliyun.com/repository/public</url>
    </mirror>
</mirrors>
~~~

### 构建项目到本地仓库

~~~shell
mvn install -Dmaven.test.skip=true
~~~

`-Dmaven.test.skip=true`表示跳过测试。

### 发布到私服

1、项目pom.xml 配置私服地址

~~~xml
<distributionManagement>
    <repository>
        <id>releases</id>
        <!-- 私服内网IP地址192.168.1.123 -->
        <url>http://192.168.1.123:9000/repository/maven-releases/</url>
    </repository>
    <snapshotRepository>
        <id>snapshots</id>
        <url>http://192.168.1.123:9000/repository/maven-snapshots/</url>
    </snapshotRepository>
</distributionManagement>
~~~

2、setting.xml 文件中配置登录账户密码。

~~~xml
<servers>
    <!-- 定义私服登录的用户名密码 -->
    <server>
        <id>releases</id>
        <username>admin</username>
        <password>123456</password>
    </server>
    <server>
        <id>snapshots</id>
        <username>admin</username>
        <password>123456</password>
    </server>
</servers>
~~~

> server id 需要和pom.xml 文件中的 repository id 保持一直。

3、执行命令发布到私服

在项目目录下执行以下命令完成项目发布。

```shell
mvn deploy -Dmaven.test.skip=true
```

4、setting.xml 文件中配置仓库地址，实现从私服下载依赖。

具体配置仓库地址的方式有很多种，这里暂时只列举一种。

~~~xml
<profiles>
    <profile>
        <id>dev</id>
        <activation>
            <jdk>1.8</jdk>
        </activation>
        <!-- 配置私服仓库地址 -->
        <repositories>
            <repository>
                <id>releases</id>
                <url>http://192.168.1.123:9000/repository/maven-releases/</url>
                <release>
                    <enabled>true</enabled>
                </release>
                <snapshots>
                    <enabled>false</enabled>
                </snapshots>
            </repository>
            <repository>
                <id>snapshots</id>
                <url>http://192.168.1.123:9000/repository/maven-snapshots/</url>
                <release>
                    <enabled>false</enabled>
                </release>
                <snapshots>
                    <enabled>true</enabled>
                </snapshots>
            </repository>
        </repositories>
        <!-- 配置插件仓库 -->
        <pluginRepositories>
            <repository>
                <id>public</id>
                <url>http://192.168.1.123:9000/repository/maven-public/</url>
                <release>
                    <enabled>true</enabled>
                </release>
                <snapshots>
                    <enabled>true</enabled>
                </snapshots>
            </repository>
        </pluginRepositories>
    </profile>
</profiles>
<activeProfiles>
    <activeProfile>dev</activeProfile>
</activeProfiles>
~~~

### 发布源码

pom.xml 文件中添加`maven-source-plugin`插件。

方式一：

~~~xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-source-plugin</artifactId>
            <version>3.2.0</version>
            <executions>
                <execution>
                    <!-- 绑定source插件到Maven的生命周期 -->
                    <id>attach-sources</id>
                    <goals>
                        <goal>jar</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
~~~

方式二：

~~~xml
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-source-plugin</artifactId>
	<version>3.0.0</version>
	<!-- 绑定source插件到Maven的生命周期,并在生命周期后执行绑定的source的goal -->
	<executions>
		<execution>
			<!-- 绑定source插件到Maven的生命周期 -->
			<phase>compile</phase>
			<!--在生命周期后执行绑定的source插件的goals -->
			<goals>
				<goal>jar-no-fork</goal>
			</goals>
		</execution>
	</executions>
</plugin>
~~~



### 第三方Jar 手动发布

发布到本地仓库



发布到私服





## Maven 脚手架

archetype





## Maven 自定义打包

assembly



## 私服搭建