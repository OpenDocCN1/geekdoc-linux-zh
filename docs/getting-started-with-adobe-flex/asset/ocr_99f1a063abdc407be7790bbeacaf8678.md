```
```java
public double getSalary() {
    return salary;
}
public void setSalary(double salary) {
    this.salary = salary;
}
```

```

# Listing 7.14 - Employee.java

# 7.5.1.5 Create JSPs

As explained earlier, Flex can access the database through RPC based services and when you are using HTTPService, you cannot call the Java method directly. You need a URL to access the data and the data must be in a format understandable by Flex like XML. So, now two JSPs will be needed which will access these Java classes and send the details required in XML format.

One JSP will be required to fetch all the employees from the database and return an XML of employee list. This is shown in *Listing 7.15* for `EmployeeList.jsp`

```
```
<%@ page language="java" contentType="text/xml; charset=UTF-8" %>
<%@ page import="com.example.emp.service.EmployeeService" %>
<%@ page import="com.example.emp.model.Employee" %>
<%@ page import="java.util.ArrayList" %>
<?xml version="1.0" encoding="UTF-8" ?>
<ITEM>
<%
    EmployeeService svc=EmployeeService.getInstance();
    ArrayList<Employee> empList=svc.getAllEmployees();
    for(Employee e:empList) {
        <EMPLOYEE>
            <EMPNO><%=e.getEmpNo() %></EMPNO>
            <EMPNAME><%= e.getFirstName() + " " + e.getMidInit() + (e.getMidInit()==null?"":" ")+e.getLastName() %></EMPNAME>
            <JOB><%= e.getJob() %></JOB>
        </EMPLOYEE>
    }
%>
</ITEM>
```

```

# Listing 7.15 - EmployeeList.jsp

Next, another JSP will be used to obtain details of the required employee based on parameter *empNo*. The code for this JSP is shown in *Listing 7.16* for `EmployeeDetails.jsp`

```
```xml
<?xml version="1.0" encoding="UTF-8" ?>
```

```