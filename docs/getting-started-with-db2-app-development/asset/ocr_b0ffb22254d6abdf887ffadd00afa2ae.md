The two pages mentioned in requirement #3 above will correspond to two resources: *book* and *catalog* which we will build later with the `scaffold` command.

In this particular example, the RoR application, the WebBrick server, and the DB2 server are all running on the same Windows machine. Therefore, when configuring the `database.yml` file, we will specify localhost.

# 7.3.1.1 Creating a DB2 database

Let's create the *booksdb* database using the following command from the DB2 Command Window, or Linux/UNIX shell:

```
```
db2 create db booksdb using codeset utf-8 territory us
```
```

This may take few minutes as DB2 is creating some internal objects, and performing some autoconfiguration. As mentioned earlier, you do not need to create the *books* table using DB2 tools. This will be created through RoR.

# 7.3.1.2 Creating the application structure

Let's create the *bookapp* application by opening a terminal, navigating to a folder where you have rights to create files (we refer to it as `<app_home>` from now on), and typing the following:

```
```
rails -d ibm_db bookapp
```
```

With this command, the *bookapp* application is created. The `-d ibm_db` indicates it should be preconfigured for a DB2 database using the ibm_db adapter. *Figure 7.16* shows you the output of the command.