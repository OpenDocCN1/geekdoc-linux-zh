For example, let's say you want to call the SQL procedure **sp_get_employees** shown in *Listing 9.9*.

```
CREATE PROCEDURE sp_get_employees (IN dept_no CHAR(3), OUT dept_name 
VARCHAR(36)) 
DYNAMIC RESULT SETS 1 
BEGIN
    DECLARE emp_cursor CURSOR WITH RETURN TO CLIENT FOR 
    SELECT firstname, lastname FROM employee workdept=dept_no; 
    OPEN emp_cursor; 
    SELECT deptname INTO dept_name FROM department WHERE deptno=dept_no; 
END @
```

# Listing 9.9 – sp_get_employees.db2

**sp_get_employees** has two parameters, the input parameter **dept_no** and the output parameter **dept_name**. It also returns one result set to the client which is defined in the cursor *emp_cursor*.

You can prepare the CALL statement as follows:

```
$shandle = $dbhandle->prepare( "CALL sp_get_employees(?,?)" );
```

The two parameters are represented as the parameter markers "?" in the CALL statement. After a successful prepare, the statement handle is returned in the variable *$shandle*.

+   3. Call **bind_param** or **bind_param_inout** method on the statement handle to bind parameters to local Perl variables or values. **bind_param** can be used for binding **IN** parameters only, while **bind_param_inout** is used for binding **IN/INOUT/OUT** parameters.

Refer to the previous section for the syntax of **bind_param**. The syntax of **bind_param_inout** method is:

```
$rv = $sth->bind_param_inout($p_num, \$bind_value, $max_len, \$attr)
```

*Table 9.4* provides details about the parameters of **bind_param_inout**

| Name | Description |
| :--- | :--- |
| **$p_num** | Specifies the 1-indexed position of the parameter in the CALL statement. |
| **$bind_value** | A Perl variable or value to be bound to the parameter specified by **$p_num**. If it's OUT/INOUT parameter, a variable is used, otherwise it can be a variable or a value. |
| **$max_len** | Specifies the minimum amount of memory to allocate to **$bind_value**. |