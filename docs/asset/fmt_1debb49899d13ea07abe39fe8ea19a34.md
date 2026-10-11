
# Fig. 11.2: Addition.java

```java
// Fig. 11.2: Addition.java

// 使用 JOptionPane 进行输入输出的加法程序。

import javax.swing.JOptionPane; // program uses JOptionPane

public class Addition {

    public static void main(String[] args) {

        // 从 JOptionPane 输入对话框获取用户输入

        String firstNumber = JOptionPane.showInputDialog("Enter first integer");

        String secondNumber = JOptionPane.showInputDialog("Enter second integer");

        // 将 Strings 转换为 int 值用于计算

        int number1 = Integer.parseInt(firstNumber);

        int number2 = Integer.parseInt(secondNumber);

        int sum = number1 + number2;

        // 在 JOptionPane 对话框中显示结果

        JOptionPane.showMessageDialog(null,"Sum is " + sum + " of Two Integers",JOptionPane.PLAIN_MESSAGE);

    } // end main

} // end class
```
