
```java
super("Finding Primes with SwingWorker");

setLayout(new BorderLayout());

// 初始化面板从用户处获取数字

JPanel northPanel = new JPanel();

northPanel.add(new JLabel("Find primes less than: "));

highestPrimeJTextField.setColumns(5);

northPanel.add(highestPrimeJTextField);

northPanel.add(getPrimesJButton);

getPrimesJButton.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        progressJProgressBar.setValue(0);
        displayPrimesJTextArea.setText("");
        statusLabel.setText("");
        int number;
        try {
            number = Integer.parseInt(highestPrimeJTextField.getText());
            calculator = new PrimeCalculator(number, displayPrimesJTextArea, statusLabel, getPrimesJButton, cancelJButton);
        } catch (NumberFormatException e) {
            statusLabel.setText("Enter an integer.");
            return;
        }
        getPrimesJButton.setEnabled(false);
        cancelJButton.setEnabled(true);
        calculator.execute();
    }
});

// 添加滚动 JScrollPane 显示计算结果

displayPrimesJTextArea.setEditable(false);
add(new JScrollPane(displayPrimesJTextArea,
    ScrollPaneConstants.VERTICAL_SCROLLBAR_ALWAYS,
    ScrollPaneConstants.HORIZONTAL_SCROLLBAR_NEVER), BorderLayout.CENTER);

// 初始化显示取消按钮、进度条和状态标签的面板

JPanel southPanel = new JPanel(new GridLayout(1, 3, 10, 10));

cancelJButton.setEnabled(false);
cancelJButton.addActionListener(new ActionListener() {
    public void actionPerformed(ActionEvent e) {
        calculator.stopCalculation();
    }
});

southPanel.add(cancelJButton);

progressJProgressBar.setPainted(true);
southPanel.add(progressJProgressBar);
southPanel.add(statusLabel);

add(northPanel, BorderLayout.NORTH);
add(southPanel, BorderLayout.SOUTH);

setSize(350, 300);
setVisible(true);
}

// 监听进度属性变化
calculator.addChangeListener(new PropertyChangeListener() {
    public void propertyChange(ChangeEvent e) {
        if (e.getPropertyName().equals("progress")) {
            int newValue = (Integer) e.getNewValue();
            progressJProgressBar.setValue(newValue);
        }
    }
});

// main 方法开始程序执行
public static void main(String[] args) {
    FindPrimes findPrimes = new FindPrimes();
    findPrimes.setDefaultCloseOperation(Frame.EXIT_ON_CLOSE);
}
```
