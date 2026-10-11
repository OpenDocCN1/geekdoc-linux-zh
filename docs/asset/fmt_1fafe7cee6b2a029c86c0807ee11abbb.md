
```java
.addGap(18, 18, 18)
.addGroup(
    layout.createParallelGroup(
        javax.swing.GroupLayout.Alignment.LEADING)
        .addComponent(greenTextField)
        .addComponent(redTextField)
    )
.addGap(18, 18, 18)
.addGroup(
    layout.createParallelGroup(
        javax.swing.GroupLayout.Alignment.LEADING)
        .addComponent(blueLabel)
    )
.addGap(18, 18, 18)
.addGroup(
    layout.createParallelGroup(
        javax.swing.GroupLayout.Alignment.LEADING)
        .addComponent(blueSlider)
    )
.addGap(18, 18, 18)
.addGroup(
    layout.createParallelGroup(
        javax.swing.GroupLayout.Alignment.LEADING)
        .addComponent(blueTextField)
    )
.addGap(18, 18, 18)
.addComponent(colorPanel)
.addGap(0, 100, javax.swing.GroupLayout.MAX_VALUE)
);
layout.setVerticalGroup(
    layout.createParallelGroup(
        javax.swing.GroupLayout.Alignment.LEADING)
        .addGroup(layout.createSequentialGroup()
            .addGroup(
                layout.createParallelGroup(
                    javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(greenLabel)
                    .addComponent(redLabel)
                )
            .addGap(18, 18, 18)
            .addGroup(
                layout.createParallelGroup(
                    javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(greenSlider)
                    .addComponent(redSlider)
                )
            .addGap(18, 18, 18)
            .addGroup(
                layout.createParallelGroup(
                    javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(greenTextField)
                    .addComponent(redTextField)
                )
            .addGap(18, 18, 18)
            .addGroup(
                layout.createParallelGroup(
                    javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(blueLabel)
                )
            .addGap(18, 18, 18)
            .addGroup(
                layout.createParallelGroup(
                    javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(blueSlider)
                )
            .addGap(18, 18, 18)
            .addGroup(
                layout.createParallelGroup(
                    javax.swing.GroupLayout.Alignment.LEADING)
                    .addComponent(blueTextField)
                )
            .addGap(18, 18, 18)
            .addComponent(colorPanel)
            .addGap(0, 100, javax.swing.GroupLayout.MAX_VALUE))
);
layout.layout(colorJPanel, colorJPanelLayout);
layout.layout(getContentPane(), layout);
pack();
}
public void changeColor() {
    colorPanel.setBackground(new java.awt.Color(
        redSlider.getValue(),
        greenSlider.getValue(),
        blueSlider.getValue()));
}
private void redSliderChanged(javax.swing.event.ChangeEvent evt) {
    changeColor();
}
```
