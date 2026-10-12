```
make
mv rsaref.a librsaref.a
```

After you create the librsaref.a library file, you can compile SSLey.

# ### Building SSLey

Follow the steps below:

+   1. Change directories to `/usr/local/src/SSLey-0.9.0b` and run the following command:
+       make -f Makefile.ssl links

+   2. If you are in the United States, you need to tell SSLey about the rsaref library package, so run the following commands:
+       ```
+       perl ./Configure gcc -DNO_DEA -DRSAref -lRSAglue \
+       -L'/pwd/.../rsaref-2.0/local/' -lrsaref
+       cp rsaref/rsaref.h include/
+       ```
+   
+       Everyone else should run the following command, which does not specify the RSAref library package:
+       ```
+       perl ./Configure gcc -DNO_DEA
+       ```

+   3. Compile and test the package by running the following commands:
+       make
+       make test

# ### Building mod_ssl and Apache

Change directories to `/usr/local/src/mod_ssl-2.0.13-1.3.9` and run the configure script as follows:

```
./configure \
--with-apache=../apache_1.3.9 \
--with-ssleay=../ SSLey-0.9.0b \
--with-rsaref=../rsaref-2.0/local \
--prefix=/usr/local/apache
```

You do not need the `--with-rsaref` option if you are not in the United States. Also, make sure you use the appropriate `--prefix` value for your desired Apache destination.