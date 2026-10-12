
# Pvaders part 2: graphics and sound

## Projects

```python
if self.ani_pos < 5:
    Player.image = self.ship_sheet.subsurface(
        self.ani_pos[0], 0, 0)
else:
    if self.ani_pos < 5:
        Player.image = self.ship_sheet.subsurface(
            self.ani_pos, 0, 0)
        self.ani_pos += 1

def player_explosion(self):
    if self.explode:
        if self.explode < 8:
            self.explosion_image = self.explosion_sheet.
            subsurface(0, self.explode_pos*9, 73, 99)
            self.explode_pos += 1
            self.screen.blit(self.explosion_image, [self.player.
            rect.x-18, self.player.rect.y-30])
        else:
            self.explode = False
            self.explode_pos = 0

def alien_explosion(self):
    for alien_explo in self.alien_explosions:
        if self.alien_explo < 9:
            self.alien_explo_graphics = self.alien.
            explosion_sheet.subsurface(0, self.alien_explo_pos*9, 94,
            99)
            self.alien_explo_pos += 1
            self.screen.blit(self.alien_explo_graphics, [self.
            rect(self.explo_dan[0]) + 50, self.explo_dan[1] + 60])
        else:
            self.alien_explo = False
            self.alien_explo_pos = 0
            self.explo_dan_alien = []

def splash_screen(self):
    while GameState.start_screen:
        self.fill_alo()
        self.screen.blit(self.infro_screen, [0, 0])
        self.screen.blit(self.infro_text, render("FIVAGOS", "white", 65, 120))
        self.screen.blit(self.game_font_render("PRESS SPACE TO PLAY", "white", 15, 270, 30))
        pygame.display.flip()
        self.control()
        self.clock.tick(self.refresh_rate / 2)

def make_player(self):
    self.player = Player()
# Find the rest of the code at github.com/rss876/pvaders
```

## Animating explosions

10 The `player_explosion()` and `alien_explosion()` methods that come after the player animation block in the Game class are similar but simpler executions of the same thing. As we only need to run through the same predefined set of frames (this time vertical), we only need to see if the `self.explo` and `self.alien_explo` flags are true before we increment the variables that change the image.

## Adding music

11 Pygame makes it easy to add a musical score to a project. Just obtain a suitable piece of music in our preferred format (we found ours via freesound.org) and load it using the `Mixer` Pygame class. As it's already been initialised via `pygame.init()`, we can go ahead and load the music. The `music.play()` request that the music should start with the app and continue to loop until it quits. We replaced 1 with the -1 music loop flag, so it plays continuously. Learn more about the `Mixer` class at www.pygame.org/docs/ref/mixer.html

## Using sound effects

12 Loading and using sounds is similar to how we do so for images in Python. First we load the sound effect using a simple assignment. For the laser beam, the initialisation looks like this:

```python
self.bullet_fx = pygame.mixer.Sound('location_of_file')
```

Then we simply trigger the sound effect at the appropriate time. In the case of the laser, we wait to play whenever we press the space bar to shoot, so we place it in the Game class's `control` method, but right after we raise the `shoot_bullet` flag. You can get different sounds from www.freesound.org.

> "Sprite sheets make it easy to draw to the screen, but it also keeps the asset count down and performance levels up"

# Build a Raspberry Pi-powered car

## What you'll need...

- A toy RC car with two channels (steering and drive)
- Adafruit PWM I2C servo driver
- Female-to-female jumper cables
- 5V battery power bank
- *Estimated cost:* £60 / $100
- Components from www.modmypi.com

## Build a Raspberry Pi-powered car

Make use of cutting-edge web technologies to take control of a remote controlled car with a smartphone or tablet....

![](img/59caadfa348382a5c408c25137901e27_129_0.png)

> **Did you know...**
> You can make this project work with just about any remote-controlled car. Follow the guide for more details.

Web technologies are moving forward at a huge pace, cloud technologies are bringing mass computing to individuals, and hardware has reached a perfect moment in time where sensors, displays and wireless technology have all evolved into efficient and affordable devices. We truly are at a point where nearly anyone can take an idea from nothing to a working product in a week and at very little cost. Just like this project, which is fun, quick and easy to build on and a fantastic way to learn. We’re going to grab an old remote-control car, rip off its radio receiver and replace it with the Raspberry Pi, hook it up on the network, fire up a bleeding-edge web server and then get your smartphone or tablet to control it by tilting the device. By the end of this, not only will you have a fun toy, you will have learnt about the basic technologies that are starting to power the world’s newest and biggest economy for the foreseeable future. Welcome to tomorrow!

![](img/59caadfa348382a5c408c25137901e27_130_0.png)

## Raspberry Pi-controlled car build process

To help our toy car come to life using the latest web technologies and our credit card-sized computer, we're going to need to make some pretty significant changes to its workings. Fortunately, the most complex aspects of the build can be accomplished with a couple of affordable purchases, namely a servo controller board to take care of the steering and throttle, and a 5V battery pack to keep the Raspberry Pi running smoothly.

### Identify and remove old radio

01 This project is effectively replacing the car's normal transmitter and receiver. Notice the three sockets on the original receiver: one goes to the motor controller and one to the steering servo. Some remote-control cars also have separate battery for the electronics, but those (especially with an electronic speed controller with BEC) get their 5V power supply directly from the speed controller, saving on components. If you don't have a speed controller with 5V BEC, you'll need to get a 5V supply elsewhere. Many shops sell 5V battery power supplies – often as mobile phone emergency top-ups. www.modmypi.com sells a suitable 5V battery power bank for under £20 and you should get a couple of hours of use from your Raspberry Pi.

![](img/59caadfa348382a5c408c25137901e27_131_0.png)

**Power up**
The 5V battery pack keeps our Raspberry Pi running for a good five hours

**Servo control**
Adafruit PWM I2C servo driver board from www.modmypi.com

**Pi-powered**
The Raspberry Pi sits front and centre to keep it as safe as possible

**Pick a car**
You can use pretty much any affordable car for this project

### Attach the servo cables to the new controller

02 We soldered our 16-channel I2C servo controller board from www.modmypi.com as per its instructions and simply plugged channel 6 (steering) and channel 1 (motor) headers onto it. There are six cables in total: the bottom two are ground; the middle two are the power and the top two are the PWM (pulse-width modulation) signals. This is a good time to think of places to mount the extra components and the best fixing method seems to be sticky-back Velcro.

![](img/59caadfa348382a5c408c25137901e27_132_0.png)

### Connect the I2C bus to the Raspberry Pi

![](img/59caadfa348382a5c408c25137901e27_132_1.png)

03 We’re using the Raspberry Pi’s I2C bus to control the servo interface board, which only needs four cables – they all go between the Raspberry Pi and the servo controller board as pictured. Visit http://bit.ly/N3nq41 for a tutorial on how to set up I2C on the Raspberry Pi. From top to bottom we need to use the 1, GND, 2, SCL, 3, SDA and 4 VCC, which map directly to the same ports on the Raspberry Pi. Essentially this is power, ground and two communication channels.

### Hooking it up to the Raspberry Pi

04 On a Rev 1 Raspberry Pi, the I2C cables look the same. Though the Rev boards have different labelling, the physical pins are in the same place. Bottom left (closest to the Raspberry power connector) is the 3.3V power; next to that is the SDA header, which is the data channel. Next to that in the bottom row is the SCL channel, which controls the clock of the I2C devices. And finally – on the top-right port – is the Ground. We recommend printing a labelled image of the GPIO pins.

### Overview of the main components

05 You should now have the servo board in the middle with the steering servo and speed controller on one side and the Raspberry Pi on the other. The motor is connected to the other end of the speed controller (that end should have much thicker wires); the speed controller also has two thick wires going to the main car’s battery – in this case a 7.2V NiCad. We now have two very separate power systems with the high current motors on one side and the low current electronics on the other. Let’s make sure it stays that way!

### Find everything a home

06 We can now put it together. Use plenty of sticky-back Velcro, tie wraps or elastic bands to keep everything secure and find spaces in the car’s body to hide the wires where possible. While it is possible to stick or screw the Raspberry Pi directly to the car, we recommend to use at least the bottom half of a case for added protection and ease of access. Insert our SD card, network cable or Wi-Fi dongle and power supply. Sit back and admire your hacking skill!

![](img/59caadfa348382a5c408c25137901e27_132_2.png)
