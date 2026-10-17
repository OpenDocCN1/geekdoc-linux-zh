
# 按照以下步骤配置 Samba：

1. 打开终端窗口。
2. 进入 `/etc/samba/`，在提示符处执行 `touch smbpasswd`。
3. 在 `smb.conf` 文件中将 `workgroup` 参数更改为你的工作组。
4. 通过取消注释 `smb.conf` 文件中的这些变量来打开 `tmp` 目录。
5. 进入服务配置中的系统设置，激活 `smb` 代理并重启机器。

## 补充材料

本红书提到了下文所述的可以从网上下载的补充材料。

## 定位 Web 材料

与本红书相关的 Web 材料可以通过 IBM Redbooks Web 服务器以电子版形式在网上获取。将你的 Web 浏览器指向：

`ftp://www.redbooks.ibm.com/redbooks/SG246431/sg246431.tar`

或者，你可以访问 IBM Redbooks 网站：

`ibm.com/redbooks`

选择“Additional materials”（补充材料）并打开与红书表号 `SG246431` 对应的目录。

## 使用 Web 材料

随本红书的补充 Web 材料包含以下文件：

| 文件名 | 说明 |
| :--- | :--- |
| `SG246431.tar` | 示例和数据库脚本 |

## 下载 Web 材料的系统要求

推荐以下系统配置：

- **硬盘空间：** 至少 10 MB
- **操作系统：** Linux
- **处理器：** Pentium III 600Mhz 或更高
- **内存：** 512MB

## 如何使用 Web 材料

在你的工作站上创建一个子目录（文件夹），并将 Web 材料 zip 文件包的内容解压到此文件夹中。

目录：

- `BuildWithAnt`: Ant 示例
- `DBscripts`: 数据库生成
- `Deploy`: 部署示例
- `ServletSP`: 示例 Web 应用程序
- `XML`: XML 应用程序

## 缩写和术语

| AAT | application assembly tool | HTTP | Hypertext Transfer Protocol |
| :--- | :--- | :--- | :--- |
| ACL | access control list | IBM | International Business Machines |
| API | application programming interface | IDE | integrated development environment |
| BLOB | binary large object | IDL | Interface Definition |
| BMP | bean-managed persistence | IIOP | Internet ORB Protocol |
| CCF | Common Connector Framework | IMS | Information Management System |
| CICS | Customer Information System | ITS | International Technical Support |
| CMP | container-managed persistence | J2EE | Java Enterprise Edition |
| CORBA | Component Object Broker | J2E | Java Standard Edition |
| DBMS | database management system | JAF | Java Activation Framework |
| DDL | data definition | JDK | Java Database Connectivity |
| DLL | dynamic link library | JFC | Java Foundation Classes |
| DML | data manipulation language | JMS | Java Messaging Service |
| DOM | document model | NDI | Java Naming and Directory Interface |
| DTD | document type | JSDK | Java Servlet Development Kit |
| EAB | Enterprise Access | |Server Page |
| EAI | Enterprise Integration | JTA | Java Transaction API |
| EAR | Enterprise Application | JVM | Java Virtual Machine |
| EIS | Enterprise Information System | LDAP | Lightweight Directory Protocol |
| EJB | Enterprise JavaBeans | OO | object oriented |
| HTML | Hypertext Markup Language | MVC | model-controller |
| GUI | graphical user interface | OMG | Object Management Group |
| RAD | rapid application development | OTS | object transaction service |
| RDBMS | relational database system | WS | Web Service |
| RMI | Remote Method Invocation | WSDL | Web Service Description Language |
| SAX | Simple API for XML | WSK | Web Service Development Kit |
| SCCI | source control interface | WTE | WebSphere Environment |
| SCM | source code management | WWW | World Wide Web |
| SCMS | software configuration | VCE | visual composition editor |
| TCP/IP | Transmission Control Protocol/Internet Protocol | VXML | voice extensible language |
| UCM | Unified Change Management | WAR | Web application |
| UDB | Universal Database | UDDI | Universal Discovery, and Integration |
| UML | Unified Modeling Language | UOW | unit of work |
| URL | uniform resource locator | UMS | extensible language |
| WML | Wireless Markup Language | WAS | Web Server |

## 相关出版物

列出的出版物有助于更深入地讨论本书涵盖的主题。

### IBM Redbooks

关于订购这些出版物，请参见第 194 页的“How to get IBM Redbooks”。

- Linux for WebSphere and DB2, `SG24-5850`
- Linux Web Hosting with WebSphere, DB2 and Domino, `SG24-6007`
- WebSphere Application V4 for Linux - Implementation and Deployment
- IBM Framework for e-business - Technology, Solution and Design, `SG24-6248`
- Web Services Wizard with WebSphere Application, `SG24-6292`
- WebSphere Version 4 Application Handbook, `SG24-6134`
- IBM WebSphere V4.0 Advanced Edition Handbook, `SG24-6176`
- EJB Development with VisualAge for WebSphere Application, `SG24-6144`
- WebSphere Application Server Enterprise Edition 4.0 - A Programmer’s Guide, `SG24-6504`
