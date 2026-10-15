
# 如何在 Linux 上为 Tomcat 创建环境变量？

> 原文：[`techbyexample.com/environment-variable-tomcat/`](https://techbyexample.com/environment-variable-tomcat/)

假设 Tomcat 8 安装在 Linux 系统的`/var/lib/tomcat8/bin/`路径下。我们在一个示例文件`setenv.sh`中包含了所有环境变量，如下所示。

**`setenv.sh`的内容：**

```bash
export variable=value
```

请按照以下步骤操作。这将导出可以被 Tomcat 服务访问的环境变量。

```bash
sudo su
cd /var/lib/tomcat8/bin/
cp /User/testuser/setenv.sh .
chmod 777 setenv.sh
sudo service tomcat8 restart
```
