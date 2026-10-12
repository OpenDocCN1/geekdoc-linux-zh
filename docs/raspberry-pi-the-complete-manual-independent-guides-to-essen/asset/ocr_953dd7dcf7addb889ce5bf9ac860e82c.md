# ### Projects

# ## Build a Raspberry Pi-powered car

# **Raspberry Pi-controlled car build process**

To help our toy car come to life using the latest web technologies and our credit card-sized computer, we're going to need to make some pretty significant changes to its workings. Fortunately, the most complex aspects of the build can be accomplished with a couple of affordable purchases, namely a servo controller board to take care of the steering and throttle, and a 5V battery pack to keep the Raspberry Pi running smoothly.

# **Identify and remove old radio**

**01** This project is effectively replacing the car's normal transmitter and receiver Notice the three sockets on the original receiver: one goes to the motor controller and one to the steering servo. Some remote-control cars also have separate

battery for the electronics, but those (especially with an electronic speed controller with BEC) get their 5V power supply directly from the speed controller, saving on components. If you don't have a speed controller with 5V BEC, you'll need to get a 5V

supply elsewhere. Many shops sell 5V battery power supplies – often as mobile phone emergency top-ups. www.modmypi.com sells a suitable 5V battery power bank for under £20 and you should get a couple of hours of use from your Raspberry Pi.

![](bbox=[0.05, 0.5, 0.94, 0.97])

**Power up**
The 5V battery pack keeps our Raspberry Pi running for a good five hours

**Servo control**
Addfull PWM DC servo driver board from www.modmypi.com

**Pi-powered**
The Raspberry Pi sits front and centre to keep it as safe as possible

**Pick a car**
You can use pretty much any affordable car for this project