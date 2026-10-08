
# Python for system administrators

## Work with Python

```ini
zend.zel_compatibility_mode = Off
short_open_tag = On
asp_tags = Off
precision = 14
y2k_compliance = On
output_buffering = 4096
;output_handler = =
zlib.output_compression = Off
```

```python
host(),'localhost'
config.set('MySQL','mysql.default_port','3306')
config.set('MySQL','mysql.allow_persistent','On')
config.set('MySQL','mysql.max_persistent','20')
```

```ini
[MySQL]
; Allow or prevent persistent links.
mysql.allow_persistent = On
mysql.max_persistent = 20
mysql.max_links = -1
mysql.default_port = 3306
mysql.default_socket = =
mysql.default_host = localhost
mysql.connect_timeout = 60
mysql.trace_mode = Off
```

```python
with open('php.ini', 'ap') as config:
    config.write(config)
Output:php.ini
[MySQL]
mysql.max_persistent = 20
mysql.allow_persistent = On
mysql.default_port = 3306
mysql.default_host = localhost
mysql.trace_mode = Off
mysql.connect_timeout = 60
```

Python provides a built-in module called ConfigParser (known as configparser in Python 3.0). You can use this module to parse and create configuration files.

> @code:writeconfig.py
> @description: The following demonstrates MySQL section to the php.ini file.
> @warning:Do not use this script with the actual php.ini file, as it's not designed to handle all aspects of a complete phpini.

```python
@code:parseconfig.py
@description: Parsing and updating the config file
import ConfigParser
config = ConfigParser.ConfigParser()
# Print config values
print config.get('MySQL','mysql.default_host')
print config.get('MySQL','mysql.default_port')
config.remove_option('MySQL','mysql.trace_mode')
with open('php.ini', 'wb') as config:
    config.write(config)
```

# Parsing JSON data

JSON (also known as JavaScript Object Notation) is a lightweight modern data-exchange format. JSON is an open standard under ECMA-262. It is a text format

![](img/c72194f2c3aec198936695a665a5167c_64_0.png)

and is completely language-independent. JSON is also used as the configuration format for modern applications such as Mozilla Firefox and Google Chrome. JSON is also very popular with modern web services such as Facebook, Twitter, Amazon EC2 etc. In this section we will use the Python module simplejson to access Yahoo Search (using the Yahoo Web Services API), which outputs JSON data.

For this section we will use the simplejson.Load function, which allows us to deserialise a JSON object into a Python object.

To use this section, you should have the following:

- 1. Python module: simplejson.

```python
@code: YahooSearch.py
import simplejson, urllib
APP_ID = 'xxxxxxx' # Change to this
y your APP ID
SEARCH_BASE = 'search.yahooapis.com/WebSearchService/1/webSearch
```

Note: You can install Python modules using the command `easy_install <module_name>`. This assumes that you have a working internet connection.

```python
class YahooSearchError(Exception):
    pass
```

- 2. Yahoo App ID:
The Yahoo App ID can be created from https://developers.yahoo.com/dashboard/createKey.html. The Yahoo App ID will be generated on the next page. See the screenshot for details. simplejson is very easy to use. In the following example we will use the capability of mapping JSON data structures to Python data types. This gives us direct access to the JSON data without developing any XML parsing code.

```python
def search(query,results=20, start=1, **kwargs):
    kwargs.update({
        'appid': APP_ID,
        'query': query,
        'results': results,
        'start': start,
        'output': 'json'
    })
    url = SEARCH_BASE + '?' + urllib.parse.urlencode(kwargs)
    result = simplejson.load(urllib.request.urlopen(url))
    if 'Error' in result:
        # An error occurred; raise an exception
        raise YahooSearchError(result['Error'])
    return result['ResultSet']
```

# JSON DATA MAPPING

| JSON | Python |
| --- | --- |
| object | dict |
| array | list |
| string | unicode |
| number (int) | int, long |
| number (real) | float |
| TRUE | TRUE |
| FALSE | FALSE |
| null | None |

Use the code listed above from the Python shell to see how it works. Change to the directory where you have saved the LUDYSearch.py and open a Python shell.

@code: Python Shell Output.

![](img/c72194f2c3aec198936695a665a5167c_65_0.png)

So, you want to use some Yahoo! APIs...
We need some information from you to use Yahoo Web Services, we need some information about the application you're building. We use this information to get a better understanding of how Yahoo Services are being used and to protect the security and privacy of Yahoo users. All questions are required.

| SUBMIT THIS FORM | GET YOUR ADDRESS | WRITE YOUR CODES |
| --- | --- | --- |

About your application

| Application Name: | LudySearch |
| --- | --- |
| Kind of Application: | Client/Desktop |
| Description: | An App to demonstrate the JSON parsing using Python 260 characters or less |

Favicon URL: http://www.yahoo.com/this/App/Favicon.gif
Optional: specify a URL to a 16x16 JPG, PNG or GIF image.

# Security & Privacy

Yahoo APIs use the OAuth protocol for secure validation of API usage and end-user authentication, if needed.
Access Scopes: This app will only access public APIs, Web Services, or RSS feeds. This app requires access to private data.

# Contact information

Just in case comes up and we need to get help:
Application Name: LudySearch
Email: 
Terms of Use: agree

An important job for a system administrator is to gather information. The next example shows how to do this. The following code shows the memory and the file system information.

```python
@code: PySysInfo.py
import os
import sigar
s = sigar.open()
mem = mem.system()
swap = sg.swap()
fslist = sg.file_system_list()
print "====Memory ===="
print "Information===="
print "\tTotal\tUsed\tFree"
print "Mem:\t",
```

```
@Output
==================
Information====
Total Used Free
Mem: 8388608 6061884 2326274
Swap: 131072 16048 115024
RAM: 8192 MB
====File System ====
Information====
Filesystem Size Used Avail
Use% Mounted on Type
```

```python
def format_size(size):
    return sigar.format_size(size)

for fs in fslist:
  dir_name = fs.dir_name()
  usage = sg.file_system_usage(dir_name)
  total = usage.total()
  used = total - usage.free()
  avail = usage.avail()
  pct = usage.usage_percent() * 100
  if pct == 0.0:
    print fs.dev_name(), format_size(total), format_size(used), format_name(name), '/', fs.type_name()
```
