
@WebService(name = "Blackjack", serviceName = "BlackjackService")

public class Blackjack {

    // 使用 @Resource 创建用于会话跟踪的 WebServiceContext

    private @Resource WebServiceContext webServiceContext;

    private MessageContext messageContext; // 用于会话跟踪

    private HttpSession session; // 存储会话的属性

    // 发一张牌

    @WebMethod(operationName = "dealCard")

    public String dealCard() {

        String card = "";

        List<String> deck = (ArrayList<String>) session.getAttribute("deck");

        card = deck.get(0); // 获取牌组顶部的牌

        deck.remove(0); // 牌组顶部的牌

        return card;

    } // end WebMethod dealCard

    // 洗牌

    @WebMethod(operationName = "shuffle")

    public void shuffle() {

        // 获取 HttpSession 对象以存储当前客户端的牌组

        messageContext = webServiceContext.getContext();

        session = ((HttpServletRequest) messageContext.get(

                MessageContext.SERVLET_REQUEST)).getSession();

        // 填充牌组

        List<String> deck = new ArrayList<String>();

        for (int face = 1; face < 13; face++) // 循环花色
            for (int suit = 0; suit < 4; suit++) // 循环花色
                deck.add(face + " " + suit); // 将每张牌添加到牌组

    }

    String tempCard; // 交换期间临时持有牌

}

**图 28.13** | 发牌和评估手牌的黑2克 Web 服务。（4 部分中的第 1 部分。）

## 28.6 Web 服务中的会话跟踪

```java

Random randomObject = new Random(); // 生成随机数

int index; // 随机选择的牌索引

```

```java

for (int i = 0; i < deck.size(); i++) // 洗牌
{

    index = randomObject.nextInt(deck.size()) - 1;
    // 将位置 i 的牌与随机选择的牌进行交换
    tempCard = deck.get(i);
    deck.set(i, deck.get(index));
    deck.set(index, tempCard);

} // for 循环结束

```

```java

// 将此添加到用户的会话中
session.setAttribute("deck", deck);

} // shuffle 方法结束

```

```java

// 确定手牌值
@WebServlet(operationName = "getHandValue")

public int getHandValue(String hand = "hand")

```

```java

// 将手牌拆分为牌
String[] cards = hand.split("\t");
int total = 0; // 手牌中牌的总值
int face; // 当前牌的面值
int aceCount = 0; // 手牌中 A 的数量

```

```java

for (int i = 0; i < cards.length; i++)
{

    // 解析字符串并获取 String 中的第一个整数
    face = Integer.parseInt(
        cards[i].substring(0, cards[i].indexOf(" ")));
    switch (face) {
        case 1: // 如果是 A，增加 aceCount 计数
            ++aceCount;
            break;
        case 11: // J
        case 12: // Q
        case 13: // K
            total += 10;
            break;
        default: // 否则，加上面值
            total += face;
            break;
    } // switch 结束

```

图 28.13 用于发牌和评估手牌的 Blackjack Web 服务。（4 部分中的第 3 部分）。

## 第 28 章 JAX-WS Web 服务。Web 2.0 与混合应用（Mash-Ups）

```java

// 如果可能，将一个 A 视为 11
if ( total + 11 + aceCount - 1 <= 21 )
    total += 11 + aceCount;
else // 否则，将所有 A 视为 1
    total += aceCount;

} // if 结束
return total;

} // getValue WebMethod 结束
} // Blackjack 类结束
```
