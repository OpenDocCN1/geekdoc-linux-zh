
# 录 A • 购物车应用程序 PHP 脚本

```php
function delete_item() {
  global $delete_id;
  If ($delete_id="") {
    // 从购物车中删除商品
    $query = "DELETE FROM carts WHERE cart_id='$delete_id'";
    $result = MYSQL_QUERY($query);
  }
}

// 显示前向购物车购买（添加）商品
function buy_item() {
  global $buy_id;
  global $session_id;
  If ($buy_id="") {
    // 将此商品插入购物车
    $query = "INSERT INTO carts (session_id,item_id) VALUES ('$session_id',";
    $query = $query.'$buy_id')";
    $result = MYSQL_QUERY($query);
  }
}

// 打印购物车内容
function print_shopping_cart() {
  global $session_id;
  global $shopping_cart_color;
  global $shopping_cart_width;
  global $PHP_SELF;
  global $session_status;
  global $uc_user_first_name;
  global $user_perm;
  global $total;
  global $items_in_cart;
  $query="SELECT items.item_id, items.item_name, items.item_price, ";
  $query=$query.'carts.cart_id FROM items, carts WHERE carts.session_id = ";
  $query=$query.'$session_id' AND carts.item_id=items.item_id ORDER BY ";
  $query=$query.'items.item_name";
  $result=mysql_query($query);
  If (mysql_num_rows($result)>0) {
    If ($session_status==0) {
      Print "<FONT FACE='Helvetica, Verdana, Arial' COLOR=";
      Print "$shopping_cart_font_color>$uc_user_first_name's ";
      Print "选择:<BR></FONT>\n";
    Else:
    Print "<FONT FACE='Helvetica, Verdana, Arial COLOR=";
    Print "$shopping_cart_font_color>我的选择:<BR></FONT>\n";
    Endif;
  Endif;
  // 开始微表格
  Print "<TABLE WIDTH=100 ORDER=0 CELLACING='0' CELLPADDING='0'>\n";
  Print "<TR><TD SRC='img/clear.gif' HEIGHT='10' WIDTH=";
  Print "$shopping_cart_width'></TD></TR>;\n";
  $items_in_cart=0;
  WHILE($row=mysql_fetch_array($result)) {
    $items_in_cart++;
    $cart_id=$row["cart_id"];
    $item_id=$row["item_id"];
    $item_name=$row["item_name"];
    $item_price=$row["item_price"];
    $total=$item_price=$total;
    // 允许在购物车中查看商品。
    Print "<TR><TD VALIGN='TOP'>";
    Print "<a href='review.php?review_cart_id=$cart_id";
    Print "&amp;review_item_id=$item_id\">";
    Print "<FONT FACE='Helvetica, Verdana, Arial' SIZE=-3 COLOR=";
    Print "$shopping_cart_font_color>$item_name</FONT>";
    Print "</a></TD>";
    Print "<TD VALIGN='RIGHT'><FONT FACE='Helvetica, Verdana, Arial, ";
    Print "Arial SIZE=-2 COLOR='#shopping_cart_font_color'>";
    $item_price_str=number_format($item_price,2,'.','\');
    Print "$$item_price_str</FONT></TD>";
    Print "<TR><TD COLSPAN=2><IMG SRC='img/clear.gif' HEIGHT='5' ";
    Print "WIDTH='$shopping_cart_width'></TD></TR>;\n";
  }
  If ($items_in_cart>0) {
    Print "<TR><TD VALIGN='TOP'>";
    Print "<FONT FACE='Helvetica, Verdana, Arial' SIZE=-3 COLOR=";
    Print "$shopping_cart_font_color>总计:</FONT>";
    Print "</TD>";
    Print "<TD VALIGN='RIGHT'><FONT FACE='Helvetica, Verdana, ";
    Print "Arial SIZE=-2 COLOR='#shopping_cart_font_color'>";
    $total_str=number_format($total,2,'.','\');
    Print "$$total_str</FONT></TD>";
  }
}
```

```php
Print "<TR><TD COLSPAN=2><IMG SRC=img/clear.gif' HEIGHT='5' WIDTH=";
Print "$shopping_cart_width'>TD</TR>";
Endif;
Print "</TABLE>\n"
// end microtable
```

) // 开始浏览列

```php
function start_browse_column()
{
    global $browse_color;
    global $browse_font_color;
    Print "<TD WIDTH='100%' ALIGN BGCOLOR='#$browse_color' ROWSPAN=1'>";
    Print "<FONT FACE='Helvetica, Verdana, Arial' COLOR='#$browse_font_color'>";
```
