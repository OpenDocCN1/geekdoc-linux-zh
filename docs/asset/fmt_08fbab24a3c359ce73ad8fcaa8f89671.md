
```java
hugeIntegerProxy.smaller(firstNumber, secondNumber);

resultsJTextArea.setText(String.format("%s %s %s %s",

firstNumber, result ? "is" : "is not", "less than",

secondNumber ) );

} // end try

} catch (Exception e) {

JOptionPane.showMessageDialog(this, e.toString(),

"Smaller method failed", JOptionPane.ERROR_MESSAGE);

e.printStackTrace();

} // end catch

}

// end method smallerButtonActionPerformed

// 调用 HugeInteger Web 服务的 equals 方法来判断
// 第一个 HugeInteger 是否等于第二个
private void equalsButtonActionPerformed(

java.awt.event.ActionEvent ev) {

String firstNumber = firstJTextField.getText();

String secondNumber = secondJTextField.getText();

if (isValid(firstNumber) && isValid(secondNumber)) {

try {

boolean result =

hugeIntegerProxy.equals(firstNumber, secondNumber);

resultsTextArea.setText(String.format("%s %s %s %s",

firstNumber, (result ? "is" : "is not"), "equal to",

secondNumber));

} // end try
catch (Exception e) {

JOptionPane.showMessageDialog(this, e.toString(),

"Equals method failed", JOptionPane.ERROR_MESSAGE);

e.printStackTrace();

} // end catch

} // end if

} // end method jButtonActionPerformed

}
```

## 28.5 SOAP

每个请求和响应都封装在 SOAP 消息中（也称为 SOAP 封包）——这是一个 XML“封装器”，包含了 Web 服务处理消息所需的信息。SOAP 消息使用 XML 编写，因此具有平台无关性。除少数例外，大多数防火墙（限制网络间通信的安全屏障）都允许 HTTP 流量通过，以便客户端无需防火墙的情况下浏览网站。因此，XML 和 HTTP 使得不同平台的计算机能够进行通信。

Web 服务使用 SOAP 是是因为它支持广泛的类型。用于传输请求和响应的线缆格式必须支持应用程序之间传递的所有类型。SOAP 支持基本类型（例如 `int`）及其包装类型（例如 `Integer`），以及 `Date`、`Time` 等。SOAP 将在第 28.8 节中讨论。有关 SOAP 的更多信息，请访问 `www.w3.org/soap/`。

当请求调用 Web 方法时，请求和所有相关信息会被封装在 SOAP 消息中，并发送到 Web 服务所在的服务器。Web 服务处理 SOAP 消息的内容（包含在 SOAP 封包中），这些内容指定了客户端想要调用的方法以及该方法的参数。这种解释 SOAP 消息内容的过程被称为解析 SOAP 消息。在 Web 服务接收并解析方法后，将使用任何指定的参数调用该方法，并将响应通过另一个 SOAP 消息返回给客户端。客户端代理解析响应（响应包含方法调用的结果），并将结果返回给客户端应用程序。

28.5 显示了 `Integer` Web 服务测试页面，展示了带有值 `99999999999999` 和 `1` 的 `HugeInteger` 的调用结果。Tester 页面还显示了 SOAP 请求和响应消息（之前未显示）。28.12 显示了由 Tester 应用程序显示的相同 SOAP 消息的相同。在图 28.12 的请求消息中，文本

```
<ns1:add>
<first>999999999999999</first>
<second>1</second>
</ns1:add>
```

指定了要调用的方法 (`add`)、方法的参数 (`first` 和 `second`) 以及参数的值 (`99999999999999999` 和 `1`)。同样，图 28.12 响应消息中的文本

```
<ns1:addResponse>
<return>10000000000000000</return>
</ns1:addResponse>
```

指定了方法 `add` 的返回值。

Web 服务的 WSDL 一样，SOAP 消息是自动生成的。因此，在发布和消费 Web 服务时，你不需要理解 SOAP 或 XML 的细节就可以利用它。

**图 28.12** | 如 Java 系统应用程序服务器的 Web 标签所示，`HugeInteger` Web 服务 `add` 方法的 SOAP 消息。

## 2.6 Web 服务中的会话跟踪

第 26.7 节描述了使用会话跟踪来维护客户端状态信息的优势，以便你可以为用户提供个性化的浏览体验。现在我们将会话跟踪整合到 Web 服务中。假设客户端应用程序需要调用同一个 Web 服务的多个方法，每个方法可能被调用多次。在这种情况下，Web 服务为客户端维护状态信息将是有益的，从而避免了多次在客户端和 Web 服务之间传递客户端信息。例如，一个提供本地餐厅评论的 Web 服务可以在初始请求期间存储客户端用户的街道地址，然后在后续请求中使用它来返回个性化的本地化结果。存储会话信息还能让 Web 服务区分客户端。

## 28.6.1 创建黑杰克 Web 服务

我们的下一个示例是一个帮助你开发黑杰克牌游戏的 Web 服务。黑杰克 Web 服务（图 28.13）提供了洗牌、从牌组中发牌以及评估手牌组合的方法。在介绍完 Web 服务后，我们使用它来担任黑杰克游戏的庄家（图 28.14）。黑杰克 Web 服务使用 `HttpSession` 对象为每个客户端应用程序维护一个唯一的牌组。多个客户端可以同时使用该服务，但特定客户端进行的 Web 方法调用仅使用存储在该客户端客户端会话中的牌。我们的示例使用了以下黑杰克规则：

- 给庄家和玩家各发两张牌。玩家的牌正面朝上发放。只有庄家的牌正面朝上。每张牌都有一个值。数字牌 2 到 10 的值等于其面值。J、Q、K 各计 10 分。A 计 0 或 11——以对玩家更有利的值为准（我们很快就会看到）。
- 如果玩家初始两张牌之和为 21（即玩家拿到了 20 点的牌和一张 A，在这种情况下 A 计 11 分），则玩家获得“黑杰克”并立即赢得游戏——除非庄家也有黑杰克（这将会导致“平局”——即如此）。
- 否则，玩家可以开始一次一次地抽取额外的牌。每张牌都正面朝上发放，玩家决定何时停止抽牌。

```java
package com.servlet.blackjack;

import java.util.ArrayList;

import java.util.Random;

import javax.annotation.Resource;

import javax.jws.WebService;

import javax.jws.WebMethod;

import javax.jws.WebParam;

import javax.servlet.http.HttpSession;

import javax.servlet.http.HttpServletRequest;

import javax.xml.ws.WebServiceContext;

import javax.xml.ws.handler.MessageContext;
```
