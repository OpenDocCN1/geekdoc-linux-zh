equivalent here, and every file added to the sketch, even if it is a library file from another directory, is copied into the sketch directory. Note that despite the visual similarity to C code, all files are given the extension `.pde` for clarity.

> **Note** You cannot create a sketch of a given name. Instead, you must create a blank new sketch and then select Save As as a separate step.

The build process itself is handled behind the scenes using `avr-gcc`, a cross-compilation toolchain for the Atmel AVR RISC processors, of which the ATmega168 is one. It creates a separate applet directory inside the sketch folder and copies all the header files into it, along with a concatenation of all the source files (ending in `.pde`). It is this `.cpp` source file that is then cross-compiled into Intel hex for upload to the Arduino.

# Arduino Software

The simplest circuit that most people build to test their setup is that of a flashing light. Pin 13 on the Arduino Diecimila board has a built-in resistor, allowing you to directly connect an LED to it and the 5V supply without damaging it. Some boards even have a surface-mounted LED, so you don’t even need that! The blink tutorial code, which can be loaded from the IDE (File > Examples > 01.Basic), is simply this:

```
```cpp
int ledPin = 13;              // LED connected to digital pin 13

void setup()                    // run once, when the sketch starts
{
  pinMode(ledPin, OUTPUT);      // sets the digital pin as output
}

void loop()                     // run over and over again
{
  digitalWrite(ledPin, HIGH);   // sets the LED on
  delay(1000);                  // waits for a second
  digitalWrite(ledPin, LOW);    // sets the LED off
  delay(1000);                  // waits for a second
}
```
```

It is easy to understand this code, with many of the usual C/C++/Java-ism being unnecessary:

+   - No header files are needed
+   - Main has been replaced by two functions: setup and loop
+   - There is no event loop or callbacks. You must read the pin states each time around a loop

If you are a classically trained developer who vehemently opposes the blocking function delay() used here, then there are examples that demonstrate the use of the millis function to infer the timing without blocking.

For most complex software and libraries, you can, of course, reference header files, but remember that any additional source files added to the project will be copied. It is certainly possible to create your own libraries, but on such small-scale projects, it often proves to be a bigger time sink.