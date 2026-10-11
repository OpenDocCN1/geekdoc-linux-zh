
## Digital Camera Conversion

Classic aesthetics with modern convenience, this old-school camera has been upgraded with a Raspberry Pi

![](img/a1548a579bd09ff29b2b92de3f565e63_155_0.png)

**Maker Profile**
**Pete Taylor**
Web manager

Pete works for a charity and has always tinkered with computers, ever since he got a hand-me-down BBC computer. He likes that the Raspberry Pi returns to a time when you could hack your own computer without making an expensive mistake.

Find out more: bit.ly/1KRASw

> “The Raspberry Pi is a maker’s dream – it’s cheap and cheerful, and the community built around it is a brilliant resource”

### Do it yourself

Version two of the project will result in a kit that people can use to convert their own cameras “that doesn’t require you to take a Dremel to the insides of a Holga”. He’s not decided yet on whether to make a kit that converts a Holga, or a kit that builds a Holga-esque case around the Raspberry Pi itself. Either way, the whole thing should also have a better photo-taking capability, which is the ultimate goal.

Old cameras have a very specific design aesthetic that it seems has been lost to time, although nostalgia for them is still very strong in certain circles. Unfortunately, while nostalgia, desire and working cameras still exist in the 21st Century, usable film is quickly dwindling in supply. So if you like the aesthetic and aren’t too bothered about using the old photo process, why not upgrade the insides with more modern technology?

“I wanted a suitable case for the Raspberry Pi camera board”, Pete tells us, “and the Holga seemed a perfect fit. Most of the available cases are either a bit ugly or suited more towards stationary webcam-type applications.”

“The Raspberry Pi is a maker’s dream – it’s cheap and cheerful, and the community that’s built up around the Pi makes a brilliant resource when you’re stuck with a problem or want to find out more.”

The entire build doesn’t require a massive amount of components either. As well as the actual camera and Pi itself, Pete used a Raspberry Pi camera board to actually take photos, a Wi-Fi module for connecting to it remotely, a battery and a switch for it, and a few buttons and resistors to wire up the camera’s control buttons to the Pi.

“It works better than I expected!” Pete said about the quality of the finished product. “Although it seems a bit daft to build a camera that’s about as good as you’d get from a cheap camera phone, it’s changed the way I take pictures. By removing the instant replay – most people seem to view the world through the displays on their phones – I can concentrate on taking the photo. Only seeing the pictures when I’ve taken the camera home and downloaded them to my PC adds a bit to the film nostalgia and I’m often surprised by the photos I’ve taken. Plus I’ve received some nice feedback about how the camera looks.”

This is only the first iteration, and Pete has plans to make the next build easier and also use the original lens with the Pi camera.

- **Top-left:** The camera of the past, updated for today.
- **Left:** The Pi is the perfect size to fit inside the camera case

![](img/a1548a579bd09ff29b2b92de3f565e63_155_1.png)

## 20 RASPBERRY PI HACKING PROJECTS

## Bitcoin Pool Table

*Modern pool pros pay digitally by scanning a QR code to insert Bitcoins*

**Maker Profile**
**Stuart Kerr**
Technical director

Stuart Kerr is the technical director of Liberty Games, which specialises in classic table and bar games. You might have heard of some of their hacks.

Find out more: libertygames.co.uk

Liberty Games loaded a Raspberry Pi into the side of a pool table that enables people to make payments via a Bitcoin app on their phone to release the balls. "We did this with the Raspberry Pi 1", Stuart tells us. "We tried to install the entire Bitcoin client on the Pi but it was struggling, and downloading the whole blockchain caused issues too. It was going to be connected to the internet, so we offloaded the heavier work to a server able to handle the blockchain. The server receives the Bitcoin payment and then communicates to the Pi securely that the payment has come in, and it syncs up the prices as well." "We connected a PiFace via a breakout board that's monitoring on WebRTC for the go-ahead from the server, and once it gets that, it sends the physical voltage to the electrical ball release mechanism."

![](img/a1548a579bd09ff29b2b92de3f565e63_156_0.png)

*Above The price of a game is displayed, in Bitcoins, on the PiFace display module*

![](img/a1548a579bd09ff29b2b92de3f565e63_156_1.png)

## Fireball Pinball

*Ian Cole and his sons enter the high score boards with Fireball HD*

**Maker Profile**
**Ian Cole**
Maker and geek raiser

Ian Cole is a keen maker, hacker and inventor, and regularly blogs about his family projects with his two sons. Their Fireball Project, for example, grew out of an innocent "Can you make it playable?"

Find out more: raisngeeks.com

At raisingeeks.com, Ian Cole and his two sons love a challenge. So the chance to repair a game table gave them the perfect Raspberry Pi primer. "We've taken an existing pinball machine playfield," says Ian, "and built a new game from it. This required learning the underlying hardware first. Then we learned how to use the Raspberry Pi, pygame for sound and text graphics, and omplayer for HD video, and we connected the software tools with the hardware of the pinball machine. "We built a MOSFET circuit on a breadboard to test a single solenoid. When that worked, we duplicated it onto a hand-soldered protoboard and extended it to control the five solenoids. The Raspberry Pi handles graphics, audio, scoring rules, saving scores, etc. One Arduino drives the lamp and switch matrix, another drives the solenoids. The three are connected with an I2C bus."

## LED Voice-Controlled Coffee Table

*Light up your living room with a voice-controlled light show for a coffee table*

**Maker Profile**
**Mikel Duke**
Software developer

Mikel loves programming, photography, biking, archery, and sharing projects.

Find out more: bit.ly/1FOhDKW

Mikel found himself in a quandary: he didn't have a coffee table. However, instead of just heading to Ikea and picking up a LACK, he decided to make one himself. Not just any coffee table though, one that lit up using a Raspberry Pi to control the sequence. "I used the Raspberry Pi because it was easy to work with and has a great community. Whenever I run into an issue, there is always documentation on how to fix it. I wanted to have network support and do more complex operations, like loading images, then I could do just using an Arduino with Ethernet. The combination of the two really made development faster. Now that Pi 4 has added support for the Raspberry Pi's integrated SPI, I am working on controlling the LEDs directly, without the Arduino." Recently, Mikel added voice control to it, using Google Now. "After you say a command to Google Now, Autovoice, a plugin for the Android app Tasker, intercepts the response back from Google. If the response matches a Tasker task, the task will be launched. I have a few tasks set up to make web service calls, basically calling a URL with parameters. This URL connects to a Java based web service I created, running on my Raspberry Pi." Mikel also encourages users not to use coasters, as drinks light up well when the table is switched on.

## Project Jarvis

The 1950s future today with your voice-activated smart home automation system

![](img/a1548a579bd09ff29b2b92de3f565e63_157_0.png)

*Above Alarm mode can only be disabled with the right finger or the master code*

> **Maker Profile**
>
> **Mayur Singh**
> *Computer systems engineering student*
>
> Located in South Africa, Mayur's expertise is in embedded systems and he is familiar with microcontrollers and systems that enable outside hardware interaction, such as the Raspberry Pi and the BeagleBone Black.
>
> Find out more: bit.ly/1Evlmc1

Home automation has been a thing for years now, with a fair few intrepid engineers and DIYers modifying their home. With wirelessly controlled lights, heating, garage doors and many other household items, it’s amazing what some have achieved. Science fiction has always portrayed houses with advanced systems and Mayur has been busy creating such a system.

“The major inspiration came from watching the *Iron Man* movies, which is where the name Jarvis comes from. I decided to build a simple home automation system, however over the many years and many reinstalls of Windows, I lost my program. I built a new and improved home automation system, which features an AI assistant and more functionality, after I saw the third *Iron Man* film.”

While home automation is one part of the project, convenience isn’t the only factor.

“The main function of the system is to help save energy in homes,” Mayur tells us. “Jarvis can read and monitor the electricity usage per light or appliance and this lets the AI perform certain tasks. These tasks are determined by outside factors, like whether or not a light should be switched on if there is adequate natural light in the room. This is a basic example but other factors influence the determination of the AI, which has control over the power to each light or appliance. The data is logged throughout the month and the system uses that information to achieve better results the following month. This is smart home automation.”

“The Jarvis AI is a major part of it, and you can talk to it. “He can control your home using voice interaction and make basic decisions about energy savings in a room. I have also recently built a wall-mounted tablet system that links to a local online grocery store. It uses voice control to identify products you need and adds the items to a list until you specify the delivery.”

With a year and a half of work on the project, everything Mayur has completed works reliably, but there are still more functions he wants to add.

> “The Raspberry Pi is a maker's dream – it's cheap and cheerful, and the community built around it is a brilliant resource”

*Left The Jarvis interface is gorgeous, but you can control the system from anywhere using your smartphone or your voice*

![](img/a1548a579bd09ff29b2b92de3f565e63_157_1.png)

### The voice

The Jarvis that this project is named after is well-known for its snarky remarks and tone of voice. Choosing an actual voice that works is a hard enough task without going for a certain style, as Mayur explains: “It’s been difficult trying to find voices with a good API and price but I have settled for a free API which offers cloud conversion and just sends an MP3 sound file back. It takes longer but it ensures that the voice works on all OS’s.”

If you're interested in having a go at creating your own Jarvis-esque home automation system then thankfully you are in luck. You can check out Joey Bernalds' extensive three-part series beginning on page 78 (of this very book) that explains how to set up a digital assistant that uses PyAudio and a few voice recognition modules in order to parse your spoken commands.
