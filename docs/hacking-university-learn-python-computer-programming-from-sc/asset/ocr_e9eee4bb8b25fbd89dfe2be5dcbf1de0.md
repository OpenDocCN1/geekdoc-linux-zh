# # Inheritance

In your more robust and expansive programs, you might use multiple related classes. As an example, think of the program where you must categorize devices on a network. Each device type (desktop, laptop, phone, etc…) will have its own class, but you will ultimately be repeating commonly used attributes. Both desktops and laptops will have names, departments, and IP addresses, but they will also have a few distinct variables specific to them such as Wi-Fi for the laptops and graphics cards for the desktop.

Through a process called “inheritance”, classes can be put into a parent/child relationship where certain parent attributes can be “inherited” by children classes. Effectively sharing attributes across classes leads to more elegant organization and less code overall.

```
```
class device:
    
    total_devices = 0
    
    def __init__(self, name, owner):
```
```