# Projects

# Raspberry Pi Plus Arduinos

```
delay(1000);
)

void flash(int n) {
  for (int i = 0; i < n; i++) {
    digitalWrite(ledPin, HIGH);
    delay(100);
    digitalWrite(ledPin, LOW);
    delay(100);
  }
}
```

Then, you can send a count from your Python code with something like:

```
ser.write('5')
```

This will flash the LED 5 connected to pin 13 on your Arduino five times. One missing element on the Raspberry Pi is an analogue-to-digital (ADC) converter to take a given voltage and turn it into a number that can be used in some piece of control software. This is where attaching an Arduino can be extremely helpful, as it has a 10-bit ADC converter included. The following code will read the voltage on pin 3 and send it out over the serial connection to the Raspberry Pi.

```
int analogPin = 3;
int val = 0;
void setup() {
  Serial.begin(9600);
}

void loop() {
  val = analogRead(analogPin);
  Serial.println(val);
}
```

This maps the measured voltage to an integer between 0 and 1023. The minimum voltage is zero, while the maximum voltage can be set with the function map(maxReference). By default, the maximum is the power supplied to the board (5

volts for 5V boards, or 3.3 volts for 3.3V boards). You can also use two internally supplied reference voltages, one at 1.1 volts and a second at 2.56 volts. For special cases, you can supply an external reference voltage to the AREF pin. You need to be sure that it is only between 0 volts and 5 volts.

Going in the opposite direction, you can use the Arduino to supply an output voltage. This is done by using a PWM (pulse width modulation) output signal. The idea is to actually send out a number of pulses with some duty cycle that is on for some percentage of the time and off for the remainder of the time. For example, if you have an LED connected to one of the pins, you can light it at half brightness with the following code.

```
int ledPin = 9;
void setup() {
  pinMode(ledPin, OUTPUT);
}

void loop() {
  analogWrite(ledPin, 127);
}
```

The second parameter to the analogWrite() function is a value between 0 and 255, which defines the duty cycle between 0% (or fully off) to 100% (or fully on). This analog output signal stays on at the given duty cycle until a new call to the analogWrite() function. By having your Raspberry Pi write out values over the serial connection, it can then control the output duty cycle by sending a simple integer. This short article will spark some ideas on how you can start combining multiple computing platforms to expand the capabilities of your own projects.

There is no reason to try to find the one silver bullet platform for your project when you can pick the sub-modules that actually do their own individual jobs best and build up the complex behaviour you need from these simpler parts.