# # My Pi project

# # Automate your indoor garden

John Shovic's indoor garden monitoring system is the perfect project for new and seasoned Pi makers alike

![](bbox=[0.05, 0.1, 0.25, 0.18])

**We’ve seen some pretty unique projects using the Pi, but the Smart Plant is entirely different. How did the concept come about?**

The original SmartPlantPi idea came from a discussion in a local pub. We were brainstorming about what we could build with the amazing amount of environmental sensors out there (while staring at my beer) and I suggested that we build an automated plant-watering system for the Raspberry Pi. What made me think of that? I had been teaching a class at the local university, CS270 Systems Programming, in which I had Raspberry Pi computers for each student to take home and build projects.

Linux can be an intimidating study when you are down in the command line studying the kernel and the multitasking system. I decided to have the students do what I call “Physical Computing”, which is where we build sensor-based projects, like a sunlight analyser, and then use LEDs and other devices for the Raspberry Pi to interact with the environment.

**How long did it take you to go from concept to a fully made product? Did you encounter any issues during the build process?**

The development of the SmartPlantPi kit took about three months from (the) start to the finish of the project and kit documentation. The big choice we made in the hardware design was the decision to go with the Grove connector system. The Grove system is a standard plug used to connect a variety of small computer devices together. All told, there are about 200 different Grove sensors out there, from a number of different manufacturers. All of the Grove connectors are the same size and have four wires but come in four flavours: FC, Digital, Analog and Serial. Going with an all-Grove design means there is absolutely no soldering required for SmartPlantPi, which makes the project much more accessible for all levels of makers.

**For those who may be unaware of the SmartPlantPi, could you give them an overview of what the project is?**

SmartPlantPi (or Smart Plant for short) is an introductory, easy-to-build Raspberry Pi-based environmental monitoring and plant watering system using advanced sensors to monitor the soil moisture, monitor the sunlight, watch the air quality and monitor temperature and humidity. It is designed to be easy and simply put together and tested with no soldering required. Smart Plant also comes with a USB-controlled pump, water flow sensor, plastic tubing for the water, and buttons for control.

**Would you say the focus of this project is on education? Can adults benefit from it as well?**

Well, everything we build for the maker market is designed for education and learning. Making is education. Making is learning. Building your own projects allows you to innovate around a framework and do wonderful things that we have never thought of.

> “Making is learning. Building your own projects allows you to innovate”

The educational goals for Smart Plant are:

+   - Learn about the Raspberry Pi and installing software on the Pi
+   - Connecting up sensors to the Raspberry Pi
+   - Learning about feedback loops and regulating water to plants
+   - Understand your indoor environment and what affects it
+   - Learn about the new technology called the Internet of Things

**What sort of role does the Raspberry Pi play here?**

The Raspberry Pi is the key component of the system. It is the brain. We could have designed this using a much simpler computer, such as an Arduino, but we wanted to provide the power of the Pi and Linux to allow the Smart Plant to be connected up to the Internet of Things and Alexa. To do that, we needed computing power, and the

Raspberry Pi provides all of that in a single inexpensive project.

**We’ve seen mentions of multiple sensors being bundled in with the Smart Plant Pi, what do they bring to this project?**

The sensor package provides a whole indoor environmental monitoring system. Temperature, Humidity, Sunlight, UV Index, and one very cool sensor: the Air Quality Sensor. We were amazed at how sensitive this inexpensive sensor was. We could detect all sorts of events in the entire house. One thing to point out is that virtually all of the time the sensor was under 3200 (rated fresh air) and the average was 2727 across the entire period.

**Are people able to track the progress of their plant at all?**

Absolutely, there are a couple of ways. The first is with the built-in OLED display. It displays status and also flashes alarms when detected. Secondly, we can monitor your plant on the internet by using PubNub and Freeboard.io (a tutorial on how to do that is part of the SmartPlantPi documentation). Here is a live link to our demo plant: freeboard.io/board/BhKt4Y

**How have you found working with the Raspberry Pi in this project? Would you use it for other projects in the future?**

The Raspberry Pi in this project is the best and most capable platform for designing projects and prototyping products. We can build projects that can do amazing things and make use of the thousands of software packages and sensors available for the Raspberry Pi.

**What is our next Raspberry Pi Kickstarter? We are building a board that will allow the maker to experiment with artificial intelligence on the Raspberry Pi with some neural network hardware assists. Can you just imagine what we can build with that? Technology doesn't just have to be the domain of the technologists. We all can be part of this future. Learn. Make. Repeat.

![](bbox=[0.79, 0.23, 0.95, 0.31])

**John Shovic**
has spent over 30 years in hardware engineering, and is a proud author of over 50 papers, including coverage of Arduino and the Raspberry Pi.

**Like it?**
You can boost a pretty incredible portfolio of work, much of which he goes into detail in over on his site at switchdoc.com. Make sure you take a look at the site's tutorial section, which is packed with tips and tricks for beginner and advanced Pi projects alike.

**Further reading**
The entire process of the SmartPlantPi is fairly complex, and if our brief overview here hasn't enough, then make sure you head across to the switchdoc.com website where a full rundown is available.