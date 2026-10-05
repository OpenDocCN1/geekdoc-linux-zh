In the early days of the Raspberry Pi, the only access to the GPIO pins was if you were running in Supervisor, or Root, mode. Fortunately, this has now changed so that you can run in Normal Mode with most libraries.

While the newly introduced Thonny IDE (Integrated Development Environment) is popular with beginners, our preferred environment for writing Python is IDLE3(it has more features), but either can be used. IDLE3 and Thonny can both be accessed from the main Desktop Raspberry menu. pick one of the you and create a new file, in Python, then type in the program shown in Listing 16-1. Remember that, in Python, the code of a matters does spaces at the start of a line, so be sure to get them right; otherwise, you will get errors when trying to run your code.

# **Listing 16-1:** LED Blink

```
#!/usr/bin/python3
import time
import R.GPIO as io # using R.GPIO

io.setmode(io.BCM)
io.setup(4,io.OUT) # make pin into an output

print("LED blinker - By Mike Cook")
print("Ctrl C to quit")
while True:
io.output(4,0)
time.sleep(0.3)
io.output(4,1)
time.sleep(0.3)
```

Save the file and run it. Your LED blinks just like the Scratch example.

Take a look at Listing 16-1 line by line. The program starts by importing the packages you need. In this case, it's the package we use to achieve a Delay, or Wait, function, and the R.GPIO package to access the GPIO pins. Note that a lot of examples use GPIO in the import statement - but we prefer the simpler and shorter as io it reduces the amount of typing and we don't have to keep switching to uppercase. Then you have to tell the library sort of numbering system you want to use. We're using the now-standard BCM system. The next line tells the GPIO pins that you want to use Pin 4 as an output. The setup method takes two values: the pin number and a number that tells the library to make an output. This is conveniently hidden by the library, by