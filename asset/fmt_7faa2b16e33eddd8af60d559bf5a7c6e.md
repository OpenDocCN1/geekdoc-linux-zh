
```java
else if ( dealersTotal == 21 ) // blackjackProxy has blackjack
    gameOver(GameStatus.LDOE);
} else if ( playerTotal == 21 ) // blackjack
    gameOver(GameStatus.BLACKJACK);
    // next card for blackjackProxy has index 2
    currentDealerCard = 2;
    // next card for player has index 13
    currentPlayerCard = 13;
} // end method dealJButtonActionPerformed
// begins application execution
public static void main(String args[]) {
    java.awt.EventQueue.invokeLater(
        new Runnable() {
            public void run() {
                new BlackjackGameFrame().setVisible(true);
            }
        }); // end call to aawt.EventQueue.invokeLater
    } // end method
// Variables declaration - do not modify
private javax.swing.JButton JButton;
private javax.swing.JLabel dealerCard10Label;
private javax.swing.JLabel dealerCard11Label;
private javax.swing.JLabel dealerCard12Label;
private javax.swing.JLabel dealerCard13Label;
private javax.swing.JLabel dealerCard14Label;
private javax.swing.JLabel dealerCard45Label;
private javax.swing.JLabel dealerCard46Label;
private javax.swing.JLabel dealerCard47Label;
private javax.swing.JLabel dealerCard48Label;
private javax.swing.JLabel dealerCard49Label;
private javax.swing.JLabel dealerCard50Label;
private javax.swing.JLabel dealerJLabel;
private javax.swing.JLabel dealerTotal1Label;
private javax.swing.JButton hitButton;
private javax.swing.JLabel playerCard10Label;
private javax.swing.JLabel playerCard11Label;
private javax.swing.JLabel playerCard1JLabel;
private javax.swing.JLabel playerCard2JLabel;
private javax.swing.JLabel playerCard2JLabel;
private javax.swing.JLabel playerCard3JLabel;
private javax.swing.JLabel playerCard4JLabel;
private javax.swing.JLabel playerCard5JLabel;
private javax.swing.JLabel playerCard6JLabel;
private javax.swing.JLabel playerCard7JLabel;
private javax.swing.JLabel playerCard8JLabel;
private javax.swing.JLabel playerCard9JLabel;
```

图. 28.14 使用 Blackjack 服务的 Blackjack 游戏。（10 部分第 7 部分。）

## 28.6 Web 服务中的会话跟踪

```java
private javax.swing.JLabel playerJLabel;
private javax.swing.JLabel playerTotalJJLabel;
private javax.swing.JButton standJButton;
private javax.swing.JLabel statusJLabel;
// End of variables declaration
// end class BlackGameJFrame
}
```

a) 用户点击 Deal 按钮后，庄家和玩家的手牌。

![](img/1df0d1e8ac6007b95647eb8ea38390af_1436_0.png)

b) 用户点击两次 Hit（要牌）然后点击 Stand（停止）后，庄家和玩家的手牌。在这种情况下，玩家赢了。

![](img/1df0d1e8ac6007b95647eb8ea38390af_1436_1.png)

图. 28.14 | 使用 Blackjack 服务的 Blackjack 游戏。（10 部分第 8 部分）。

c) 用户根据初始手牌点击 **Stand**（停止）后，庄家和玩家的手牌。在这种情况下，玩家输了。

![](img/1df0d1e8ac6007b95647eb8ea38390af_1437_0.png)

d) 用户获得点黑数（Blackjack）后，庄家和玩家的手牌。

![](img/1df0d1e8ac6007b95647eb8ea38390af_1437_1.png)

**图. 28.14** | 使用 Blackjack 服务的 Blackjack 游戏。（10 部分第 9 部分）。

### 28.6 Web 服务中的会话跟踪 1393

d) 庄家获得点黑数（Blackjack）后，庄家和玩家的手牌。

![](img/1df0d1e8ac6007b95647eb8ea38390af_1438_0.png)

**图. 28.14** | 使用 Blackjack 服务的 Blackjack 游戏。（10 部分第 10 部分）。

- 用户点击 Deal 按钮后，庄家和玩家的手牌。
- 用户点击两次 Hit 然后点击 Stand 后，庄家和玩家的手牌。在这种情况下，玩家赢了。
- 用户根据初始手牌点击 **Stand** 后，庄家和玩家的手牌。在这种情况下，玩家输了。
- 用户获得点黑数后，庄家和玩家的手牌。
- 庄家获得点黑数后，庄家和玩家的手牌。

# 第 28 章 JAX-WS Web 服务。Web 2.0 与 Mash-Ups 1394

方法 `displayCard`（第 134–184 行）更新 GUI 以显示新发出的牌。该方法接收的参数是：一个必须设置的 `JLabel` 整数索引，以及一个代表牌的字符串。空字符串表示我们想要显示牌面。如果方法 `methodCard` 接收到的非空字符串，程序将从字符串中提取牌面并使用此信息正确显示。`switch` 语句（第 159–173 行）将数字转换为花色，并将相应的字符分配给 `suitletter`（h 代表红桃，d 代表菱，c 代表梅花，s 代表黑桃）。`suitletter` 中的字符用于完成文件名。

在这个示例中，你学习了如何设置 Web 服务来支持会话处理。你还学习了如何跟踪每个客户端的会话状态。从桌面应用程序到会话跟踪的一部分。现在你将学习如何从 Web 服务访问数据库，以及如何从客户端应用程序消费 Web 服务。

## 2.7 从 Web 应用消费数据库驱动的 Web 服务

我们之前的示例是从 Netbeans 创建的桌面应用程序访问 Web 服务。然而，我们可以轻松地在 Web 应用中使用它们。事实上，基于 Web 的服务变得越来越流行，应用程序消费 Web 服务已很常见。在这一节中，我们展示了一个航空公司预订服务，它可以接收客户希望预订的座位类型信息，如果有可用座位则进行预订。在节的后面，我们将展示一个 Web 应用程序，允许客户指定预订请求，然后使用航空公司预订服务尝试执行该请求。我们使用 Sun Java Studio Creator 2 来创建 Web 应用程序。

### 2.7.1 在 Netbeans 中配置 Java DB 并创建 Reservation 数据库

在示例中，我们的 Web 服务使用包含名为 `Seats` 的单表的 Reservation 数据库来查找匹配请求的座位。你将使用 Netbeans 提供的工具创建和操作 Java DB 数据库。
