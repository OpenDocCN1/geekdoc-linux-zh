
`search_column();`

Else:

    `browse_column();`

Endif;

// 显示页面底部

`end_shop_column();`

`divide_colv();`

`end_browse_column();`

`end_shop_browse_table();`

# 购物车应用程序导出文件

## 460 附录 B 购物车应用程序转文件

```sql
# phpMyAdmin MySQL-Dump
# http://phppwizard.net/phpAdmin/
#
# Host: localhost Database : shopcart
--------------------------------------
#
# 表 'carts' 的表结构
#
CREATE TABLE carts (
  cart_id mediumint(9) DEFAULT '0' NOT NULL auto_increment,
  session_id tinyint(4) DEFAULT '0' NOT NULL,
  item_id tinyint(4) DEFAULT '0' NOT NULL,
  PRIMARY KEY (cart_id),
  KEY session_id (session_id, item_id)
);
--------------------------------------
#
# 表 'categories' 的表结构
#
CREATE TABLE categories (
  category_id tinyint(4) DEFAULT '0' NOT NULL auto_increment,
  category_name varchar(15) NOT NULL,
  PRIMARY KEY (category_id),
  KEY category_id (category_id),
  UNIQUE category_name (category_name)
);
--------------------------------------
#
# 表 'images' 的表结构
#
CREATE TABLE images (
  image_id mediumint(9) DEFAULT '0' NOT NULL auto_increment,
  image_type varchar(30) NOT NULL,
  image_data longblob,
  PRIMARY KEY (image_id)
);
```

附录 B • 购物车应用程序导出文件 461

```sql
#
# ------------------------------------------------------
# # 表 'items' 的表结构
#
CREATE TABLE items (
item_id int(11) DEFAULT '0' NOT NULL auto_increment,
item_name varchar(30),
item_description tinytext,
item_price float(10,2) DEFAULT '0.00' NOT NULL,
category_id tinyint(4) DEFAULT '0' NOT NULL,
image_id mediumint(9) DEFAULT '0' NOT NULL,
PRIMARY KEY (item_id),
KEY image_id (image_id),
KEY category_id (category_id)
);
```

```sql
#
# ------------------------------------------------------
# # 表 'sessions' 的表结构
#
CREATE TABLE sessions (
session_id int(11) DEFAULT '0' NOT NULL auto_increment,
user_id int(11) DEFAULT '0',
session_status tinyint(4) DEFAULT '0' NOT NULL,
category_id tinyint(4),
PRIMARY KEY (session_id)
);
```

```sql
#
# ------------------------------------------------------
# # 表 'users' 的表结构
#
CREATE TABLE users (
user_id int(11) DEFAULT '0' NOT NULL auto_increment,
user_first_name varchar(15),
user_last_name varchar(15),
user_mail_address varchar(100),
user_credit_card varchar(20),
user_password varchar(30) NOT NULL,
user_perm tinyint(4) DEFAULT '0' NOT NULL,
PRIMARY KEY (user_id)
);
```
