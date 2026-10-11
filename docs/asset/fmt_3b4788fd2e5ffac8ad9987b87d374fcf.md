
`return String.format("%s: %s\n%s: %s\n%s: %s", "employee", firstName, "lastName", lastName, "social security number", socialSecurityNumber);`

} // end method toString

**图 9.9** | 带有 protected 实例变量的 CommissionEmployee2。（3部分第3部分）

我们将 `CommissionEmployee` 的实例变量 `firstName`、`lastName`、`socialSecurityNumber`、`grossSales` 和 `commissionRate` 声明为 `public`，以便子类访问超类变量。然而，将实例变量声明为 `public` 是一种糟糕的工程实践，因为它允许无限制地访问实例变量，增加了错误的概率。使用 `protected` 实例变量，子类可以访问这些变量，但同包内的类则无法访问。

`BasePlusCommissionEmployee3` 类（图 9.10）是 `CommissionEmployee2` 类（第5行）的修改，它继承自 `CommissionEmployee` 并继承了受保护的实例变量 `grossSales` 和 `commissionRate`。结果是，在编译 `earnings` 方法第32行以及 `toString` 方法第40-42行时，编译器不会生成错误。如果另一个类继承 `BasePlusCommissionEmployee3`，新的子类也将继承这些受保护成员。

```
// Fig. 10: BasePlusCommissionEmployee3.java

// BasePlusCommissionEmployee3 继承自 CommissionEmployee

// 并拥有 CommissionEmployee 的 的保护成员。

public class BasePlusCommissionEmployee3 extends CommissionEmployee

{

    private double baseSalary; // 周基础工资

    // 六参数构造函数

    public BasePlusCommissionEmployee3(String first, String last,

        String ssn, double sales, double rate, double salary)

    {

        super(first, last, ssn, sales, rate);

        setBaseSalary(salary); // 验证并存储基础工资

    } // 六参数 BasePlusCommissionEmployee3 构造函数

    // 设置基础工资

    public void setBaseSalary(double salary)

    {

        baseSalary = (salary < 0.0) ? 0.0 : salary;

    } // end method setBaseSalary

    // 返回基础工资

    public double getBaseSalary()

    {

        return baseSalary;

    } // end method getBaseSalary

    // 计算收入

    public double earnings()

    {

        return baseSalary + (commissionRate * grossSales);

    } // end method earnings

    // BasePlusCommissionEmployee3 的字符串表示

    public String toString()

    {

        return String.format("%s: %s\n%s: %s\n%s: %.2f\n%s: %.2f\n%s: %.2f",

            "base commission employee", firstName, "lastName", lastName,

            "social security number", socialSecurityNumber,

            "gross sales", grossSales, "commission rate", commissionRate,

            "base salary", baseSalary);

    } // end method toString

}
```

图 9.10 | 继承了实例变量的 BasePlusCommissionEmployee3。

`BasePlusCommissionEmployee3` 不继承 `CommissionEmployee2` 的构造函数。然而，`BasePlusCommissionEmployee3` 类的六参数构造函数（第10-15行）显式地调用了 `CommissionEmployee2` 的五参数构造函数。`BasePlusCommissionEmployee3` 的六参数构造函数必须显式地调用五

## 9.4 超类与子类之间的关系 443

`CommissionEmployee2` 类的构造函数，因为 `CommissionEmployee2` 没有提供可以被隐式调用的无参数构造函数。

9.11 使用 `BasePlusCommissionEmployee` 对象来执行与图 9.7 对 `BasePlusCommissionEmployee` 对象执行的相同任务（图 9.6）。注意，这两个程序的输出是完全相同的。尽管我们在没有使用继承的情况下声明了 `BasePlusCommissionEmployee` 类，并使用继承声明了 `BasePlusCommissionEmployee3` 类，但这两个类提供了相同的功能。`BasePlusCommissionEmployee3` 类的代码为 45 行，比 `BasePlusCommissionEmployee` 类的 115 行短得多，因为 `BasePlusCommissionEmployee3` 从 `CommissionEmployee2` 继承了大部分功能，而 `BasePlusCommissionEmployee` 类只继承了 `Object` 类的功能。此外，佣金员工的功能只有一份。

```java
// Fig. 9.11: BasePlusCommissionEmployee3.java
// Testing类 BasePlusCommissionEmployee3.

public static void main(String[] args) {
    // 实例化 BasePlusCommissionEmployee3 对象
    BasePlusCommissionEmployee3 employee =
        new BasePlusCommissionEmployee3(
        "Bob", "Lewis", "333-3333", 5000, 0.44, 300);
    // 获取get佣金员工数据
    System.out.println("Employee information obtained by get methods: %n");
    System.out.printf("%s %s", "First name is", employee.getFirstName());
    System.out.printf("%s %s", "Last name is", employee.getLastName());
    System.out.printf("%s %s", "Social securityNumber is", employee.getSocialSecurityNumber());
    System.out.printf("%s %f", "Gross sales is", employee.getGrossSales());
    System.out.printf("%s %f", "Commission rate is", employee.getCommissionRate());
    System.out.printf("%s %f", "Base salary is", employee.getBaseSalary());
    employee.setBaseSalary(1000); // 设置基本工资
    System.out.printf("%n%s%n%s%n",
