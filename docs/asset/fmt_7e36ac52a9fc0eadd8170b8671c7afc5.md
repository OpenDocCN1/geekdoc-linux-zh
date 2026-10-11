
```java
// 图 28.20: Equation.java
// 包含等式信息的 Equation 类
package com.deitel.jht7.generator;
public class Equation {
    private int leftOperand;
    private int rightOperand;
```

**图 28.20** | 存储等式信息的 Equation 类。（3 部分中的第 1 部分。）

## 28.8 将自定义类型对象传递给 Web 服务

```java
private int resultValue;
private String operationType;

// 要求的无参数构造函数
public Equation()
{
    this(0
```

**图 28.20** | 存储等式信息的 Equation 类。（3 部分中的第 2 部分。）

```java
return rightOperand;
}// getRightOperand 方法结束

// 获取 returnValue
public int getReturnValue()
{
    return returnValue;
}// getReturnValue 方法结束
}
// 获取 operationType
public String getOperationType()
{
    return operationType;
}// getOperationType 方法结束
}
// 要求的 setter
public void setLeftHandSide(String value)
{
    // 空方法体
}// setLeftHandSide 方法结束
}
// 要求的 setter
public void setRightHandSide(String value)
{
    // 空方法体
}// setRightHandSide 方法结束
}
// 要求的 setter
public void setLeftOperand(int value)
{
    // 空方法体
}// setLeftOperand 方法结束
}
// 要求的 setter
public void setRightOperand(int value)
{
    // 空方法体
}// setRightOperand 方法结束
}
// 要求的 setter
public void setReturnValue(int value)
{
    // 空方法体
}// setResultOperand 方法结束
}
// 要求的 setter
public void setOperationType(String value)
{
    // 空方法体
}// setOperationType 方法结束
} // class Equation
```

**图 28.20** | 存储等式信息的 Equation 类。（3 部分中的第 3 部分。）

类 `Equation` 定义了方法 `getLeftHandSide` 和 `setLeftHandSide`（第 41–44 和 77–80 行）；`getRightHandSide` 和 `setRightHandSide`（第 47–50 和 83–86 行）；`getLeftOperand` 和 `setOperand`（第 53–56 和 89–92 行）；`getRightOperand` 和 `setOperand`（第 59–62 和 95–98 行）；`getReturnValue` 和 `setValue`（第 65–68 和 101–104 行）；`getOperationType` 和 `setObjectType`（第 71–74 和 107–110 行）。Web 服务的客户端不需要修改实例变量的值。但请记住，只有当属性是公共的或具有 set 和 get 方法时，它才能被序列化。

```java
// 图 28.20: Equation.java
// 包含等式信息的 Equation 类
package com.deitel.jht7.generator;
public class Equation {
    private int leftOperand;
    private int rightOperand;
```

### 创建 EquationGenerator Web 服务

图 28.21 中的 `EquationGenerator` 类是一个返回 `Equation` 对象的 Web 服务。

```java
// 图 28.21: EquationGenerator.java
// 生成等式的 Web 服务
package com.deitel.jht7.generator;
import java.util.Random;
import javax.jws.WebService;
import javax.jws.WebMethod;
import javax.jws.WebParam;

@WebService(name = "EquationGenerator", serviceName = "EquationGeneratorService")
public class EquationGenerator {
    private int minimum;
    private int maximum;

    // 要求的无参数构造函数
    public EquationGenerator() {
        minimum = (int) Math.pow(10, 0);
        maximum = (int) Math.pow(10, 3);
    }

    // 生成数学等式并返回
    @WebMethod(operationName = "generateEquation")
    public Equation generateEquation(@WebParam(name = "operation") String operation,
                                      @WebParam(name = "difficulty") int difficulty) {
        Random randomObject = new Random();
        return new Equation(randomObject.nextInt(maximum - minimum) + minimum, operation);
    }
}
```

## 28.8 将自定义类型的对象传递给 Web 服务

生成方程（Equation）的结果。

![](img/1df0d1e8ac6007b95647eb8ea38390af_1454_0.png)

**图 28.22** | 测试一个返回 XML 序列化 Equation 对象的 Web 方法。（第 2 部分，共 2 部分。）

`minimum` 的值是通过将 10 的方为小于 level 的幂（第 23 行）确定的。这计算了具有 level 长度数字的最小数。如果 level 为 1，`minimum` 为 1；如果 level 为 2，`minimum` 为 10；如果 level 为 3，`minimum` 为 100。对于 `maximum` 的值（用于形成方程的任何随机生成数的上界），程序将 10 的方提升为指定 level 参数的幂（第 23 行）。如果 level 为 1，`maximum` 为 100；如果 level 为 2，`maximum` 为 100；如果 level 为 3，`maximum` 为 1000。

第 28–30 行创建并返回一个新的 `Equation` 对象，该对象由随机数和 `generateEquation` 接收到的字符串操作组成。程序调用了 `Random.nextInt` 方法，它返回一个小于指定上界的 int 类型。该方法生成一个大于或等于 `minimum` 但小于 `maximum` 的左操作数值（即一个 1 位的数字）。右操作数是另一个具有此类特征的随机数。

### 消费 EquationGenerator Web 服务

Math Tutor 应用程序（图 28.23）使用了 `EquationGenerator` Web 服务。该应用程序调用 Web 服务 `generateEquation` 方法来创建一个 `Equation` 对象。辅助器显示方程的左侧并等待用户输入。第 9 行还声明了一个 `Generator` 实例变量，我们用它来获取 `EquationGenerator` 代理对象。第 10–11 行声明了 `EquationGenerator` 和 `Equation` 类型的实例变量。
