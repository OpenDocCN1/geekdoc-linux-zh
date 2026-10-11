
`ObjectOutputStream` `outputStream`;

`outputStream.writeInt(account)`;

`outputStream.writeChars(company)`;

`outputStream.writeDouble(amount)`;

- b) 下述语句应从"`payables.txt`"文件读取记录。应该使用变量`payable`来引用此文件。

```java
Scanner inPayable = new Scanner( new File("payables.txt") );
PayablesRecord record = ( PayablesRecord )inPayable.readObject();
```
