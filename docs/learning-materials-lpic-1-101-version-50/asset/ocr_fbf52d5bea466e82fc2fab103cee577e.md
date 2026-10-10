# # Answers to Explorational Exercises

+   1. The SIGHUP signal can be used as a way to restart certain daemons. With the **Apache HTTPD web server** — for example — sending SIGHUP to the parent process (the one started by init) kills off its children. The parent, however, re-reads its configuration files, re-opens log files and spawns a new set of children. Do the following tasks:

+   * Start the web server:

```
$ sudo systemctl start apache2
```

+   * Make sure you know the PID of the parent process:

```
$ ps aux | grep apache2
```

The parent process is that started by the root user. In our case the one with PID 1653.

+   * Make the Apache HTTPD web server restart by sending it the SIGHUP signal to the parent process:

```
$ kill -SIGHUP 1653
```

+   * Check that the parent was not killed and that new children have been spawned:

```
$ ps aux | grep apache2
```

Now you should see the parent apache2 process together with two new children.

+   2. Although initially static, the output of ps can be *turned* dynamic by combining ps and watch. We will monitor the **Apache HTTPD web server** for new connections. Before doing the tasks described below it is recommended that you read the description of the MaxConnectionsPerChild directive in **Apache MPM Common Directives**.

+   * Add the **MaxConnectionsPerChild** directive with a value of 1 in the config file of apache2 — in *Debian* and derivatives that is found in /etc/apache2/apache2.conf; in the **CentOS** family, in /etc/httpd/conf/httpd.conf. Do not forget to restart apache2 for the changes to take effect.

The line to include in the config file is **MaxConnectionsPerChild 1**. One way to restart the web server is through **sudo systemctl restart apache2**.