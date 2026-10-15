
## `set_color_theme` 函数

```php
function set_color_theme()
{
    // 设置颜色方案
    global $body_background_color;
    global $body_font_color;
    global $top_header_color;
    global $top_header_company_font_color;
    global $main_index_tab_color;
    global $main_index_tab_font_color;
    global $index_tab_color;
    global $index_tab_font_color;
    global $dividing_hline_color;
    global $dividing_vline_color;
    global $shopping_cart_color;
    global $shopping_cart_font_color;
    global $browse_color;
    global $browse_font_color;
    global $shopping_cart_width; // 最小宽度
    global $shopping_cart_height; // 最小高度
    global $company_name;
    global $search_categories; // 如果 $search_categories=='current'，则只有当前类别会被搜索。
    global $table_row_rows;
    global $table_row_cols;
    global $table_row_5=5;
    global $table_row_cols=30;
    $body_background_color='336699';
    $body_font_color='000000';
    $top_header_color='336699';
    $top_header_font_color='EEEEEE';
    $main_index_tab_color='990000';
    $main_index_tab_font_color='EEEEEE';
    $index_tab_color='003366';
    $index_tab_font_color='EEEEEE';
    $dividing_hline_color='990000';
    $dividing_vline_color='990000';
    $shopping_cart_color='336699';
    $shopping_cart_font_color='FFFFFFFF';
    $browse_color='FFFFFFFF';
    $browse_font_color='336699';
    $shopping_cart_width='100'; // 最小宽度
    $shopping_cart_height='0'; // 最小高度
    $company_name='phpshopcart.org';
    // 如果 $search_categories=='current'，则只有当前类别会被
    // 搜索。
    // $search_categories=='current';
}
```

## `connect_db` 函数

```php
// 初始化数据库连接
// 用户名和密码应该存储在独立的非公共文件中
// 并在此处
// include()' 它们。
function connect_db()

    global $db_server;
    global $db_username;
    global $db_password;
    MYSQL_CONNECT($db_server,$db_username,$db_password) OR DIE("无法连接到数据库");
    @MYSQL_SELECT_DB($db_name) or die("无法选择数据库");
}
```

## `display_image` 函数

```php
// 请求图片，显示图片并退出。退出 是关键的！
function display_image()
{
    global $image_id;
    $result=mysql_query("SELECT * FROM images WHERE image_id=$image_id");
    while ($row=mysql_fetch_array($result)) {
        $image_type=$row["image_type"];
        $image_data=$row["image_data"];
        header("Content-type: $image_type");
        print $image_data;
        exit();
    }
}
```
