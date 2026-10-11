![](bbox=[0.22, 0.106, 0.79, 0.353])

*Figure 283: Procomn filter by Path*

Applying this additional filter produces the following results:

![](bbox=[0.13, 0.418, 0.87, 0.59])

*Figure 284: fodhelper.exe looking for command value*

According to this output, we see something rather interesting. The **fodhelper.exe** application attempts to query the **HKCU\\Software\\Classes\\ms-settings\\shell\\open\\command** registry key, which does not appear to exist.

In order to better understand why this is happening and what exactly this registry key is used for, we’ll modify our check under the Path and look specifically for any access to entries that contain **ms-settings\\shell\\open\\command**. If the process can successfully access that key in some other hive, the results will provide us with more clues.