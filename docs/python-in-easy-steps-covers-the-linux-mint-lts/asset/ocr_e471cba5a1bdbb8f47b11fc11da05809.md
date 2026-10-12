| %M | Minute number 0-59 |
| %p | AM or PM equivalent for locale |
| %S | Second number 0-59 |
| %w | Week day number 0(Sunday)-6 |
| %W | Week of the year number 0-53 |
| %X | Time appropriate for locale (%x for appropriate date) |
| %Y | Year 0001-9999 (%y for year 00-99) |
| %z | Timezone offset from UTC as +HHMM or -HHMM |
| %Z | Timezone name |

![](bbox=[0.12, 0.39, 0.22, 0.46])

As the datetime object is in a module of the same name, simply importing the module means it would be referenced as **datetime.datetime**. Use **from datetime import \*** so it can be referenced just as **datetime**.

![](bbox=[0.12, 0.53, 0.22, 0.6])

As the **strftime()** method requires a string argument, the directive must be enclosed between quote marks.

+   1. Start a new Python script by importing the “datetime” module to make its features available 
+      from datetime import *

![](bbox=[0.12, 0.73, 0.22, 0.83])

+   2. Next, create a datetime object with attributes assigned to current date and time values then display its contents