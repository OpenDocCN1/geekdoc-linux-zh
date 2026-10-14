
<server>

<log>

<log-file>../logs/errors</log-file>

<archive-suffix>%Y%m%d</archive-suffix>

<log-level>info</log-level>

</log>

```
<!-- 增加每个线程的输出缓冲区大小。这允许 Web Server 接收来自来自 j2ee-module SAF 的数据并为慢客户端进行缓冲。这反过来允许 j2ee-module 及时返回系统资源。 -->
```

<http>

  <output-buffer-size>40960</output-buffer-size>

</http>

<!-- 对于具有更深调用栈深度的 Java Web 应用程序，具有较高栈大小的典型工作线程池并不罕见 -->

<thread-pool>

  <max-threads>250</max-threads>

  <stack-size>256000</stack-size>

</thread-pool>

<!-- JVM 虚拟机设置 -->

<jvm>

  <java-home>.../java-home</java-home>

  <server-class>.../server-class-path</server-class>

  <debug-false=debug>

  <jvm-options>-Xdebug -Xrunjdwp:transport=dt_socket,server=y,
    suspend=n,address=7896</jvm-options>

  <jvm-options>-Dsecurity.auth.login.config=login.conf</jvm-options>

<!-- 增加了 ms 和 mx，默认情况下为 -Xms128m -Xmx256m

<jvm-options>-server -XX:NewSize=1g</jvm-options>-XX:+ParallelGC</jvm-options>

  <jvm-options>-XX:+UseParallelGC -XX:+ParallelGCThreads=20</jvm-options>

<!-- 添加了密钥库位置 -->

<jvm-options>-Dcom.sun.management.jmxremote -Djavax.net.ssl.keyStore=....keystore -Djavax.net.ssl.keyPassword=...</jvm-options>

</jvm>

<!-- 将 MySQL 数据源配置为 JDBC 资源 -->

<jdbc-resource>

  <jdbc-name>jdbc:rollerdb</jdbc-name>

  <datasource-class>com.mysql.jdbc.optional.MysqlDataSource</datasource-class>

  <property>

    <name>Password</name>

    <value>...</value>

    <description/>

  </property>

  <property>

    <name>User</name>

    <value>...</value>

    <description/>

  </property>

</jdbc-resource>

```

```

<name>URL</name>

<value>jdbc:mysql://some:3306/database?autoCommit=true&unicode=true&characterEncoding=utf-8</value>

<description/>

</property>

<description>datasource</description>

<min-connections>15</min-connections>

<max-connections>250</max-connections>

<idle-timeout>180</idle-timeout>

<connection-validation>metadata</connection-validation>

</jdbc-resource>

<mail-resource>

<jndi-name>mail/Session</jndi-name>

<description>roller session</description>

<property>

<name>mail.smtp.host</name>

<value>host</value>

<description>Mail hostname</description>

</property>

</mail-resource>

<!-- Web 应用程序在虚拟服务器中配置

所有 URI 为 '/' 的流量都会执行 Web 应用程序 -->

<virtual-server>

<name>blogs</name>

<host>blogs</host>

<listener-name>http-1</listener-name>

<web-app>

<uri>/</uri>

<path>_default</path>

<description/>

</web-app>

</virtual-server>

```

## 12.2 Site：SUN FORUMS

Sun Forums 基于 Jive Forums，这是一个 Java Web 应用程序，以简单的 WAR 文件形式部署在运行 Java 平台标准版 `Java SE` 6 的 Web 服务器上。Jive 部署在 Web Server 7.0 上，运行在两台配备 8GB 内存的 Sun Fire V40Z 服务器上。这些服务器连接到运行 Solaris 10 操作系统的 Sun F490 服务器上的 Oracle 10g 数据库服务器。

与 Sun Blogs（第 12.1 节）类似，支持此应用程序的 Web 服务器所需的配置很少。示例 12.2 展示了为了获得所需的站点性能所需的配置更改。并未列出整个 `server xml` 文件，而是提供了相关部分并显示了内联注释。

### 示例 12.2 Sun Forum 服务器配置

```xml
<server>

<!-- Java VM 设置，三十位服务器的最大可用堆大小，并行 GC 选项以及 Tangosol 相性备份 -->
<jvm>
<jvm-options>-Xms2048m -Xmx2748m -server -XX:+UseParallelGC -XX:+Parallel1DGC -XX:ParallelGCThreads=4 -XX:+AggressiveOpts/></jvm-options>
</jvm-options>
<jvm-options>
<jvm-options>-Dtangasol.coherence.localhost=72.5.126.82</jvm-options>
</jvm>
```

```xml
-- 略高的 keep-alive 线程设置，表示预计的并发 HTTP 连接更高 --
<keep-alive>
<threads>8</threads>
</keep-alive>
```

```xml
-- 典型的工作线程池，对于调用栈深度较深的 Java Web 应用程序，较大的栈大小并不罕见 --
<thread-pool>
<min-threads>128</min-threads>
<max-threads>256</max-threads>
<stack-size>262144</stack-size>
</thread-pool>
```

```xml
-- 配置为 JDBC 资源的 Oracle 数据源 --
<resource>
<jndi-name>jdbc:jdcforum/jndi-name</jndi-name>
<datasource-class>oracle.jdbc.pool.OracleDataSource</datasource-class>
<min-connections>130</min-connections>
<max-connections>200</max-connections>
<idle-timeout>0</idle-timeout>
```

```xml
<isolation-level>read-committed</isolation-level>
<property>
  <name>MaxStatements</name>
  <value>200</value>
</property>
<property>
  <name>ImplicitCachingEnabled</name>
  <value>true</value>
</property>
<jdbc-resource>
```

```xml
```
