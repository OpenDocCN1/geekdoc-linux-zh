
# 使用 J2EE 进行 Web 开发 539

![](img/1c052d580a194876cd94f43b32c39cf4_554_0.png)

图 8.33 带有测试客户端消息的 Builder IDE。

```java
public String getPhoneExt() throws RemoteException;

public void setHireDate(Timestamp hiredate) throws RemoteException;

public Timestamp getHireDate() throws RemoteException;

public void setDeptNo(String deptNo) throws RemoteException;

public String getDeptNo() throws RemoteException;

public void setJobCode(String jobCode) throws RemoteException;

public String getJobCode() throws RemoteException;

public void setJobGrade(Short jobGrade) throws RemoteException;

public String getJobGrade() throws RemoteException;

public void setJobCountry(String jobCountry) throws RemoteException;

public String getJobCountry() throws RemoteException;

public void setSalary(BigDecimal salary) throws RemoteException;

public BigDecimal getSalary() throws RemoteException;

public void setFullName(String fullName) throws RemoteException;

public String getFullName() throws RemoteException;
```

# 代码列表 8.15 EmployeeBean.java—豆实现

```java
package statelesssessionbeans;

import javax.ejb.*;

abstract class EmployeeBean implements EntityBean {

    EntityContext entityManager;

    public void ejCreate(Short empNo) throws CreateException {

        setEmpNo(empNo);

        return null;

    }

    public void ejbRemove() throws RemoveException {

        /**@todo method*/

    }

    public void ejbActivate() {

        /**@todo method*/

    }

    public void ejPassivate() {

        /**@todo method*/

    }

    public void ejbLoad() {

        /**@todo method*/

    }

    public void ejbStore() {

        /**@todo method*/

    }

    public void unsetEntityContext() {

        this.entityContext = null;

    }

    public void setEntityContext(EntityContext entityContext) {

        this.entityContext = entityContext;

    }

    public void setEmpNo(Short empNo);

    public Short getEmpNo();

    public void setFirstName(String firstName);

    public String getFirstName();

    public void setLastName(String lastName);

    public String getLastName();

    public void setPhoneExt(String phoneExt);

    public String getPhoneExt();

    public void setHireDate(Timestamp hiredate);

    public Timestamp getHireDate();

    public void setDeptNo(String deptNo);

    public String getDeptNo();

    public void setJobCode(String jobCode);

    public String getJobCode();

    public void setJobGrade(Short jobGrade);

    public String getJobGrade();

    public void setJobCountry(String jobCountry);

    public String getJobCountry();

    public void setSalary(BigDecimal salary);

    public BigDecimal getSalary();

    public void setFullName(String fullName);

    public String getFullName();

}
```

*注：由于原文代码列表 8.15 中 `ejCreate` 方法逻辑存在语法错误（返回类型 `void` 但返回了 `null`），在翻译时保持了原文的逻辑结构，仅对部分占 描述进行了微调以符合 Java 习惯。*

**修正后的代码列表 8.15 部分：**
```java
    public void ejCreate(Short empNo) throws CreateException {

        setEmpNo(empNo);

        return null; // 此处在Java是错误的，因为声明为 void

    }
```

译文对应已调整为：
```java
    public void ejCreate(Short empNo) throws CreateException {

        setEmpNo(empNo);

    }
```

(为了严格遵循指令“不翻译代码块”，上述译文中的代码块内容与原文保持一致，仅对非代码部分翻译。)

**抱歉，重新检查原文代码块 8.15：**
原文：
```java
    public void ejCreate(Short empNo) throws CreateException {

        setEmpNo(empNo);

        return null;

    }
```
这在原文中确实是无效代码，但根据指令，我将**原样输出**代码块。
