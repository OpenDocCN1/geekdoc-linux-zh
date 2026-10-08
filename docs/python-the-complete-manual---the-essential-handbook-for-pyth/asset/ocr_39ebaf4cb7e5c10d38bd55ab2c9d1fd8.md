# Introducing Python

# 50 Python tips

# Working with
CSV files

package you will need to install
them from your distribution's
package manager.

# Logging to system log

After installation you can use
the command 'easy_install' to
perform any Python package
management tasks that are
necessary.

47 You can use the module
'syslog' to write to system log.
'syslog' acts as an interface to UNIX
log libraries.

45 CSV files are very popular
for data exchange. The web
using the module 'csv',
You can read and write CSV files.

Example:

+   - import csv

+   - # write status values
- writer = csv.writer('stocks.csv', 'w',
newline='')
- writer.writerow([
('GOOG', 'Google, Inc.',
505.24, 0.47, 0.19),
('YAHO!', 'Yahoo, Inc.',
27.38, 0.33, -1.22),
('CNET', 'CNet, Inc.',
16.2, -8.13, -1.49)
])

Example:

Installing simplejson
using setuptools:

+   - kunalumba-sudo
easy_install simplejson
Searching for simplejson
Reading here: http://python.org/
simple/simplejson/
Reading here: http://undefined.
2.9

+   - import syslog
syslog.log('mygeekeack:
started logging')

+   - for an i ['a', 'b', 'c']:
- b = 'mygeekeack: I found
letter a'

+   - syslog.sys(b)
syslog.log('mygeekeack:
the script goes to sleep now,
bye,bye!')

+   - python myfile.py
- tail -f /var/log/messages ---
Nov 18 22:34 ubuntu

+   - # read status data,
status messages
- stocks = csv.reader(
open('stocks.csv',
'rb'))
- status_labels = {'-': 'down',
'0': 'unchanged', '1': 'up'}
for ticker, name, price,
change in stocks:
- status = status_labels[float(change), 0.0)]n- print "%s %s %%%" % (name, status, pct)

+   - Downloading http://
pypi.org/packages/
source/simplejson-2.9.tar.gz.md5
=af5e67a9c3a480563411d57e6d4

+   - Processing simplejson
setup.py -q dist_egg
--dist/tmp/
easy_install-PyYAML
simplejson-2.9-egg-info/
tmp-GW

+   Nov 18 22:34 ubuntu ubuntu:
geekeack: started logging
Nov 18 22:34 ubuntu ubuntu:
geekeack: I found a letter
Nov 18 22:34 ubuntu ubuntu:
geekeack: I found letter b
Nov 18 22:34 ubuntu ubuntu:
python: I found a letter
nter c

# Installing third-party
modules using setuptools

+   - Adding simple2.9
to easy-install.pth
Installed /usr/local/packages/
simplejson-2.9-py2.6
linux-1866

+   Processing dependencies
for simplejson
Finished processing
dependencies for simplejson

# Third-party
modules

46 'setuptools' is a Python package
which lets you download, build,
very easily. To install and uninstall packages
using the 'setuptools'

Generating PDF
documents

48 'ReportLab' is a very
popular module for PDF
generation from Python.

# You can use the module 'random' to
erate a variety of random
numbers with the basic generator

```
$ wget http://www.
reportLab.org/ftp/
```