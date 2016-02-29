看看传统web开发模式下直接方式的数据库访问代码，总结

* 先要指定数据库的目标地址，用户名密码连接到数据库，获取一个连接对象供之后使用
* 从连接对象上下文中提交拼接好的SQL字符串提交数据库
* 通过 API 取得结果集信息，可能是数组，可能是迭代器
* 关闭连接
* 以上每步都要处理数据库调用的异常

而使用存储过程开发，直接就嵌入了SQL

### PHP

A demo for access PostgreSQL database:

```php
<?
   $conn = pg_Connect("localhost", "5432", "", "", "mydb");
   if (!$conn) {
      echo "An error occured.\n";
      exit;
   }

   $result = pg_Exec($conn, "select * from table1");
   if (!$result) {
      echo "An error occured.\n";
      exit;
   }

   $num = pg_NumRows($result);
   $i = 0;

   while ($i < $num) {
      echo "name: ";
      echo pg_Result($result, $i, "name");
      echo "  age: ";
      echo pg_Result($result, $i, "age");
      echo "<BR>";
      $i++;
   }

   pg_FreeResult($result);
   pg_Close($conn);
>
```


A demo for access ORACLE database:

```php
An example PHP/FI Oracle application:

<?
PutEnv("ORACLE_HOME=path_to_your_oracle_home"
PutEnv("ORACLE_SID=database"

/* Establish a connection between PHP and Oracle. */
$conn = Ora_Logon("username" "password"

if ($conn < 0) {
    echo("Could not connect to Oracle.\n"
    exit;
}

/* Open a cursor in Oracle. */
$cursor = Ora_Open($conn);

if ($cursor < 0) {
    echo("Could not open a cursor.\n"
    Ora_Logoff($conn);
    exit;
}

/* Turn off autocommit. */
Ora_CommitOff($conn);

/* This is the SQL query. */
$query = "SELECT * FROM some_table"

if (Ora_Parse($cursor, $query) < 0) {
    echo("Parse failed!\n"
    Ora_Logoff($conn);
    exit;
}

/* Execute the SQL statement associated with $cursor and
   prepare storage for select-list items. */
$ncols = Ora_Exec($cursor);

echo "lt;P>\n"
echo "lt;TABLE BORDER=1 CELLSPACING=0>\n"

/*  Retrieve all rows from the database one after another. */
while (Ora_Fetch($cursor) == 1) {
    $i = 0;
    echo "lt;TR>\n"
    while ($i < $ncols) {
     /* Get data for a single column of currently fetched row. */
     $col = Ora_GetColumn($cursor, $i);
        echo("lt;TD>$col</TD>\n"
     $i++;
    }
    echo("lt;/TR>\n"
}

echo "</TABLE>\n";

/* Close the Oracle connection. */
Ora_Close($cursor);
 
/* Disconnect the logon data area. */
Ora_Logoff($conn);
>
```
