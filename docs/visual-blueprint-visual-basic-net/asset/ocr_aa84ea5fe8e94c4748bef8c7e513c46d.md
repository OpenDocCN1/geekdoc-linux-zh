# PROVIDE ACCESS TO DISABLED USERS

Accessibility aids make it easier for the disabled to use computers. For example, blind people can use screen readers to verbalize the information shown on screen, and people who cannot use a keyboard and mouse can rely on voice input utilities. You can use properties provided in Windows Forms controls to aid disabled users with your application.

To enable users with disabilities to use your application effectively, you need to consider some guidelines that target problem areas an individual may encounter. Always provide a flexible user interface that accommodates the user's needs and preferences. Use color to enhance and emphasize information shown by other means. Do not use color as the only means of using a part of your application. Keyboard access to all parts of your application enables all users, especially disabled users, to use your application more effectively. The size of text and graphics affects both accessibility and usability. You should enable users to size objects on the screen and follow system metrics for preset user preferences.

All Windows Forms controls inherit an AccessibleObject that stores information to use with software- and hardware-based accessibility aids. The AccessibleDescription property of the object appears in the Properties window and specifies a description for the control. For example, an Exit button may contain the description "A button with the text Exit." The AccessibleName property reports a name for the control to accessibility aids. The AccessibleRole property reports the role of the control. In most cases, the designer sets this property correctly. For example, the AccessibilityRole of a Button control is AccessibilityRole.Button. In some cases, you may want to change this property. For example, if you use a PictureBox control to draw a chart, you can set the role to AccessibilityRole.Chart.

# PROVIDE ACCESS TO DISABLED USERS

![](bbox=[0.04, 0.6, 0.96, 0.85])

+   1. Open an existing project.
+   2. Click a control on a Windows Form.
+   3. Click the AccessibleDescription property in the Properties window and type a description for the particular control.
+   4. Click AccessibleName and type in a name for the control.