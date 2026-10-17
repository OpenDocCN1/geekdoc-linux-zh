
```perl
my $self = shift;

if (@_) $self->(FIRST_NAME) = shift }

return $self->(FIRST_NAME);
```

```perl
sub middle_initial {
    my $self = shift;
    if (@_) $self->(MIDDLE_INITIAL) = shift }
    return $self->(MIDDLE_INITIAL);
}
```

```perl
sub last_name {
    my $self = shift;
    if (@_) $self->(LAST_NAME) = shift }
    return $self->(LAST_NAME);
}
```

```perl
sub address_line_1 {
    my $self = shift;
    if (@_) $self->(ADDRESS_LINE_1) = shift }
    return $self->(ADDRESS_LINE_1);
}
```

```perl
sub address_line_2 {
    my $self = shift;
    if (@_) $self->(ADDRESS_LINE_2) = shift }
    return $self->(ADDRESS_LINE_2);
}
```

```perl
sub city {
    my $self = shift;
    if (@_) $self->(CITY) = shift }
    return $self->(CITY);
}
```

```perl
sub state {
    my $self = shift;
    if (@_) $self->(STATE) = shift }
    return $self->(STATE);
}
```

################################################################

#
# primary_key - 上述特殊情况将
# 将适当的值赋值给适当的主
# 键字段
#
#
################################################################

```perl
sub primary_key {
    my $self = shift;
    if (@_) $self->(CUSTOMER_ID) = shift }
    return $self->(CUSTOMER_ID);
}
```

################################################################

#
# insert - 编写将数据插入数据库的查询
#
#
################################################################

```perl
sub insert {
    my $self = shift;
    # 连接到数据库
    $dbname='='order_entry_db
    $user='dba';
    $password='dba2pass';
    $dbd='mysql
    $dbh=DBI->connect($dbname, $user, $password, $dbd);
    if (!$dbh) {
        print "ERROR connecting to database:$DBI::errstr\n"
    }else {
        print "connecting to database...\n"
    }
```

```perl
# 创建使用的本地变量
my $cust_id=$self->customer_id;
my $first_name=$self->first_name;
my $middle_initial=$self->middle_initial;
my $last_name=$self->last_name;
my $address_line_1=$self->address_line_1;
my $address_line_2=$self->address_line_2;
my $city=$self->city;
my $state=$self->state;
my $zip=$self->zip;
my $phone_number=$self->phone_number;
```

```perl
# 创建查询
my $query="insert into customer values (\n'$cust_id','$first_name','$middle_initial','$last_name',
'$address_line_1','$address_line_2',
'$city','$state','$zip',
'$phone_number','$N')")
```

```perl
# 执行查询
print "preparing and executing sql...\n"
my $sth=$dbh->prepare("$query");
my $error=$sth->execute();
$sth->finish();
$dbh->disconnect();
return $error;
}
}
```

####################################################
#
# browse - 写入用于从数据库选择数据的查询语句
#
####################################################

```perl
sub browse(
    my $self = shift;
    # 连接数据库
    my $dbname='order_entry_db'
    my $user='dba'
    my $password='dba2pass'
    my $dbd='mysql'
    my $dbh=DBI->connect($dbname, $user, $password, $dbd)
    if (!$dbh) {
        print "ERROR connecting to database: DBI::errstr\n"
    } else {
        print "connecting to database......\n"
    }
    # 创建查询
    my $query="select * from customer where 1=1 "
    foreach $field (keys(%$self)) {
        if($self->{$field}) {
            $query=$query."and $field = ${self->{$field}}"
        }
        $index[$ii]=$field;
        $ii++;
    }
    # 执行查询
    my $sth=$dbh->prepare("$query")
    my $error=$sth->execute()
    my @fields=undef;
    # 打印行
    while(@fields=$sth->fetchrow_array) {
        print "@fields\n"
    }
    # 清理
    $sth->finish;
    $dbh->disconnect();
    return $error;
}
```

######################################################################
#
#
# delete - 写入用于从数据库删除数据的查询语句
#
#
#
######################################################################

```perl
sub delete {
    my $self = shift;
    # 连接数据库
    my $dbname='order_entry_db'
    my $user='dba'
    my $password='dbapass'
    my $dbd='mysql'
    my $dbh=DBI->connect($dbname, $user, $password, $dbd)
    if (!$dbh) {
        print "ERROR connecting to database: $DBI::errstr\n"
    } else {
        print "connecting to database......\n"
    }
```
