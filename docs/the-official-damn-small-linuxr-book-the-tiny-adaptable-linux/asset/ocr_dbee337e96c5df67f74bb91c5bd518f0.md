# Other Wireless Card Using Ndiswrapper

If you find that your wireless card is not natively supported by drivers contained in DSL, the catch-all wireless solution is Ndiswrapper. Ndiswrapper uses the same drivers that Microsoft Windows uses. The drivers may be obtained from the software CD that was included when you bought your wireless card. The drivers may also be obtained from the vendor's support website.

A very good source for selecting which Windows driver to use is the Ndiswrapper website itself:

```
http://ndiswrapper.sourceforge.net/mediawiki/index.php/List
```

To open the ndiswrapper setup window, select the Ndiswrapper button from the DSL Control Panel. The ndiswrapper setup window appears as shown in Figure 4-20.

![](bbox=[0.15, 0.57, 0.42, 0.72])

Using Ndiswrapper usually means having two files: an .inf file together with a .sys file. Often, when DSL is used on a machine that also runs Windows, you can simply mount the drive that contains Windows and specify the full windows path to the .inf file. Note that you use the forward slash and not the backward slash, as shown in Figure 4-20.

+   - The sid field is the name of the wireless access point. This can be left blank to use the closest or strongest signal. Otherwise, enter the name of the access point.
+   - The wep field is the encryption key. If none is used, leave it blank. Otherwise, you must enter the key as colon separated pairs—for example, 12:34:56:78:FF. This key should be a hexadecimal representation of the encryption key entered when the wireless router was configured.

Press the OK button when you are ready to attempt a connection. A small pop-up displays the results of your connection attempt.