```
size: <minsize>,<maxsize>
expires: <mintime>,<maxtime>
options: <options>
}
```

The method name is either cnfs or timehash indicating the storage method to which the class is applied. A special method called trash can also be used to define a storage class for which all messages are thrown away.

Inside each class are five parameters:

+   - **newsgroups:** A wildcard expression indicating which newsgroups are accepted by the storage class.
+   - **class:** A unique number identifying the storage class. The number should be between 0 and 255 and should be unique among all the storage classes in `storage.conf`.
+   - **size:** The minimum size in bytes of articles accepted by the class and, optionally, the maximum size of articles accepted by the class. A maximum size of zero indicates that there is no upper limit on article size and a minimum size of zero indicates that there is no lower limit on article size.
+   - **expires:** The minimum expire time for articles accepted by the class and, optionally, the maximum time for articles accepted by the class. A maximum time or zero indicates that there is no maximum on the expire time for articles accepted in the class.
+   - **options:** The name of the metacycbuff used to store articles accepted by this storage class. This parameter is only used for CNFS storage classes.

The following is a sample `storage.conf` file:

```
method cnfs {
    newsgroups: alt.binaries.*
    class: 0
    size: 0,1000000
    expires: 0,4d
    options: SMALAREA
}
method cnfs {
    newsgroups: *
    class: 2
    size: 0,0
    expires: 0,0
    options: BIGAREA
}
```

The first storage class indicates that articles destined for groups whose names start with `alt.binaries` are between 0 and 1MB in size and expire within 4 days should be stored in the SMALAREA metacycbuff. The second storage class accepts any articles that are rejected by the first storage class and stores them in the BIGAREA metacycbuff.

If your system uses timehash storage, you might use the following `storage.conf` file to achieve a similar result: