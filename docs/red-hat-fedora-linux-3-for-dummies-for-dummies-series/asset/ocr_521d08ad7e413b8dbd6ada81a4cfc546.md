8. Fill out the registration form as appropriate and click the **Register** button at the bottom right of the page.

The Sun shopping cart page opens.

9. Click the **Check Out** button.

The License Agreement page opens.

10. Click the **Accept** radio button and the **Continue** button.

11. Click the **Place Order** button when the **Verify Order** page opens.

A JavaScript dialog opens prompting you for a final confirmation.

12. Click the **OK** button.

The Download page for the Java(TM) 2 Runtime Environment opens.

13. Click the **Linux RPM** in **self-extracting file** link.

The dialog box labeled *Opening j2re-1_5_0-linux-i586-rpm.bin* opens.

14. Click the **OK** button.

The dialog box labeled *Enter name of file to save to... * opens.

15. Click the **Save** button.

The Download Manager dialog box opens, showing the progress of the file download. You must now extract and link the Java library to Mozilla to make use of them.

1. Open a **GNOME Terminal** window by clicking the **GNOME Menu** and selecting **System Tools->Terminal**.

We assume you're still logged in as Root.

2. In the **GNOME Terminal**, enter these commands:

```
chmod +x j2re*
./j2re*
```

3. Press the spacebar while you simultaneously read, digest and (pre-sumably) agree with the license agreement.

Once again you should probably have your legal team by your side.

4. Type in yes when you finish reading the agreement.

5. Enter the following command in the **GNOME Terminal**:

```
rpm -ivh j2re*rpm
```

6. Create a link to the Java plug-in by entering the following (single) command:

```
ln -s
/usr/java/j2re1.5.0/plugin/i386/
ns7/libjavaplugin_oji.so
/usr/lib/mozilla/plugins/
libjavaplugin_oji.so
```