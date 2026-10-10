Two files will be added to this package.

+   * One under the sub-package model – Employee.java. This is a simple java bean with getter and setter methods that represent the Employee entity in the database.
+   * One under the sub-package service – EmployeeService.java. This contains the business methods for the employee application.

After adding the two files, your Project structure must look as shown in Figure 7.16

![](bbox=[0.16, 0.29, 0.52, 0.51])

# **Figure 7.16 - Project structure after adding the Java code**

The EmployeeService.java has 4 important methods. Out of these four, two methods contain the business logic – getAllEmployees() and getEmployeeById(). The other two are private methods used by the class to access the database and execute the query.

+   * getAllEmployees – This method returns a list of all the employees from the database to the caller.
+   * getEmployeeById – This method returns the details of employees based on the Id (primary key), which is passed as parameter by the caller to this method.
+   * establishConnection – This method checks for an existing connection and returns it if found, else it creates a new one and returns that to the caller.
+   * executeQuery – This method executes the query and returns the result set to the caller based upon the query string passed to it. This avoids repeating the same code.

*Listing 7.13 below shows the code for EmployeeService.java*

```
```
package com.example.emp.service;

import java.sql.Connection;
import java.sql.DriverManager;
```
```