
**图 10.13** | 实现 `Payable` 的 `Employee` 类。（2 部分之2。）

## 10.7 案例研究：创建和使用接口 497

在图 10.13 中，我们以不同的方式处理了这种情况。记得，当一个类实现接口时，该类与编译器达成契约，声明要么实现接口中的所有方法，要么被声明为抽象类。如果选择后者，我们不需要在抽象类中将方法声明为抽象——它们在接口中已隐式地声明为抽象。抽象类的任何子类都必须实现这些方法以履行与编译器的超级契约。如果子类没有这样做，则必须被声明为抽象。正如第 61–62 行的注释所示，图 10.13 中的类 `Employee` 的每个 `Direct Employee` 子类都继承了超类实现方法 `getPaymentAmount` 的契约——因此必须实现该方法以成为可以实例化对象的具体类。扩展 `Employee` 的子类的类将继承 `getPaymentAmount` 的实现，也将是一个具体类。

## 10.7.5 修改 `SalariedEmployee` 类供 `Payable` 层次结构使用

图 10.14 包含了 `SalariedEmployee` 类的修改版本，它扩展了 `Employee` 并履行了超类 `Employee` 实现 `Payable` 方法 `getPaymentAmount` 的契约。此版本的 `SalariedEmployee` 与图 10.5 相同，例外是[根据提供的源文件，文本已截断]。

## 10.7 案例研究：创建和使用接口 499

![](img/1df0d1e8ac6007b95647eb8ea38390af_544_0.png)

软件工程观察：使用父类引用，我们可以以多态方式调用在父类声明（以及类对象中）中指定的任何方法。使用接口，我们可以以多态方式调用在接口声明（以及类对象中）中指定的任何方法——因为接口类型的变量可以引用一个对象以调用方法，而所有对象都包含类对象的方法。

## 10.7.6 使用接口 `Payable` 处理发票和员工

`PayableInterfaceTest`（图 10.15）阐明了接口 `Payable` 可用于在单个应用程序中以多态方式处理一组发票（Invoices）和员工（Employees）。第 9 行声明了 `payableObjects` 并为其分配了一个包含四个 `Payable` 变量的数组。第 12–13 行将 `Invoice` 对象的引用赋值给 `payableObjects` 的前两个元素。第 14–17 行随后将 `SalariedEmployee` 对象的引用赋值给 `payableObjects` 的剩余元素。这些赋值是允许的，因为 `Invoice` 是 `SalariedEmployee`，`SalariedEmployee` 是 `Employee`，而 `Employee` 是 `Payable`。第 23–29 行显示了用于多态态处理每个 `Payable` 对象的增强语句，将对象打印为字符串以及付款金额日期。注意 27 调用了未在接口 `Payable` 中声明的 `toString`——所有引用（包括接口类型的引用）都指向扩展 `Object` 的对象，因此具有 `toString` 方法。（注意在这里也可以隐式地调用 `toString`）。第 28 行调用 `Payable` 方法 `getAmount` 以获取 `payableObjects` 中每个对象的付款金额，无论对象的实际类型如何。输出显示第 27–28 行中的方法调用了方法 `toString` 和 `getAmount` 的相应类实现。例如，当 `currentEmployee` 在循环第一次迭代中返回 `Invoice` 对象时，将执行 `Invoice` 类的 `toString` 和 `getPaymentAmount`。

```java
// Fig. 10.15: PayableInterfaceTest.java
// 测试接口 Payable。
public class PayableTest {
    public static void main(String args[]) {
        // 创建包含四个元素的数组
        Payable payableObjects[] = new Payable[4];
        // 用实现 Payable 的对象填充数组
        payableObjects[0] = new Invoice("01234", "seat", 2, 375.00);
        payableObjects[1] = new Invoice("06789", "tire", 79.95);
        payableObjects[2] = new SalariedEmployee("John", "Smith", 111-1111, 800.00);
        payableObjects[3] = new SalariedEmployee("Lisa", "Barnes", 888-8888, 1200.00);
    }
}
```

图 10.15 | 以多态方式处理发票和员工的接口测试程序。（2 部分中的第 1 部分）。

## 第 10 章 面对象编程：多态

```java
System.out.println(
"Invoices and Employees processed polymorphically:\n" );
// 通用地处理数组 payableObjects 中的每个元素
for ( Payable currentPayable : payableObjects ) {
    // 输出 currentPayable 及其相应的付款金额
    System.out.printf("%s\n: $%,.2f\n\n",
    currentPayable.toString(),
    "payment due", currentPayable.getPaymentAmount());
} // end for
} // end main
}// end class PayableInterfaceTest
```

以多态方式处理的发票和员工：
invoice:
part number: 01234 (seat)
quantity: 2
price per item: $375.00
payment due: $750.00

invoice:
part number: 56789 (tire)
quantity: 4
price per item: $79.95
payment due: $319.80

salaried employee: John Smith
social security number: 111-11-1111
weekly salary: $800.00
payment due: $800.00

salaried employee: Lisa Barnes
social security number: 888-88-8888
weekly salary: $1,200.00
payment due: $1,200.00

> **图 10.15** 以多态方式处理发票和员工的接口测试程序。（2 部分中的第 2 部分）

![](img/1df0d1e8ac6007b95647eb8ea38390af_545_0.png)

使用接口类型的引用可以调用 `Object` 类的所有方法。引用指向一个对象，而所有对象都继承 `Object` 类的方法。

## 10.7.7 使用接口声明常量

正如我们在 10.7 节中提到的，接口可以声明常量。这些常量隐式地是 `public`、`static` 和 `final`——再次，在接口声明中不需要这些关键字。接口的一个流行用途声明一组可以在许多类声明中使用的常量。考虑接口 `Constants`：

## 10.7 案例研究：创建和使用接口

```java
public interface Constants {
    int ONE = 1;
    int TWO = 2;
    int THREE = 3;
}
```
