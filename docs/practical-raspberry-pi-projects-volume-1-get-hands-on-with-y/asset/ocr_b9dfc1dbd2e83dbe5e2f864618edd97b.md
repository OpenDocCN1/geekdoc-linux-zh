# RUN SCIENCE EXPERIMENTS ON THE EXPEYES KIT

![](bbox=[0.0, 0.06, 0.95, 0.7])

*Above* There’s a great range of experiments for you to try inside the ExpEYES documentation over at: bit.ly/1EH7dvfy

A digital storage oscilloscope is a useful tool in any engineer or hacker’s toolbox, as it enables you to get insights into your projects that aren’t possible with visual checks

+   14  **The Python library (continued)**
+       Now we will plot a sine wave using the ExpEYES and PyLab libraries. On the device, connect OD1 to IN1 and SINE to AI with some wire. Run the following code and you should see that a sign wave has been plotted.

```
```python
import expeyes.eyes
from pylab import *

p=expeyes.eyes3.open()
p.set_state(10,1)
print p.set_voltage(2.5)
ion()
t,v = p.capture(1,300,100)
plot t,v
```
*in interactive mode*
```

+   15  **Further experiments**
+       This tutorial has shown you just a single example of the documented ExpEYES experiments available at http://expeyes.in. There is a wide variety of different techniques and phenomena explored in those experiments, so it is highly recommended to get your hands on an ExpEYES kit and work through them. Running through those examples as a beginner will give you a much deeper understanding of electronics.

+   16  **The verdict**
+       A digital storage oscilloscope (plus extras) is a useful tool in any engineer or hacker’s toolbox, as it enables you to get insights into your projects that aren’t possible with just visual checks or using a multimeter. Whilst no £50 oscilloscope will compare to expensive professional units, this is a great entry-level product as well as a versatile, portable USB device with multiplatform support for when you just can’t be lugging around a 10 kg, £1000+ scope.