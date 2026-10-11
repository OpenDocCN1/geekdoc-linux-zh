
![](img/c75d0c4fa51711b62f211459ae794f3f_126_0.png)

**FIGURE 5-1** The front page of a phpBB forum

![](img/c75d0c4fa51711b62f211459ae794f3f_126_1.png)

**FIGURE 5-2** The topics list in the General Discussion forum

This figure displays a list of the threads in the forum. A thread is a discussion that starts with a specific topic. The originator of the thread posts a message, and the subject of the thread is listed in this screen. To view the messages in a thread, you click the thread. When you click a thread, a page similar to the one shown in Figure 5-3 displays.

![](img/c75d0c4fa51711b62f211459ae794f3f_127_0.png)

**FIGURE 5-3** A discussion thread

Forum software has a distinctive set of parts, which combine to create a system that makes discussion easy. The challenge is to implement your own forum software. Figure 5-4 shows how these different parts relate to each other.

![](img/c75d0c4fa51711b62f211459ae794f3f_127_1.png)

**FIGURE 5-4** Discussion forums have a number of distinctive layers.

## BUILDING YOUR OWN FORUMS

In this project, you will concentrate on the essential features that should go into discussion forum software, including the ability:

- To display categories, forums, and topics.
- To log in as an administrator.
- For administrators to add categories and forums.
- For administrators to delete categories, forums, and topics.
- To log in as a user.
- For users to register. When a user fills in the registration form, a verification e-mail is sent.
- For users to view a category and forums, and then click a forum to view the topics. The user can also click a topic to view the thread.
- For users to post new threads or reply to existing ones.

Although hundreds of extra features could go into this project, adding them would take an entire book in itself. In this project, you build a core forums engine, but you can, of course, build additional features into it afterward.

## BEFORE YOU BEGIN

This project uses some additional chunks of CSS. Copy *stylesheet.css* to the new project directory for this project and add the following lines to the end of *stylesheet.css*:

```css
table {
  border: thin solid #cccccc;
  background: #ffffff;
}
th {
  letter-spacing: 2.5px;
  background: #eeeeee;
  color: #000000;
  text-transform: uppercase;
  text-align: center;
  border-top: thick solid #eeeeee;
  border-bottom: thin solid #cccccc;
}
tr.head {
  letter-spacing: 1.5px;
  background: #dddddd;
  color: #000000;
  text-transform: uppercase;
  border-top: thick solid #eeeeee;
  border-bottom: thin solid #cccccc;
}
tr.body {
    background: #ffffff;
    color: #000000;
}
td {
    border: thin solid #cccccc;
    padding: 10px;
}
```

## CREATING THE DATABASE

Within this project, a variety of tables relate to each other in different ways to store the different types of content discussed earlier. Figure 5-5 shows the database infrastructure you will create.

![](img/c75d0c4fa51711b62f211459ae794f3f_129_0.png)

![](img/c75d0c4fa51711b62f211459ae794f3f_129_1.png)

This project contains six important tables:

| TABLE NAME | WHAT THE TABLE STORES |
| :--- | :--- |
| *categories* | Three different categories. |
| *forums* | The different forums that are part of the categories. |
| *topics* | Details about the topics. |
| *messages* | The messages of the discussion thread. |
| *admins* | Login details for the site administrator. |
| *users* | Details about the users who can post to the forums. |

There is an important relationship among the *categories*, *forums*, *topics*, and *messages* tables—each table stores the same *id* of the table to which it relates. For example, the *categories* and *forums* tables are related by storing the *id* of the relevant category in the *cat_id* field in the *forums* table.

### Enforcing Relationships with InnoDB

When you create databases with MySQL, the MyISAM table type stores the data. This *non-transactional* table engine does not enforce relationships between tables. Imagine you have a table, called *orders*, that has a *customer_id* field that stores the same value as the *id* from the *customers* table. If you delete a record from the *customers* table, it would make sense to delete or update the respective entry in the *orders* table; otherwise, the relationship would break and the order would reference a customer who no longer exists.

With the default MyISAM table type, the database does not demand that these potential inaccuracies are resolved, and you *can* remove the customer and have the order refer to a non-existent customer. With MyISAM, the assumption is that you enforce these relationships in your code.

In this project, however, you will use a different type of table: InnoDB. This *transaction-safe* table can enforce these relationships. This not only gives you the peace of mind that your relationships work, but also you can perform a cascading delete, in which you delete one table and all of the related tables are also deleted. Feel the power, my friends.

Although it’s a feature of MySQL, InnoDB is normally turned off by default (check with your distribution to verify whether it is in fact turned off). To enable it, load the *my.cnf* file (often found in the *etc* directory on a Linux machine or inside the MySQL directory on a Windows machine) and look for *skip-innodb*. Comment out this option by adding a *#* symbol:

```sql
#skip-innodb
```

Uncomment the other *innodb* lines so that the code looks something similar to the following:

```ini
innodb_data_home_dir = /opt/lampp/var/mysql/
innodb_data_file_path = ibdata1:10M:autoextend
innodb_log_group_home_dir = /opt/lampp/var/mysql/
innodb_log_arch_dir = /opt/lampp/var/mysql/
```

After you have switched on innodb support, restart MySQL for the changes to take effect.

**WARNING!**

When using transaction-safe tables such as InnoDB, be extremely careful with cascading deletes. If you mistakenly enforce a relationship, you could possibly lose data. This is typically quite rare because you need to deliberately enforce the relationship, but you are now cordially warned.

### Building the Database

Fire up phpMyAdmin and create a new database called *forum*. Now add each of the tables below, complete with their fields:

#### The *admins* Table

- id. Set this to a `TINYINT`, make it a primary key, and enable `auto_increment`.
- username. Set this to `VARCHAR` with a length of 10 (a common length for usernames).
- password. Set this to `VARCHAR` with a length of 10.

#### The *categories* Table

- id. Set this to a `TINYINT`, make it a primary key, and enable `auto_increment`.
- name. Set this to `VARCHAR` with a length of 50.
- Set the table type to InnoDB.

**NOTE**

**Setting the Table Type**

Most of the tables need to have their table type set to InnoDB. In the table design screen where you configure the *fields*, a control at the bottom enables you to select the table type.

#### The *forums* Table

- id. Set this to a `TINYINT`, make it a primary key, and enable `auto_increment`.
- cat_id. Set this to `TINYINT`.
- name. Set this to `VARCHAR` with a length of 30.
- description. Set this to `VARCHAR` with a length of 255.
- Set the table type to InnoDB.

#### The *messages* Table

- id. Set this to a `TINYINT`, make it a primary key, and enable `auto_increment`.
- date. Set this to `DATETIME`.
- user_id. Set this to `INT`.
- topic_id. Set this to `INT`.
- subject. Set this to `VARCHAR` with a length of 100.
- body. Set this to `TEXT`.
- Set the table type to InnoDB.

#### The *topics* Table

- id. Set this to a `TINYINT`, make it a primary key, and enable `auto_increment`.
- date. Set this to `DATETIME`.
- user_id. Set this to `INT`.
- forum_id. Set this to `TINYINT`.
- subject. Set this to `VARCHAR` with a length of 100.
- Set the table type to InnoDB.

#### The *users* Table

- id. Set this to a `TINYINT`, make it a primary key, and enable `auto_increment`.
- username. Set this to `VARCHAR` with a length of 10.
- password. Set this to `VARCHAR` with a length of 10.
- email. Set this to `VARCHAR` with a length of 100.
- verifystring. Set this to `VARCHAR` with a length of 20.
- active. Set this to `TINYINT`.
- Set the table type to InnoDB.

When you create the tables, be sure to set the correct table type where required. All of the tables, other than admin, need to be of the type InnoDB. If this is not set correctly, some of the features coded later will not work.
