![](Image00000.jpg)

Raspberry PiAn Easy Guide to Programming, Developing, and Setup of Raspberry PI Projects for BeginnersALEXISRODRÍGUEZCopyright © 2020 Alexis RodríguezAll rights reserved .It is not legal to reproduce, duplicate, or transmit any part of this document by either electronic means or in printed format. Recording of this publication is strictly prohibitedDisclaimerThe information in this book is based on personal experience and anecdotal evidence. Although the author has made every attempt to achieve an accuracy of the information gathered in this book, they make no representation or warranties concerning the accuracy or completeness of the contents of this book. Your circumstances may not be suited to some illustrations in this book.The author disclaims any liability arising directly or indirectly from the use of this book. Readers are encouraged to seek accounting, legal, or professional help when required.This guide is for informational purposes only, and the author does not accept any responsibilities for any liabilities resulting from the use of this information. While every attempt has been made to verify the information provided here, the author cannot assume any responsibility for errors, inaccuracies, or omission.Contents[INTRODUCTION](#text00004.html_a423)              [CHAPTER ONE](#text00005.html_a424)              [UNDERSTANDING RASPBERRY PI](#text00005.html_a425)              [Different Models of Raspberry PI](#text00005.html_a426)              [The General Features and Provisions of Raspberry PI](#text00005.html_a427)              [The General Provisions of Raspberry Pi](#text00005.html_a428)              [The Specifications of the Hardware of Raspberry Pi](#text00005.html_a429)              [The Central Processing Unit (CPU)](#text00005.html_a42A)              [The Ethernet Port](#text00005.html_a42B)              [The Graphics Processing Unit (GPU)](#text00005.html_a42C)              [General Purpose Input & Output (GPIO) Pins](#text00005.html_a42D)              [Raspberry Pi Memory](#text00005.html_a42E)              [The Universal Asynchronous Receiver / Transmitter (UART)](#text00005.html_a42F)              [Display Monitors or TV](#text00005.html_a42G)              [Power Source Cable or Connector](#text00005.html_a42H)              [The Board of Raspberry Pi Model A](#text00005.html_a42J)              [The Features of the Board of Model A Raspberry Pi](#text00005.html_a42K)              [The Board of Model B Raspberry Pi](#text00005.html_a42M)              [The Features of the Board of Model B Raspberry Pi](#text00005.html_a42N)              [Functionalities of Raspberry PI](#text00005.html_a42P)              [Detailed Explanations of these Projects](#text00005.html_a42R)              [Other Projects you can do using Raspberry Pi](#text00005.html_a42S)              [All the Tools Required to Setup Raspberry PI](#text00005.html_a42T)              [Internet Connection](#text00005.html_a42U)              [Installing Raspberry PI](#text00005.html_a42V)              [Installing Raspbian on a Raspberry Pi](#text00005.html_a42W)              [What is NOOBS?](#text00005.html_a42X)              [NOOBS Installation Manager](#text00005.html_a42Y)              [Raspberry Pi Installer](#text00005.html_a42Z)              [CHAPTER TWO](#text00006.html_a430)              [BASIC PROGRAMS IN PYTHON](#text00006.html_a431)              [Basic Python Programs](#text00006.html_a432)              [Python Programs for Functions](#text00006.html_a433)              [Python Programs for Numbers](#text00006.html_a434)              [Python Programs for Array](#text00006.html_a435)              [Python Programs for Circular Linked List](#text00006.html_a436)              [Python Programs for Doubly Linked List](#text00006.html_a437)              [Python for Native Data Type Programs](#text00006.html_a438)              [Python Programs for Conditions and Loops](#text00006.html_a439)              [The Versions of Python and their Release Dates](#text00006.html_a43A)              [How to Run Python](#text00006.html_a43B)              [Requirements for Running Python Programs on a Raspberry Pi](#text00006.html_a43C)              [Details about Python Libraries](#text00006.html_a43D)              [Running Python Programs Using Terminal](#text00006.html_a43E)              [Running Python Programs through IDE](#text00006.html_a43F)              [Running Python Program Using Thonny](#text00006.html_a43G)              [Executing Python Script with Python Shell](#text00006.html_a43H)              [Reasons for Using Loops in Python](#text00006.html_a43J)              [Benefits of Using Python Loops](#text00006.html_a43K)              [Different Loop Statements in Python Programs](#text00006.html_a43M)              [Features of IDLE](#text00006.html_a43N)              [Types of Python IDEs](#text00006.html_a43P)              [Microsoft Visual Studio IDE](#text00006.html_a43R)              [Numbers and Variables](#text00006.html_a43S)              [Types of Numerical Variables](#text00006.html_a43T)              [Floating-Point Values](#text00006.html_a43U)              [How to Declare Variables and Assign Values](#text00006.html_a43V)              [How to Reference Objects in Python](#text00006.html_a43W)              [How to Create Object Identity in Python](#text00006.html_a43X)              [How to Determine the Names of Variables](#text00006.html_a43Y)              [How to Create Multiple Assignments](#text00006.html_a43Z)              [Assigning a Single Factor to Multiple Variables](#text00006.html_a440)              [Assigning Multiple Factors to Multiple Variables](#text00006.html_a441)              [How to Install the Application Initially](#text00006.html_a442)              [How to Improve Error Handling Using Try and Except Method](#text00006.html_a443)              [CHAPTER THREE](#text00007.html_a444)              [WHAT ARE DICTIONARIES, LISTS, AND STRINGS?](#text00007.html_a445)              [How to Create Dictionaries](#text00007.html_a446)              [How to Access the Values of Dictionaries](#text00007.html_a447)              [How to Add Dictionary Values](#text00007.html_a448)              [How to Delete Elements using del keyword](#text00007.html_a449)              [Understanding the String Theory](#text00007.html_a44A)              [How to Create String in Python](#text00007.html_a44B)              [How to Index and Split Strings](#text00007.html_a44C)              [How to Reassign Strings](#text00007.html_a44D)              [How to Delete Strings](#text00007.html_a44E)              [What are String Operators?](#text00007.html_a44F)              [String Formatting in Python using Escape Sequence](#text00007.html_a44G)              [String Functions in Python](#text00007.html_a44H)              [What are the lists and their functions?](#text00007.html_a44J)              [Built-in Functions in Python Lists](#text00007.html_a44K)              [What are Multiple Assignments and Multiple Return Values?](#text00007.html_a44M)              [Using Multiple Assignments with a List](#text00007.html_a44N)              [Using Multiple Assignments with a String](#text00007.html_a44P)              [Uses of Multiple Assignments in Python](#text00007.html_a44R)              [Multiple Return Values](#text00007.html_a44S)              [Defining and Identifying Function Keys in Python](#text00007.html_a44T)              [Types of Number Conversions in Python](#text00007.html_a44U)              [Using Python Decimal](#text00007.html_a44V)              [Lists and Dictionaries](#text00007.html_a44W)              [CHAPTER FOUR](#text00008.html_a44X)              [UNDERSTANDING CLASSES, METHODS, AND MODULES](#text00008.html_a44Y)              [What is a Module?](#text00008.html_a44Z)              [What are the modules in Raspberry PI?](#text00008.html_a450)              [The Specifications of a Computer Module](#text00008.html_a451)              [Libraries in Python](#text00008.html_a452)              [Features of Matplotlib](#text00008.html_a453)              [Features of Requests Library](#text00008.html_a454)              [Features of Theano Library](#text00008.html_a455)              [Features of Pillow Library](#text00008.html_a456)[Features of Keras Library](#text00008.html_a457)              [Features of Fire Library](#text00008.html_a458)              [Features of NLTK (Natural Language Toolkit)](#text00008.html_a459)              [Features of Arrow Library](#text00008.html_a45A)              [Features of FlashText Library](#text00008.html_a45B)              [What is object orientation?](#text00008.html_a45C)              [CHAPTER FIVE](#text00009.html_a45D)              [HOW TO USE FILES AND INTERNET WITH RASPBERRY PI](#text00009.html_a45E)              [Using Files and Internet on Raspberry Pi](#text00009.html_a45F)              [What are the files in Raspberry PI?](#text00009.html_a45G)              [Step-By-Step Method of Accessing a File in a Raspberry Pi](#text00009.html_a45H)              [How to manage the file system](#text00009.html_a45J)              [How to Create Files](#text00009.html_a45K)              [Deleting Files](#text00009.html_a45M)              [How to Copy Files](#text00009.html_a45N)              [How to Show the Content of a File](#text00009.html_a45P)              [Reading and Writing Files](#text00009.html_a45R)              [Ways to Write Values](#text00009.html_a45S)              [What are the differences between the Internet and Pickling?#](#text00009.html_a45T)              [CHAPTER SIX](#text00010.html_a45U)              [HANDLING GRAPHICAL USER INTERFACES IN RASPBERRY](#text00010.html_a45V)              [GUIs on Raspberry Pi](#text00010.html_a45W)              [What is Tkinter Module in Python](#text00010.html_a45X)              [The Approach on How to Use Tkinter](#text00010.html_a45Y)              [How do Hello World and Temperature Converter operate in GUI](#text00010.html_a45Z)              [Understanding Listbox and Spinbox](#text00010.html_a460)              [The Parameters for Using Listbox](#text00010.html_a461)              [The Methods of Listbox Objects](#text00010.html_a462)              [CHAPTER SEVEN](#text00011.html_a463)              [HARDWARE INTERFACES IN RASPBERRY](#text00011.html_a464)              [Pin Connections in GPI](#text00011.html_a465) .....................................................................................................................[Prototyping Boards in Raspberry](#text00011.html_a466)              [Features of Prototyping Boards in Raspberry Pi](#text00011.html_a467)              [CHAPTER EIGHT](#text00012.html_a468)              [LEAD FADER AND PROTOTYPING PROJECTS](#text00012.html_a469)              [Requirements for Lead Fader Projects](#text00012.html_a46A)              [How to Assemble the Hardware](#text00012.html_a46B)              [Running the Software](#text00012.html_a46C)              [Requirements for Prototyping Project](#text00012.html_a46D)              [How to Assemble Prototyping Hardware](#text00012.html_a46E)              [What are in Phase Two of the Prototyping Project?](#text00012.html_a46F)              [CHAPTER NINE](#text00013.html_a46G)              [PROJECTS IN RASPBERRY PI](#text00013.html_a46H)              [How to Construct a Weather Station](#text00013.html_a46J)              [How to Craft a Security System](#text00013.html_a46K)              [CHAPTER TEN](#text00014.html_a46M)              [HOW TO PROGRAM GAMES](#text00014.html_a46N)              [Step-by-step Process of Games Programming in Raspberry PI](#text00014.html_a46P)              [Types of Games in Raspberry PI](#text00014.html_a46R)              [What are the coordinates?](#text00014.html_a46S)              [How to follow the Mouse](#text00014.html_a46T)              [CHAPTER ELEVEN](#text00015.html_a46U)              [WHAT IS RASPBERRY PI ROBOT?](#text00015.html_a46V)              [Requirements for Raspberry PI Robot](#text00015.html_a46W)              [Connect your System to the Power Source](#text00015.html_a46X)              [How to Handle Autonomous Rover](#text00015.html_a46Y)              [How to Assemble the Hardware](#text00015.html_a46Z)              [CONCLUSION](#text00016.html_a470)              INTRODUCTIONAre you interested in this new small device that has taken center stage of the IT industry? Raspberry PI made a debut on February 24th, 2012. Unfortunately, the website of the supplying firm crashed. However, new models of Raspberry PI 2, have been released and are in circulation.This computer device has a Linux operating system and designed with a High-Definition Multimedia Interface (HDMI) video output. You can connect a computer monitor or television into it. But the monitor must have a DVI connector with HDMI to DVI adapters connected to the system before it can function correctly. Your Raspberry PI may not work if your monitor has only a VGA connector.This device is a global phenomenon. It is useful for various activities such as a regulator for smart home appliances and a media center. Additionally, the Raspberry Pi could serve as a desktop workstation. Now, beginners can code or decode python programming language. In the same vein, experienced programmers that are not conversant with Raspberry PI can learn various ways of using the features and functionalities of the software for different businesses.You can begin to write programs for your device using the renowned Python programming language. You can learn the essentials of graphical user interfaces. Understanding the pygame module will assist you in building fun and exciting games.Raspberry PI Foundation recommended using Raspbian Wheezy distribution. The book contains a perfect representation of this phenomenon for better understanding. It is good to note that the original Raspbian operating system was developed and designed by Peter Green and Mike Thompson.In this book, you will learn the ABC of Raspberry Pi and the requirements of setting it up. You will also learn basic programs in Python. Other things that can help you navigate and use the Raspbian include a comprehensive knowledge of string theory, lists, and dictionaries.How to use files and the internet are necessary information every newbie in the field needs to enjoy this technology. Mastering the operations of GUIs and other hardware interfaces in Raspberry are proficient skills for success in software programming.Let's dive inside the book for you to see and know more!CHAPTER ONEUNDERSTANDING RASPBERRY PI![Raspberry Pi.PNG](Image00002.jpg)Raspberry Pi DeviceRaspberry Pi functions as a desktop computer designed to access the internet and play games. It can help you to build spreadsheets and word-processing documents. Additionally, the Raspbian can help you play high-definition videos.This device can help beginners and experienced software engineers to learn computing skills and programming languages such as Python and Scratch.  A Pi is an affordable computer device as small as a credit card that you can plug into a television or computer monitor. It also functions with a mouse and standard keyboard.The system is a multipurpose machine used for building digital projects. The varieties of projects it can handle include building weather stations, and recording and playing music. Also, it comes with infra-red cameras for tweeting birdhouses.It is designed as a prototype of a computer that enables children to learn to program. They will also know how to operate a computer device.Raspberry Pi is a trademark from Raspberry Pi Foundation. This charity organization is registered and located in the United Kingdom. The registration number is 1129409 . It was founded with the purpose of furthering the academic courses of children and adults interested in acquiring technical skills in the field of computer science and other subjects in that field. Another target market for this product is the literate masses in developing countries, who may avail themselves of the opportunity of learning programming.                                             Different Models of Raspberry PIThere are two models of Raspberry Pi; the first model (A) and the second model (B). The differentiating factor is its USB port. Model A has a port that can consume less power, excluding the Ethernet port. But the B model, including the Ethernet port, can use up more energy. The model B is developed in China.Raspberry Pi is designed as open-source technologies with multimedia web and communication features. The Pi board launched this computer module in 2014 and integrated into a module the board of model B Raspberry Pi. With this, you can use it as an embedded system making the device useful.The General Features and Provisions of Raspberry PIRaspberry Pi exists in different generations, such as the Pi, P2, P3, and P4\. These generations cost like the first models. But vary in the hardware and some features, which reveal upgrades in the Raspbian technology.These latest technologies incorporate a board with a built-in Bluetooth feature. They are enabled by a Quad-Core Broadcom BCM283764bit ARMv8 processor. The P2 operates with 900 MHz, while P3 functions at 1.2 GHz. All these models have four USB ports with a naked board that can be extended, including an upgraded power system.The Raspbian is a well-designed British-made computer device that is a bestseller on the market today, according to Eben Upton, founder of the Raspberry Pi. With this system, you can access more opportunities for the IoT, and accomplish more fantastic projects faster.The new model of this device is designed with a built-in wireless connection. It was featuring a hub with standard internet connectivity. Various gadgets can be interconnected to the device with flexible operational costs. Also, it works with a power source of 2.5 amp. You do not need another cable to power more complex USB devices.The General Provisions of Raspberry Pi

1.  It has Bluetooth of 4.1.
2.  The video outputs include PAL and NTSC (composite video) using 3.5 mm jack and HDMI.
3.  Four USB ports.
4.  A CPU with Quad-core 64-bit ARM Cortex A53 reached at 1.2 GHz.
5.  The device weighs 1.6 oz (45g).
6.  The power source is 5 volts with GPIO header or MicroUSB.
7.  The size of the Raspberry Pi is 85.60 mm × 56.5 mm.
8.  The memory has 1 GB LPDDR-900 SDRAM with Linux Operating System. That is 900 megahertz (MHz).
9.  Raspbian has a network of 10/100 Mbps Ethernet and 802.IIn Wireless LAN.
10.  The GPU has a 400 megahertz (MHz) Video core IV multimedia.
11.  The peripherals 17 GPIO with specific functions and HAT ID bus.
12.  Other specifications include a USB mouse, USB WiFi adaptor.

The Specifications of the Hardware of Raspberry Pi![Inner components of a Raspberry.png](Image00003.jpg)Specifications of a Raspberry PiThis microcomputer is an educational tool with hardware having the following specifications: GPIO pins, power source connector, central processing unit (CPU), random access memory (RAM), Xbee socket, GPU, and UART.Raspberry Pi has mass storage using an SD flash memory card. You PC boots into Microsoft windows through the hard disk while an SD memory card helps the Raspbian to boot. Other specifications of the hardware include a US standard keyboard, video cable, power supply cable, monitor, and a microSD card having Linux operating system.Other optional specifications you may need include device case, model A or model B, WiFI adaptor, internet connectivity, USB mouse, and powered USB hub. Use a LAN cable for internet connectivity to the B model.Detailed explanations of all the specs includeThe Central Processing Unit (CPU)The CPU works serves as the brain and hub of your system. It performs instructions in the computer using logical and mathematical functions. Raspberry Pi uses the ARM11 series processor functioning in the capacity of Samsung Galaxy.The Ethernet PortThis port is designed for accessing the internet by plugging your home router. It is the gateway for interacting with other devices.The Graphics Processing Unit (GPU)You can speed up calculating image functions using the GPU. This is a single chip on the board of your Raspberry Pi, and the GPU supports OpenGL. It is also built using a Broadcom video-core IV.General Purpose Input & Output (GPIO) PinsYou can associate and interact with other electronic boards using the GPIO pins. Depending on the way you programmed your Raspberry Pi, these pins can receive and process input and output commands. It can function with digital GPIO pins too. Other electronic units are connected to the Raspbian through these pins.  For instance, you can transmit digital data by connecting the general-purpose input & output pins to the temperature sensor.Raspberry Pi MemoryIf you compare Raspberry Pi to other computer devices, it is a miniature PC. Other standard computers have RAM measured in gigabytes, but the RAM of a Raspbian contains a minimum of 256 MB while the maximum Ram is 512 MB.The Universal Asynchronous Receiver / Transmitter (UART)The UART is a serial input and output port used for transferring serial data like a text. Programmers use it for debugging and converting codes.Display Monitors or TVRaspberry Pi board uses two monitors or television for displaying digital data. These include HDMI and Composite displays. Use a low-cost adaptor with an HDMI male cable to connect several LCD and HD TV monitors.The versions of HDMI supported by your Raspberry Pi are 1.3 and 1.4 using 1.4 cables too. These can help the functions of the video and audio settings of Raspberry Pi. However, it does not support the HDMI l/p adapter. The composite video functions are used for connecting old televisions.In this case, connecting the device to a display unit using a composite video connection can make the audio system functional. Connect the 3.5 mm jack socket and send it to your television. This is possible using a cable that is adjustable for 3.5 mm to double the RCA connection.Power Source Cable or ConnectorYou can power your microcomputer using an external power source. This is a small switch beside the shield.XBee SocketThis feature in the board of a Raspberry pi is used for wireless communication.The Board of Raspberry Pi Model AThe board of model A is designed as a Broadcom (BCM2835) SOC board. This model is made with an ARM1176JZF-Score CPU. It has an SD card of 256 MB RAM with 700 megahertz (MHz).The USB 2.0 ports features external data connectivity, which is an optional tool in the system. The board is powered through a micro-USB adapter. This adapter carries a minimum power range of 2 W.You can also speed up image calculations features using the graphics, which is a special chip in the system.  It is a built-in structure with Broadcom video-core IV cable. This feature is relevant for running a video or game through the Raspberry Pi.The Features of the Board of Model A Raspberry PiThe board of model A Raspberry Pi has unique features such as:

1.  The dimensions of its board are 8.6 cm × 5.4 cm × 1.5 cm.
2.  There is a slot for SD, SDIO, and MMC cards.
3.  The SD card RAM is 256 MB.
4.  The video output is composite featuring RCA (NTSC and PAL), and HDMI with cables versions 1.3 and 1.4.
5.  It comes with an audio output, a 3.5 mm jack, and HDMI.
6.  Its board functions with an operating system called Linux.
7.  It has a full HD multimedia processor with Broadcom BCM2835 SoC.
8.  The 2.0 USB connector is single.
9.  The board has a dual-core video-core IV multimedia coprocessor.

The Board of Model B Raspberry PiThe model B of Raspberry Pi features a board with Broadcom BCM2835 SOC. The board is designed with an SD-RAM of 512 MB and 700 MHz. The CPU core is ARM1176JZF-S. The boars of USB 2.0 port utilize outside data connectivity features.You can only connect with other system through the web in model B using the Ethernet in Raspberry Pi. This system is powered with a micro USB adapter. The minimum range of power needed is 2.5 W.The graphics feature a specialized chip. This is used for speeding up the image calculations. Running a game or video using your system is possible, as it has a built-in Broadcom video-core IV cable. This can help you for streaming a video and playing games.The Features of the Board of Model B Raspberry Pi

1.  It features an HDMI audio output with a 33.5 mm jack.
2.  The system functions with a Linux operating system.
3.  The SD card has a RAM with a memory of 512 MB.
4.  The dimensions are 8.6 cm × 5.4 cm × 1.7 cm.
5.  It functions with a dual-core video-core IV multimedia coprocessor.
6.  Its video output functions with a composite RCA (PAL & NTSC). This includes an HDMI with versions 1.3 and 1.4 cables.
7.  The 2.0 USB connector is single.
8.  The board has 10/100 Ethernet RJ45 jack.
9.  The Broadcom (BCM2835) SoC has a full high-definition multimedia processor.
10.  The board storage has SDIO, SD, and MMC slots.

Functionalities of Raspberry PIRaspberry Pi can be applied in various computerized projects such as controlling robots, internet Radio, carputer, media streaming, Arcade machine, home automation, and a tablet computer. Other projects include cosmic equipment, coffee, and hunting for meteorites.Detailed Explanations of these Projects

1.  Using Raspberry Pi for controlling the Velocity of a DC motor

This project is aimed at using a your Pi device for controlling the speed of DC motor.The equipment you need includes a model of Raspberry Pi, DC motor, LED, capacitors, resistors, and computer monitor or TV. Others are transformer, wiring pi or PHP program, voltage regulator, motor driver IC, and diode.How it WorksYou can regulate the velocity of a DC motor using your Raspberry Pi. The voltage applied for the terminals of a DC motor is comparative to its speed. If there is a varied voltage across the terminals of a motor, the rate will also vary consequently. This is the reason for this project. You can operate the motor at different speeds by connecting it to a keyboard. If you press the key, the system starts functioning immediately.If you want to handle this project, you can program the PWM to cause an output. The output is initiated using wiring pi or PHP. This feature is based on the duty cycle that can cause a change in the average current and voltage of the system.When this happens, it causes the velocity of the DC engine to change.At this stage, you should interface a motor driver IC to the board. This step will cause the board to receive the signals of PWM. THis will also send the required opposite polarity (O/P) to the DC motor. The overturn polarization between the two magnetic fields causes the DC engine to function.

2.  Controlling the auto power of street lights using a Raspberry Pi

The purpose of this task is for students to know the ways of controlling the auto power of street lights.The items needed for this project are diodes, resistors, LEDs, computer monitor or television, and crystal. Other equipment includes MOSFET, transformers, wiring Pi or PHP program, capacitors, and white LEDs.  How it worksThe reason for choosing LED lights is to use them as street lights, and they consume less energy. LED lights have longer life span if compared to other lights. The PWM signals are developed and used for regulating the intensity of lights through a Raspberry Pi. This feature causes a MOSFET to regulate the lights making them attain a desired operational level.This will cause the strength of LED lights to change steadily from dusk to dawn. You will notice this occurrence more during peak period when there will be full intensity. After some time, the heat of the light will gradually reduce. You can achieve a variable voltage across the LEDs using MOSFET switching through pulse width modulation.Other Projects you can do using Raspberry PiThese include

*   Touch screen tablet.
*   Synced music and Christmas lights.
*   Lego Raspberry Pi enclosure.
*   Programmable sequential switching.
*   Controlling Drones

![Drones controlled with Pi.png](Image00004.jpg)Drones Controlled by Raspberry Pi

*   Solar street lights.
*   Wearable computerized devices powered by Raspberry Pi.
*   Autonomous robot arm control through Bluetooth control using Raspberry Pi.

![Controlling Robots.png](Image00005.jpg)Robots controlled by Raspberry Pi

*   Business computerization using Zigbee with Raspberry Pi.

All the Tools Required to Setup Raspberry PI![Tools for Raspberry.png](Image00006.jpg)Tools for Raspberry SetupAll the tools you require to set up your Raspberry Pi technology include Raspberry Pi model, DC motor, SD card, connectivity or display cables, Mouse, power supply, and keyboard. Other optional tools and equipment needed are 3.5 mm jack earphones or headphones and internet connectivity using a WiFi adapter or Ethernet cable.KeyboardUse a standard keyboard or a regular keyboard to input data in your microcomputer.MouseA conventional mouse is also used to input information into the system.SD Card![An SD Card.png](Image00007.jpg)An SD card for Raspberry PiYou should get an 8 GB class of 4 SD cards for your Raspbian. This is already installed with NOOBS. Most times, you can buy an SD card already installed with NOOBS. Another way to get [NOOBS](https://www.raspberrypi.org/downloads/) is by downloading it for free.If you have the foremost Raspberry Pi Model A or Raspberry Pi Model B, you need a full-size SD card. However, the new models of Raspberry Pi model A+ and Raspberry Pi model B+ are designed to use micro SD cards. Other models include model B of Raspberry Pi 2, model B of Raspberry Pi 3, and Raspberry Pi Zero, all function with micro SD cards.Internet ConnectionUse a WiFi adapter or Ethernet cable to connect your device to the internet. With this, you can download software or update an existing one.Power supplyThe optimal power supply required by your Raspberry Pi is at least 5 volts. Apply a 5-volt micro USB power supply to power your device. If you use a power output with a lower voltage, the device will function funnily.Earphones of HeadphonesYour microcomputer functions with earphones or headphones using a 3.5 mm jack.HDMI / DVI Monitor or TelevisionA Raspberry Pi functions with a television or HDMI monitor or DVI monitor as a display unit. If you want more explicit pictures and high-quality images, use a monitor with HDMI input. If you are using older devices, use other connections. An original Ethernet cable is ideal for internet access to the system. Raspberry Pi 3 comes with a integrated wireless LAN.Installing Raspberry PIInstalling Raspbian on your device is easy by following simple guidelines. A Raspberry Pi functions with an operating system called a Raspbian. This originates from the Linux distribution Debian. All Raspberry Pi's hardware functions with the Linux operating system.The Raspbian is a multipurpose and professional operating system that makes your Raspberry Pi device to work well as a computer. It features a browser, command buttons, and several other programs.A Raspberry Pi can function as a home computer since it is a low-cost device with attributes of a PC. It serves as a springboard enabling you to perform other tasks and projects seamlessly. You can use it as wireless access points or play exciting video games.Installing Raspbian on a Raspberry PiInstalling Raspbian is a natural process. You will use a microSD card and write the disc image after [downloading](https://www.raspberrypi.org/downloads/) the Raspbian. Get an 8 GB microSD card, a PC with an opening for SD cards, a mouse, keyboard, power, and a Raspberry Pi, as stated above.What is NOOBS?![Download Noobs.png](Image00008.jpg)NOOBS Installation ManagerNOOBS is an installation manager for operating systems. It is another option for installing Raspbian on your Pi device. Some SD cards are pre-loaded with NOOBs making it easier to install Raspbian to your Raspberry. If it is not pre-installed, you can [download NOOBS](https://www.raspberrypi.org/downloads/) to your SD card before using it to download Raspberry Pi.Method 1Download Raspbian OS![Raspberry Pi Installer.png](Image00009.jpg)Raspberry Pi InstallerThe first method for installing Raspberry Pi is downloading the [Raspbian](https://www.raspberrypi.org/downloads/raspberry-pi-os/) disc image. This is the current version of the operating software in a Raspberry Pi. You can download the Raspbian disc image using a PC or Mac computer.                                          This process may take some time with the traditional download feature. You can also use the torrent, although this could take up to an hour to download to your system. But wait for it.Method 2Unzip the Compressed FileAfter downloading, the next step is to unzip the File. It exists with the ZIP64 format. However, this depends on how the built-in features in your system are. If they are updated and current, you can use any program to unzip the File.Some programs for unzipping files in a Raspberry Pi include

1.  [Unzip](http://unarchiver.c3.cx/unarchiver) for persons using the Linux operating system.
2.  The [Unarchiver](http://unarchiver.c3.cx/unarchiver) for Mac users.
3.  [7-Zip](http://www.7-zip.org/) for programmers using windows software.

Method 3Use a MicroSD Card and Write the Disc Image![Micro SD card.png](Image00010.jpg)MicroSD CardPut your microSD card into your system and write the disc image to it. This may demand some programs such as:

1.  Etcher for those using the Linux OS in their devices. This program is recommended by the Raspberry Pi Foundation.
2.  Win32 Disk Imager suitable for programmers using windows operating system.
3.  Users with Mac devices can utilize the program already installed in the system for writing the disc image.

It could take different processes to write the disc image to the card on those devices. But the procedures are self-explanatory and easy to understand. During the writing process, you will be requested to choose a destination in your system, select the microSD card. For the disc image, select the "Unzipped Raspbian file." Click on double-check. After this, tap the icon and write the image to your microSD card.With this process, the disc image will be written to the card.Method 4Boot up Your Raspberry Pi after Inserting the microSD CardThe final stage is to insert the SD card into your device and boot your device. Remember to plug in the power source and the peripherals. If you have updated your device to the current edition of Raspbian, this will display on the desktop of your Raspberry Pi.Apply the default username and password.Username: piPassword: RaspberryAfterward, you can change to your username and password.![Change name.png](Image00011.jpg)Change Name and PasswordThe ConnectionsAs I stated earlier, a Raspberry Pi is already equipped with a microSD card slot. Inserting an SD card into the slot is easy since it is the primary storage space in a Raspberry Pi board. Its function is the same as a hard disc in any computer device.The operating system is Linux OS, which is loaded onto the SD card. This operating system is bootable after plugging the Pi into a power source. A Raspberry Pi supports Linux OS, Mac, ARM, and Qtonpi operating systems.You can select any of these operating systems for your Raspberry Pi device. Then, you can use a disk manager application and write it to an SD card. Other external storage systems include a USB drive or a USB external hard drive.Different sizes and brands of SD cards are available on the market. However, your Raspberry Pi can contain an SD card with a maximum storage capacity of 64 GB.The connections that can make your Raspberry Pi functional include a monitor or TV, Mouse, and keyboard.  Various output channels are needed for the display unit. These include composite video, DSI video, and HDMI video. However, the DSI video output needs specific hardware to function.The SD card is an essential component of a Raspberry pi board. Most times, they may sell a Raspberry Pi board with or without an SD card. It is used for storing files, documents, and other programs in this microcomputer.If you purchase a Raspberry pi board without an SD card, then you should buy a minimum of 4 GB for your device. But it can contain a total of 8 GB. With this system; you can manage web traffic properly. It also functions as a typical computer with a low-cost server, although smaller in size.CHAPTER TWOBASIC PROGRAMS IN PYTHONPython is a multipurpose, high-level, and interpreted programming language that was developed and released in 1991 by Guido van Rossum. The design philosophy embraces code readability and remarkable for using meaningful whitespace. The language is well-constructed and objects oriented in its approach. It is aimed at helping programmers to write clear and understandable codes for large-scale projects, including small-scale tasks.Python encourages multiple programming features, such as functional programming and structured programming. It is garbage collected and dynamically typed. Python has a comprehensive and standard library. It is also described as batteries included in its unique features.This programming concept was create and introduced in the 1980s. It became the follower of the ABC language. List comprehensions and garbage collections are features of python 2.0\. This program was released in 2000 with reference counting. Also, Python 3.0 was released in 2008. This was a review and amendment of the language, although not backward compatible. It is good to note that Python 2 codes cannot run on Python 3 in unmodified format.The language of Python 2 was planned and initiated for 2015 but discontinued in 2020\. Python 2.7.18 is the last Python 2.7 to be released. It is the last Python 2 programs that will be issued. There shall be no improvements or security patches to be released for it. Since Python 2 has ended, Python 3.5.x and others are supported.Different operating systems have Python interpreters. A community of programmers called Python Software Foundation directs and manages resources for CPython and Python development. Python is a free source for a reference implementation. It is developed and maintained this group of programmers.Varieties of basic Python programs abound on many topics such as basic python programming, functions, types of native data, and conditions and loops.Basic Python ProgramsBasic programs in Python include

1.  Python program for showing calendar.
2.  Python program for converting kilometers to miles.
3.  Python program for arithmetical operations.
4.  Python program for converting Celsius to Fahrenheit.
5.  Python program for swapping two variables.
6.  Python program for printing "Hello Python."
7.  Python program for solving a quadratic equation.
8.  Python program for determining the area of a triangle.
9.  Python program for generating a random number.

Python Programs for Functions

1.  Python program for converting decimal to binary, octal, hexadecimal.
2.  Python program for determining HCF.
3.  Python program for calculating LCM.
4.  Python program for making a simple calculator.
5.  Python program for displaying the calendar.
6.  Python program for determining the factorial of a numeral using recursion.
7.  Python program for determining the ASCII value of a character.
8.  Python program for displaying Fibonacci series through recursion.

Python Programs for Numbers

1.  Python program for checking if the given number is Happy Number.
2.  Python program for determining if a specific number is a Harshad Number.
3.  Python program for printing all pronic figures between 1 and 100.
4.  Python program for printing all happy numerals between 1 to 100.
5.  Python program for checking if the particular number is a Disarium Number.
6.  Python program for printing every disarium digit between 1 and 100.

Python Programs for Array

1.  Python program for printing the sum of all elements in an array.
2.  Python program for printing the smallest element in an array.
3.  Python program for printing the factors of an array present on odd positions.
4.  Python program for printing the number of factors present in an array.
5.  Python program for printing the biggest factor in an array.
6.  Python program for printing the elements of an array present in an even position.
7.  Python program for printing the factors of an array in reverse order.
8.  Python program for printing the duplicate factors of an array.
9.  Python program for printing the elements of an array.
10.  Python program for sorting the digits of an array in descending order.
11.  Python program for rotating the strings of an array to the right-side.
12.  Python program for sorting the numbers of an array in ascending order.
13.  Python program for copying all elements of one array into another array.
14.  Python program for rotating the elements of an array to the left-side.
15.  Python program for calculating the frequency of each element in the array.

Python Programs for Circular Linked List

1.  Python program for removing a node from the starting of the circular linked list.
2.  Python program for deleting a node from the end of the circular linked list.
3.  Python program for erasing a number from the center of the circular linked list.
4.  Python program for tracing the minimum and maximum value node from a circular linked list.
5.  Python program for creating a rounded linked list of N nodes and counting the number of nodes.
6.  Python program for creating and displaying a circular linked list.
7.  Python program for creating a rounded linked list of n nodes and displaying it in reverse order.
8.  Python program for organizing the factors of the circular linked list.
9.  Python program for removing duplicate elements from a circular linked list.
10.  Python program for searching a figure in a circular linked list.
11.  Python program for inserting a fresh node in the center of the circular linked list.
12.  Python program for inserting a current node at the finishing of the circular linked list.
13.  Python program for inserting a current node at the starting of the circular linked list.

Python Programs for Doubly Linked List

1.  Python program for inserting a current node at the starting of the doubly linked list.
2.  Python program for inserting a new node in the center of a doubly linked list.
3.  Python program for inserting a new node at the finishing of a doubly linked list.
4.  Python program for deleting a current node from the starting of the doubly linked list.
5.  Python program for deleting a new node from the center of the doubly linked list.
6.  Python program for deleting a new node from the end of the doubly linked list.
7.  Python program for converting a specific binary tree to a doubly-linked list.
8.  Python program for determining the minimum and maximum value node from a doubly linked list.
9.  Python program for creating a doubly-linked list from a ternary list.
10.  Python program for creating a doubly-linked list of n nodes by counting the frequency of nodes.
11.  Python program for creating and displaying an extra linked list.
12.  Python program for creating a doubly-linked list of n nodes and displaying them in reverse order.
13.  Python program for searching an element in a doubly-linked list.
14.  Python program for removing duplicate elements from a doubly linked list.
15.  Python program for rotating extra linked list by N nodes.

Python for Native Data Type Programs

*   Python program for transposing a matrix.
*   Python program for removing punctuation from a string.
*   Python program for adding two matrices.
*   Python program for sorting words in alphabetical order.
*   Python programs for multiplying two matrices.

Python Programs for Conditions and Loops

*   Python program for checking leap year.
*   Python program for checking Armstrong's number.
*   Python program for determining Armstrong's figures in an interval.
*   Python program for calculating the total of natural numbers.
*   Python program for checking prime numbers.
*   Python program for checking whether a figure is positive, negative, or zero.
*   Python program for if a number is odd or even.
*   Python program for printing the Fibonacci sequence.
*   Python program for displaying a multiplication table.
*   Python program for calculating the factorial of a number.
*   Python program for printing all prime numerals in an interval.

The Versions of Python and their Release Dates

| S/N | The Versions of Python | Release Dates |
| 1. | Python 1.0 | January 1994 |
| 2. | Python 1.5 | December 31st , 1997 |
| 3. | Python 1.5.2 | April 1999 |
| 4. | Python 1.6 | September 5th , 2000 |
| 5. | Python 2.0 | October 16th , 2000 |
| 6. | Python 2.0.1 | June 22nd , 2001 |
| 7. | Python 2.1 | April 17th , 2001 |
| 8. | Python 2.2 | December 21st , 2001 |
| 9. | Python 2.3 | July 29th, 2003 |
| 10. | Python 2.4 | November 30th , 2004 |
| 11. | Python 2.5 | September 19th , 2006 |
| 12. | Python 2.6 | October 1st , 2008 |
| 13. | Python 2.7 | July 3rd , 2010 |
| 14. | Python 3.0 | December 3rd , 2008 |
| 15. | Python 3.1 | June 27th , 2009 |
| 16. | Python 3.2 | February 20th , 2011 |
| 17. | Python 3.3 | September 29th , 2012 |
| 18. | Python 3.4 | March 16th , 2014 |
| 19. | Python 3.5 | September 13th , 2015 |
| 20. | Python 3.6 | December 23rd , 2016 |
| 21. | Python 3.7 | June 27th , 2018 |
| 22. | Python 3.8 | October 14th, 2019 |

Current Versions of Python Programs, which are final releases of the versions and their release dates include

| S/N | The Versions of Python | Release Date |
| 1. | Python 2.4.6 | December 19th , 2008 |
| 2. | Python 2.5.6 | May 26th , 2011 |
| 3. | Python 2.6.9 | October 29th , 2013 |
| 4. | Python 2.7.10 | May 23rd , 2015 |
| 5. | Python 2.7.13 | December 17th , 2016 |
| 6 | Python 3.5.3 | January 17th , 2017 |
| 7. | Python 3.6.10 | December 18th , 2019 |
| 8. | Python 3.8.2 | February 24th , 2020 |

..How to Run PythonPython is a great and valuable language for your Pi device. Installing and running it on the hardware together with GPIO pins are smooth processes. The Raspbian can accommodate python programs.Requirements for Running Python Programs on a Raspberry PiThe requirements for running python programs on your device include

1.  HDMI monitor or TV.
2.  Raspberry Pi device.
3.  Mouse and keyboard.
4.  Raspbian Operating System on an SD card.

Details about Python LibrariesA python program may need external libraries before it can work on a Raspbian. Therefore, you need to install extra libraries using PIP, which can only install libraries for programs in the terminal window. PIP is a package or module manager for Python. A good reason for this is that Python IDE programs come with a local copy of Python. Using the terminal window for running programs is recommended since it functions with external libraries installed using the preferred installer program (PIP). However, PIP is built-in by default into python packages with versions 3.4 or later versions.Python programs are installed through a terminal, IDE, or Thonny.Running Python Programs Using TerminalPython programs are also run using a terminal window. But you should understand the way to the program before opening the terminal. You can locate the program following this method:Go to Documents > Python > Main.py.After this, open the window and apply the cd command. This can help you to change the working directory to another directory containing Python program such as:cd Documents/PythonSuppose you want to check whether your Python program is in the catalog. You can use the command dir. This will also list all files and folders within that directory. If the application is not contained in the archives, you must go back and find where the program is located in the catalog.Now, let us use the Python command and execute this Python program. It will run the Python file stated after the command. For example:Python yourfilename.pyAnother method is to check if your File has spaces such as:Python your File name.pyRunning Python Programs through IDEThe Operating System of your Raspberry Pi comes with several IDEs useful for programming. One of the IDEs in your Raspbian is the original Python IDE. You can open this by opening the Raspbian logo. Then, scroll to Programming and click on Python 3 (IDLE)After loading the IDE, click on File > Open. If the File opens, navigate to the Python program. Then, Run the program. Simply tap Run button and click Run Module. Another way is to go to the keyboard and press F5. Running Python Program Using ThonnyAnother necessary Python IDE with several features is Thonny. With this debugger, you can watch variables and step through codes. It could also be applied for running Python programs by following these methods:Navigate to the logo of Raspbian and click it. Scroll down to find Programming and tap on Thonny Python IDE.After this process, click on the File menu. Locate and click the Open button and scroll to the program. If the program has downloaded, tap on the Run button to Run the present file.Python ShellThis interprets languages in Python and used for executing the code serially. Python shell is also called Python Interactive Shell for executing one Python command and getting results.Python shell gets a command from the user. If the programmer types the prompt, the program will execute it and display the result.If you are using windows, open the Python shell by typing Python . Then, press Enter.After this, you will see three symbols of Greater than (>>>). Enter a single statement, and the result will appear if you enter an expression like 5 + 3, and press Enter. The result will show on another line below it.Executing Python Script with Python ShellPython shell is applied for executing a single statement. However, running multiple statements requires you to create a Python file using the extension .py. Then, write Python scripts in various statements.Another way to handle this is by using Notepad and a statement such as:lookatPythonScript.pyprint – "Look at Python Script."print – "Receive Python lessons from the Teacher."You can save this as myPythonScript.py . Then, navigate the command button and scroll to the folder to save this File. This process can help you to apply the Python lookatPythonScript.py command.Python Shell could be applied for executing Python languages and commands.LoopsIn any programming language, the flow of programs is sequential by default. In most cases, you can alter the sequence of programs. But, executing a particular code could be done repeatedly.Programming languages offer several types of loops that can repeat some specific codes many times.Reasons for Using Loops in PythonOne of the reasons for using loops is that it helps in simplifying complex problems. Python loops enable you to alter or modify the sequence of programs. With this, instead of rewriting a particular code uncountable time, you can repeat it predetermined or fixed number of times.In this case, for printing a number ten times, no need to apply the print statement ten times. Simply print inside a loop. The loop can run up to ten repetitions or iterations.Benefits of Using Python LoopsUsing loops in Python programs come with various benefits such as:

*   Loops help a programmer to reuse codes.
*   If you are using python loops, you don't have to rewrite a specific code uncountable times.
*   Python loops enable a user to traverse over the elements of data structures such as linked lists or array.

Different Loop Statements in Python Programs

| S/N | Python Loop Statement | Description of Codes |
| 1. | Post tested loop or Do-while loop. | Until a specific order is reached, the do-while loop continues. In a programming language, it is called a post-tested loop. This statement is applied when you can perform the function at least once. Also, it is used for menu-driven programs. |
| 2. | Pre-tested loop or While loop | Without knowing the number of repetitions or iterations in advance, you can apply the while loop for that scenario. In the while loop, a block of expressions are executed until the specified condition is satisfied in that loop. This type of loop is called the pre-tested loop. |
| 3. | Per-tested loop or For loop | A per-tested loop is applied for executing some part of the circle until the specific condition is met. This is also called 'for a loop.' This loop statement is the right choice where the number of repetitions or iterations is determined in advance. |

IDLE and EditorIn Python language, IDLE or IDE means Integrated Development Environment. Also, you can refer to it as Python IDLE editor. Beginners use this tool in programming until they acquire more experience. Professional programmers use Komodo or Eclipse, which are more reliable and better programs than IDLE.Python IDLE is a GUI for developing Python programs. During Python installations, the GUI could be installed automatically. In a straightforward GUI environment, it helps you for running, debugging, and editing Python programs. IDE automates the process of compiling, editing, and testing in an SLDC.IDLE can build its windows using the standard library's Tkinter GUI toolkit. It is a multipurpose software that can run on several platforms such as Mac, Linux, Windows Operating System, and more.Features of IDLE

1.  It functions as an integrated bugger.
2.  IDLE helps in syntax colorization and command history.
3.  This feature supports multiple windows.
4.  Relevant for unindent or auto-indent for Python codes.
5.  Word auto-completion process.

In Microsoft word, such as windows 7 or windows 8, Python IDLE functions effectively. You could see it at the Start Button Menu in Windows 7, as an Entry. In Windows 8, go to the Start Menu and type IDLE. This can help you for running it in the system. Immediately, it will show the details of the OS and Python version in the device.The code should be written after this prompt >>> on your windows. After pressing on the Enter button, the program will be executed. One-line commands are executed using shell windows. But, this is not applied for writing full-fledged programs.Python IDLE has a built-in text editor. It is useful for writing and saving your codes. Editors begin to function if you click on File > New File. This command opens a window for typing your code.But saving this code in a box file before running it is ideal. Simply click on File, then Save. However, ensure that the data has a .py extension.Running the code requires you tap on the Run button. This will take you to the Run Module . You can simply press F5\. The result of this program will be printed on the window bearing IDLE. The result will show below the Restart line.Types of Python IDEsDifferent types of Python IDEs that could be used in software development are Atom, Thonny, Eric, Rodeo, Spyder, PyCharm, Wing, Microsoft Visual Studio, Jupyter Notebook, and PyDev.Atom IDEAtom IDE was built by GitHub as an open-source cross-platform. This framework uses an electron that enhances cross-platform desktop applications. The platform functions with Node.js and Chromium, which are presently known as Hackable Text Editor.The Features of this Integrated Development Environment includei. Viewing outputs on Atom doesn’t require opening another window.ii. Atom features built-in support for viewing and editing Markdown files using a plugin called Markdown Preview Plus .Thonny IDELearning or teaching programming languages demands you to use Thonny IDE. Tartu University built this software. It is useful for highlighting syntax errors and supporting code completion processes. Some of the features of this IDE include

1.  Useful auto code completion and highlighting errors.
2.  It serves as a simple debugger.

Eric IDEEric IDE is a program developed by Python as an editor. It is valuable for professional programmers and amateurs.The features of this software include

1.  Task management support with built-in bugger.
2.  They are used as source code folding, editors, and configurable window layout.
3.  Eric is used for version control and advanced project management.

Rodeo IDERetrieving data and information from various sources is possible using Rodeo Integrated Development Environment. It is regarded as an ideal IDE for programs. This software is used for the auto-completion of codes and supports cross-platform functionalities.The features of this program include

1.  Syntax highlighting, auto code completion, and visual file navigation.
2.  Enhances your skills for plotting, interacting, inspecting, and comparing data.

Spyder IDESpyder is ideal for data science with an open-source and highly recognizable in the IDE market. It means the Scientific Python Development Environment (Spyder). This program accepts and functions on all relevant platforms such as MacOS X, Windows, and Linux Operating System.Spyder IDE offers various functionalities such as document viewer, integrated console, localized code editor, and variable explorer. Other scientific modules, such as SciPy, NumPy, etc. are supported by this IDE.The various features of this program include:

1.  Secure integration with the IPython console.
2.  Functions correctly in automatic code completion mode and multi-language editor.
3.  It offers a better auto code completion with syntax highlighting features.

PyCharm IDEPyCharm was built by the Jet Brains as software for Python with a cross-platform for Integrated Development Environment (IDE). This IDE is available in a free version and paid (PRO) version, and it is the most widely used open-source program. It helps developers and programmers take care of regular tasks.PyCharm is a full-fledged IDE with fast error checking and correction, database accessibility, auto code completion, quick project navigation, and remote development support.The features of this program include

1.  It helps in highlighting errors.
2.  Enhances Python web development frameworks such as Javascript, Angular JS, etc.
3.  PyCharm functions as a powerful debugger.
4.  It is valuable for smart code navigation.

Wing IDEWing IDE is packed with decent and necessary development support features. This cross-platform offer free edition for beginners, although it has a Pro version that has 30 days trial. This will enable learners and experienced programmers to try it out.This IDE program offers services such as debugging, auto-completion, syntax highlighting, and indents.The main features of the Wing IDE is that

1.  The wing is customizable with extensions.
2.  This IDE enhances remote development and test-driven development together with the unit test.

Microsoft Visual Studio IDENow, you can develop and debug the latest cloud or web projects using Microsoft Visual Studio. It is an open-source code editor with a marketplace for extensions.The features include

1.  Valuable for coding programs in Visual studio.
2.  It could be found in a free and PRO versions.

Jupyter Notebook IDEIn the Data Science industry, Jupyter Notebook is a frequently used IPython notebook editor. You can use it for crafting and operating notebook documents. This web resource is developed on the server-client structure since Python is an interpreted language.Some of the features of this IDE include

1.  Jupyter Notebook is necessary and suitable for beginners in data science.
2.  It is useful for markdowns.
3.  This IDE is valuable for creating and editing codes.

PyDev IDEPyDev IDE is an outside plugin for Eclipse and a commonly used program in Python. If you have experience in Java, it is usually a natural choice for Python developers with this background. Most programmers know it as a Python interpreter.In the years 2003 and 2004, Aleksander Totic is renowned for his contribution to the Mosaic browser. He also worked on the Pydev project during this period. It is an integration of Django, auto code completion, block indents, and smart indents.The features of this IDE include

1.  PyDev supports black formatter, Mypy, and virtual environments.
2.  It has reliable parameters such as debugging, code average functionalities, code analysis, and refactoring.
3.  It is suitable Unit test integration, PyLint integration, and remote debugger.

Numbers and VariablesNumbers and variables in Python refer to numerical variables.Python NumbersIn Python, digits are stored as floating-point values, integers, and complex numbers. This also depends on the requirements of the program. There are two types, which are floating-point values and integer.Python VariablesA variable refers to the position of memory in the system and as an identifier used for holding values. Python is an inferred language and doesn't need specifying types of variables.Variables are groups of letters and digits (numbers). However, they start with a note or an underscore. In writing variables, you can use lower case letters for names of variables such as John and john are two separate variables.Types of Numerical VariablesTwo kinds of numerical variables are available.IntegersIntegers are numerical values consisting of whole numbers such as 1, 2, 3, 10, 20, 100, 2000, 50,000, 1000000, 10,000,000, etc. You apply this variable in Python by writing any whole number, as shown above.ExamplesThe expression x = 2 means that the integer number 2 will be stored in the variable x. X is the variable, and 2 is the number, hence the tag' numerical variables'.  If you are using 64-bit systems, you can store whole numbers between the values of 4000338912344092341 and 4000338912344092340 in an integer variable Python platform.Floating-Point ValuesFloating-point values are Python numbers with decimal points. Any number written with a decimal part is identified as a floating-point value.Therefore, a term like x = 6.5 means that the floating-point value (6.5) is stored in the variable x. Moreover, vast numbers could be stored in this way, such as 3.2250738585072015 × 10308 to 2\. 7976931348623157 × 10308.Integer numbers could be converted to floating numbers using the float number functionality. For example,

| X = 6Print (x)Print  ( float (x) ) |

If this expression is executed, the code can produce an output such as:

| >>>55.0>>> |

However, you can convert a floating-point value to an integer number by using the integer-number functionality. Look at what will happen by dividing two integer numbers:

| >>>  x = 5>>>  y = 2>>>  z = x / y>>>  print  (z)2.5>>> |

In the expression above, numerical (numbers) are defined as integers (whole numbers). The result of this operation was a floating-point number. It is a Python 3.x feature – Python 2.x that would operate integer division and return the result of 2.Variables Used for Identifier NamingVariables are applied for identifier naming. Programmers use it for identifying literals in the program. Here are various ways to name an identifier in an expression.

1.  There should be no whitespace and special characters in an identifier name. Examples of such characters include #, ^, %, =, !, &, etc.
2.  In Python, identifier names are case sensitive. That means my book' and 'MyBook' is not the same expression.
3.  Valid identifiers in a statement include n_9, _n, a123, and so on.
4.  Invalid identifiers in a statement include n 9, n%4, 1a, and so on.
5.  The names of an identifier must be similar to the keywords expressed in the language.
6.  The variable must begin with characters such as an underscore ( _ ) or an alphabet.
7.  In a Python statement, every letter except the first character could be an alphabet of an upper case such as A, B, C, D, …, or a lower case such as a, b, c, d, …. It could also be a digit such as 1, 2, 3, 4, … or an underscore ( _ ).

How to Declare Variables and Assign ValuesYou don't have to declare variables before applying them in the program. Python enables you to form a variable at the right time when they are needed in an expression.Variables are defined and declared immediately and automatically by assigning a value them. Use the sign (=), 'equals' in a statement to declare a variable. This mark assigns rates to variables.How to Reference Objects in PythonAs a programmer, you need to understand how to reference objects in Python. This defines the way Python interpreter functions as you declare a variable. The way you handle variables is different from other programming languages.Experience programmers understand that Python features as a highly object-oriented programming language. Therefore, all data items belong to a particular type of class. For example:

| Print ("James") |

Output:

| James |

An integer is created by the Python object and highlights it to the console. I created a string object in the above print statement.Another way to determine this is using the built-in type ( ) functionality . For example:

| Type ("James") |

Output:

| < class  ‘str’ > |

In Python programs, variables are classified as symbolic names functioning as pointers or references to objects in a statement. The variables are used to assign names to objects. For example:

| b = 20 |

![](Image00012.jpg) b            20Therefore, "b" in the above image represents "20", which is an integer object. I can also assign the integer value (20) to a new variable, such as "c." The expression will become

| b = 20c = b |

![](Image00013.jpg) ![](Image00014.jpg) b                 20                      cIn this expression, the variable b is referring to a specific object that c is pointing. The reason is that Python doesn’t build separate objects for variables. It is what you put in that will be represented.But assigning a new value to c means that both variables will refer to different objects. For example:

| b = 20c = 30 |

In this expression,![](Image00012.jpg) b            20![](Image00015.jpg) c             30Python software is designed to manage memories properly. Therefore, assigning similar variables to two different values is possible.How to Create Object Identity in PythonEvery created object in Python is unique and identifiable. Therefore, no two objects will be represented by the same identifier. There is a built-in identifier functionality Id ( ) function that could be used to identify the object identifier.Look at this example:

| b = 20c = bprint (id(b))print (id(c))# Reassigned variable bb = 500print (id(b)) |

Output:

| 14073498291168140734982911682822056960944 |

I assigned the c = b, b, and c are pointing to the same object. If we examined according to the id ( ) functionality, it returned the same number. I assigned b to 500, and it referred to the new object identifier.How to Determine the Names of VariablesI have explained the ways to ascertain valid and invalid variables. Variable names can come in various lengths. They could have lower case characters (a, b, c, etc.) and upper case characters such as (A, B, C, etc.). Other elements in the names of variables include underscore ( _ ) and digits (1, 2, 3, etc.).Find below examples of valid variable names:

| name = “Devansh”age = 25marks = 90.50print(name)print(age)print(marks) |

Output:

| Devansh2590.5 |

Consider other valid variable names such as

| name = “A”Name = “B”name = “C”NAME = “D”n-a-m-e = “E”_name  = “F”name_ =  “G”_name_ = “H”Na56me = “I”print (name, Name, naMe, NAME, n-a-m-e, NAME, n_a_m_e, name_, _name, na56me) |

Output:

| A B C D E D E F G F I |

In the previous example, I have categorized some variable names, such as _name_. NAME, _name, name, etc. These codes may confuse if a beginner tries to read them. Therefore, they are not recommended except the programmer defines and describes them accurately to make them more readable and understandable.However, you can create multi-word keywords using the following methods:

1.  Snake Case

Categorizing your keywords using the snake case method ensures that the words are marked separately by the underscore ( _ ) sign. For example, name_of_learner, name_of_the-developer, etc.

2.  Camel Case

In this method, each abbreviation or word in the center of a statement begins with a capital letter. There is no whitespace among the words. Examples of codes in a camel case include nameOfLearner, valueOfVariable, etc.

3.  Pascal Case

In this method, the first word begins with a capital letter. An example is NameOfLearner.How to Create Multiple AssignmentsIn Python programs, you can assign multiple variables value in one statement. It is regarded as multiple assignments.These could be expressed in two ways, such as assigning a single value to multiple variables and conveying multiple values to multiple variables.Here are few examples:Assigning a Single Factor to Multiple Variables

| a=b=c=30print(a)print(b)print(c) |

Output:

| 303030 |

Assigning Multiple Factors to Multiple Variables

| x,y,z=20,25,30print xprint yprint z |

Output:

| 202530 |

In Python programs, values are assigned in the order and manner the variables occur in a statement.Some fundamentals, a beginner, should take note of in Python include comments and tokens with their different types in programs.Tokens are reserved words, punctuation marks, and other expressions in words. The smallest unit of letters in a particular program is called tokens. Examples of tokens in programming language include identifiers, literals, operators, and keywords.Simulating Dice![Example of a Simulating Dice.png](Image00016.jpg)An Example of a Simulating DiceThis section is meant for beginners in Python to teach them how to make a common dice roll simulator. You will also learn how to repeat dice rolls. With this lesson, you will learn the methods of setting the lowest and highest values of the dice.Here are some critical steps to follow in handling a simulating dice.Print or Output Random Figures from 1 and 6It is good, to begin with, a central program to output an arbitrary integer from one and six. This is for a simple dice roll. This could be done using the casual integrated library in Python. With this, you can also produce a casual variable using the radint () feature in the library.There is a random import code at the start of the program to use and import the random library. You cannot use this collection without importing it. Therefore, import this library from the program before proceeding.Next is to set the minimum and maximum values of the casual figure from one and six. The lowest and highest values will be stored using these variables. You can modify these values if you add on to the codes.Generating random variables is easy using the radint () functionality in the library. The smallest and largest values become the parameters that the radint () method uses in generating values randomly. It will then produce a casual figure between the smallest and largest values.How to Install the Application InitiallyNow, whenever you run the program, the code will print out a random variable from one to six. That means if you operate the application five times, the output could appear like this:

| 53611 |

However, don't forget that every runtime is a casual output. If you run the code, the output will be different. Before running the program, ensure that you store the letters as dice_roll.py . Then, go to the terminal and use this command: python3 dice_roll.py. This will help you to install the software in the programming area.Whenever you install the program, hit the up arrow, and enter the terminal. If you're going to get the output, as shown above, you have to operate the program up to five times.Request for a Second Dice Roll from the UserYou can get the user's input through the input () function. At this stage, the user will be asked this: "Want to spin the dice again?" The expected answer here is 'yes.' If not, it should be 'no.'The user's input will be stored in a variable. This answer helps you to get support for his information, which will be 'y' or yes. If you want other variations of the data, you can get more help to do that.A while loop runs while the assessment of a variable is true. This variable will be called again by the users of the program. You begin by fixing the value of back to true. With this, you can have a while loop having the setting again.You can publish a random dice roll to the monitor inside the while loop. Now, you can request another dice roll from the user. This helps you in altering the value of again to ‘Not true’ if the programmer won’t reiterate a dice roll.You can even evaluate if the input is 'y' or 'yes' using an 'if statement.' If this expression is true, then 'again' must be True. If it is not valid, you should change 'again' to False .Remember, the code for this program is dice_roll.pyRunning the Program a Second TimeWith this command: python3 dice_roll.py, you will operate the game a second time. Immediately, a hit and miss dice roll will be given to you. You will be asked if you desire to roll the dice secondly. If you enter 'y,' you will get a second dice roll. But if you enter 'No' or another text, instead of 'y' or 'yes,' the program quits or ends.Request for Minimum and Maximum Dice ValuesRequesting for the lowest and highest values of dice is a way to improve the program. A die comes with many sides. Even some dice could have 120 sides. Simulating a dice roll using a die having many sides, you can type the smallest and biggest digit for the die.Some dies can have a low number like1\. But you can ask for the smallest and biggest values to generalize the program. At the starting of the code, you can request for an input from the user. Then, you can convert the data to an integer before proceeding.What Happens when an invalid input is typed? When a user enters an invalid input, which is not a number. The program quits or ends. Then, a Traceback error will appear.For instance, someone types in a text such as 'hi' instead of typing the minimum value. The input function cannot convert the word 'hi' to an integer. It will only throw an error and quit the program.Improve your Dealing with an InputDoing a second dice roll helps you to improve the input. You only need to add the input 'y' or 'yes,' which is the acceptable word. This data could be converted to a lower case before checking the input. Then, you will have 'YES,' 'Y,' or Yes, which are valid in the program. In case you don't want to change the again variable, use the break or continue commands. This enables you to continue into the second iteration or break the loop.When the user handles a second dice roll, you can go to the second iterating loop using the continue command. If the programmer or user doesn't want to roll a second dice, the break command is executed. This will cause the program to end as it will come out of the loop. How to Improve Error Handling Using Try and Except MethodAt the starting of the program, the user can enter an invalid minimum or maximum value. This will cause the application to display an error and quit.The error could be handled using this method. You can output an 'input invalid program that will revert to default program.' Then, you should set the lowest and highest values to a default of 1 and 6. The player will be requested to enter a low and high value inside the try block. A display of error in any of these values will not execute the block of code. There will be a print statement from the except block of code. This will come as a customized error message that can help you to set the smallest and biggest values of the dice to default values of one and six.This feature can help you to improve the error handling of the code slightly. You can add more support for handling errors with these blocks of code.There are many ways of doing the dice simulator. It depends on the type you choose and your experience as a programmer. But you can add up a few things to enhance your experience. Adding more support for input and using a GUI can boost your expertise in handling the dice simulator in Python.CHAPTER THREEWHAT ARE DICTIONARIES, LISTS, AND STRINGS?There are some built-in structures in Python. These include dictionaries, lists, strings, and other structures. DictionariesDictionaries in Python are used for storing data in a key-value pair format. They are the data type that can simulate real-life data arrangement in Python. In this case, some peculiar values exist for some specific keys. This data structure is mutable. But dictionaries are expressed as values and element keys.ValuesIn Python, values are expressed as lists, integers, tuples, etc.Element KeysElement keys are defined as single element keys.A dictionary is the collection of key-value pairs, which can be any Python object. But the keys are immutable Python objects such as strings, tuples, and numbers.How to Create DictionariesYou can create dictionaries using key-value pairs that are enclosed with curly brackets such as these {}. Each key in the dictionary is separated from the figures using a colon (:).Here is the syntax to define the dictionary below:

| Dict = {“Name”: “John”, “Age”: 30 |

In this expression, you will see the dictionary Dict; the keys Name and Age are the strings known as immutable objects.Create a dictionary and print its content. Look at this example:

| Employee = {"Name": "Thompson", "Age", 40, "salary": 35000, "Company": "GOOGLE"}print(type(Employee))print("printing Employee data … ")print(Employee) |

Output

| <class 'dict'>Printing Employee data ….{‘Name’ : ‘Thompson’, ‘Age’ : 40, ‘salary’ : 35000, ‘Company’ : ‘GOOGLE’} |

Python offers built-in function dict( ) method. This feature is used for creating a dictionary. The curly braces {} with no value or object are used for generating an blank dictionary.

| # Creating an empty DictionaryDict = {}print(“Empty Dictionary: “)print(Dict)# Creating a Dictionary# with dict() methodDict = dict({1: ‘Java’, 2: ‘T’, 3:’Point’})print(“\nCreate Dictionary by using dict(): “)print(Dict)# Creating a Dictionary# with each item as a PairDict = ([(1, ‘Devansh’), (2, ‘Sharma’)])print("\nDictionary with each item as a pair: ")print(Dict) |

Output:

| Empty Dictionary:{}Create Dictionary by using dict( ):{1: ‘Java’ 2: ‘T’, 3: ‘Point’}Dictionary with each item as a pair:{1: 'Devansh', 2: 'Sharma'} |

How to Access the Values of DictionariesEarlier in this chapter, we have discussed the way to access lists and tuples using indexing features. But you can access the values in the dictionary using keys because these keys are peculiar in the dictionary of Python programs.The values of a glossary are accessed through the following steps.

| Employee = {“Name”:  “James”, “Age”: 25. “salary”:28000,”Company”:”GOOGLE”}print(type(Employee))print(“printing Employee data ….”)print(“Name : %s” %Employee[“Name”])print(“Age : %d” %Employee[“Age”])print(“Salary : %d” %Employee[“salary”])print(“Company : %s” %Employee[“Company”]) |

Output:

| <class 'dict'>printing Employee data ….Name : JamesAge : 25Salary : 28000Company : GOOGLE |

In Python, you will find an alternative method of using the get( ) method for accessing dictionary values. The result you would get is similar to the output by the indexing.How to Add Dictionary ValuesAs I said earlier, the dictionary is a mutable data type. You can update its values using the specific keys. The values are updated together with key Dict[key] = value . Existing values can be updated using the update ( ) method. This feature enables you to update the key-values present in a dictionary. It helps to update the new keys added in the dictionary.Here is an example of how to update dictionary values.

| # Creating an Empty DictionaryDict = {}print(“Empty Dictionary: “)print(Dict)#How to Add Elements to Dictionary SeriallyDict[0] = ‘Paul’Dict [2] = ‘John’Dict [3] = ‘Richard’print(“\nDictionary after adding 3 elements: “)print(Dict)#How to Add Set of Values# with a single key# The [‘Emp_ages’] = 20, 33, 24print(“\nDictionary after adding 3 elements: “)print(Dict)# Updating existing Key's ValueDict[3] = ‘JavaTpoint’print(“\nUpdated key value: “)print(Dict) |

Output:

| Empty Dictionary:{}Dictionary after adding 3 elements:{0: ‘Paul’, 2: ‘John’, 3: ‘Richard’}Dictionary after adding 3 elements:{0: ‘Paul’, 2: ‘John’, 3: ‘Richard’,  ‘Emp_ages’ : (20, 33, 24)}Updated key value:{0: ‘Paul’, 2: ‘John’,  3: ‘JavaTpoint’, ‘Emp_ages’ : (20, 33, 24)} |

How to Delete Elements using del keywordYou can quickly delete the items of the dictionary using a del keyword, such as in this example.

| Employee = {"Name": "James", "Age": 25, "salary":35000," Company":" GOOGLE"}print(type(Employee))print("printing Employee data ….")print(Employee)print(Deleting some of the employee data")del Employee["Name"]del Employee["Company"]print("printing the modified information ")print(Employee)print("Deleting the dictionary: Employee");del Employeeprint("Lets try to print it again ");print(Employee) |

Output:

| <class ‘dict’> …..Printing Employee data ….{‘Name’ : ‘James’, ‘Age’ : 25, ‘salary’ : 25000, ‘Company’ : ‘GOOGLE’}Deleting some of the employee dataprinting the modified information{‘Age’ : 25,  ‘salary’ : 25000}Deleting the dictionary: EmployeeLet's try to print it againNameError: name 'Employee' is not defined |

An error is in the above print statement because the Employee dictionary that was requested for printing has been deleted.Another method is through the pop ( ) method. This method accepts the key as an argument. It also removes the related value as in the example below:

| # Creating a DictionaryDict = {1: ‘JavaTpoint’, 2: ‘Paul’, 3: ‘Thompson’}# Deleting a key# using pop( ) methodPop_ele = Dict.pop(3)Print(Dict) |

Output:

| {1: 'JavaTpoint',  2: 'Paul’} |

In Python, there are built-in methods such as popitem( ) methods and clear ( ) methods for removing factors from the glossary.Popitem methods remove arbitrary elements from a dictionary. Also, the clear( ) feature removes all elements from the whole Python dictionary.How to Iterate DictionaryYou can use a loop for iterating a dictionary. Look at the example# Using for loop to print all the keys of a dictionary.

| Employee = {“Name”,: “James”,  “Age”: 29,  “salary”: 25000, “Company”: “GOOGLE” |

Output:

| NameAgeSalaryCompany |

The Properties or Features of Dictionary KeysIn Python dictionaries, multiple values cannot be stored for the same keys. In situations where multiple values are assigned to a single key, the value that is assigned last to such key becomes the value of such key. For example:

| Employee = {“Name”:”James”, “Age”:30, “salary”:35000\. "Company":" GOOGLE"," Name":" James"}For x,y in Empoyee.items ( ):print(x,y) |

Output

| Name JamesAge 30Salary 35000Company GOOGLE |

The second method is a situation where the keys are not mutable objects. Strings, tuples, and numbers could form the key. However, lists are considered as mutable objects and not useful as the keys in the dictionary. For example:

| Employee = {“Name”: “John”, “Age”: 29, “salary” 35000, “Company”:”GOOGLE”, [100,201,301]:”Department ID”}For x,y in Employee.items ( ):Print(x,y) |

Output

| Traceback - recent call last:File “dictionary.py”, line 1, inEmployee = {“Name”: “James” , “Age”: 30, “salary”:25000, “Company”: “GOOGLE”, [100,201,301]:”Department ID”}TypeError: unhashable type: ‘list’ |

Looking at the methods and functions of the built-in dictionary in Python programs includeThe Methods of Built-in Dictionary

1.  dict.copy( ) – this helps in returning a shallow copy of the dictionary.
2.  dict.get(key, default  = "None" - used for getting the specified value for the passed key.
3.  dic.clear( ) – used for deleting all the items of the dictionary.
4.  dict.fromkeys(iterable, value = None, /) – this is used for creating a new dictionary from the iterable, making the values equal to value.
5.  dict.keys( ) – used for returning all the keys of the dictionary.
6.  dict.items( ) – this method returns all the key-value pairs as a tuple.
7.  dict.has_key(key) – if the glossary has the specified key, this method returns true.
8.  dict.values( ) – this method returns all the values of the dictionary.
9.  dict.update(dict2) – useful for updating the dictionary by adding key-value pair of dict2 to the dictionary.
10.  dict.setdefault(key,default = "None") – this feature sets the key to the default figure if the specified key is not in the dictionary.
11.  index( )
12.  len( )
13.  count( )
14.  pop( )
15.  popItem( )

Functions of Built-in Dictionary

1.  len(dict) – this functionality is used for estimating the length of the dictionary.
2.  type(variable) – used for printing the type of the passed variable.
3.  cmp(dict 1, dict2) – this is used for comparing items of both the dictionary and returns true, especially if the first dictionary values are greater than the second dictionary. Otherwise, the output will return false.
4.  str(dict) – this feature converts the dictionary into a printable sequence representation.

Understanding the String TheoryPython strings are popular data types. This is a collection of characters surrounded by single quotes, double quotes, and even triple quotes. A computer device does not understand these characters. However, manipulated character, which is a combination of the 0's and 1's, are stored internally.These characters are encoded in the Unicode character or ASCII. This feature makes Python strings to be regarded as a collection of Unicode characters.Strings are formed by the series of letters in the quotes or enclosing the character. You can create strings using triple quotes, single quotes, or even double-quotes.Let us check this example using syntax to create a string.

| Str = “Hi Python !” |

In this example, the type of variable string used is Python script.

| Print(type(str), it will print a string (str). |

Strings are handled as a sequence of characters. In other words, Python doesn't agree with the letter data-type. Therefore, one letter represented as 'p' can be handled like the string of the first length.How to Create String in PythonStrings are created by putting the letters in double quotes or single quotes. There are also triple quotes used for representing strings. However, you can use triple quotes for docstrings or multiline strings.  For example

| #Using one quotation marksString1 = ‘Hello Python’print(string1)#Using double quotation marksString2 = “Hello Python”print (string2)#Using triple quotation marksString3 = "" ' Triple quotation marks are used for representing docstrings or multiline strings"'Print(str3) |

Output:

| Hello PythonHello PythonTriple quotation marks are generally used to represent docstrings or multiline strings. |

How to Index and Split StringsIn Python language, as in other languages, the indexing of Python strings begin from 0\. That means the string "HELLO" is indexed as shown below.Str = "HELLO"

| H | E | L | L |

0             1                         2                   3                 4str[0] = ‘H’str[1] = ‘E’str[2] = ‘L’str[3] = ‘L’str[4] = ‘O’Now, you can also check this example below.

| Str = “HELLO”print(str[0])print(str[1])print(str[2])print(str[3])print(str[4])# this is returning the indexError because 6th index doesn’t existprint(str[6]) |

Output:

| HELLOIndexError: string index is out of normal range |

As shown in the example above, the individual characters of the string can be accessed using the slice operator [ ]. Meanwhile, the substring could be obtained using the colon operator (: ) in Python.Look at this example:Str = "HELLO"

| H | E | L | L |

0             1                         2                   3                 4str[0] = ‘H’                                  str[:] = ‘HELLO’str[1] = ‘E’                                   str[0:] = ‘HELLO’str[2] = ‘L’                                   str[:5] = ‘HELLO’str[3] = ‘L’                                   str[:3] = ‘HEL’str[4] = ‘O’                                  str[0:2] = ‘HE’str[1:4] = ‘ELL’In these examples, you can see that the higher series given in the slice operator is exclusive at all times. That is if str (string) = 'HELLO' is given. Then, str [1:3] will have str - string[1] = ‘E’ and str[2] = ‘L’ with nothing else attached.Check this example

| # Given StringStr = “JAVAPOINT”# Begin 0th index to the endprint(str[0:])# Begins 1th index to the 4th indexPrint(str[1:5])# Begins 2nd Index to the 3rd indexPrint(str[2:4])# Begins 0th index to 2nd indexPrint(str[:3])# Begins 4th index to 6th indexprint(str[4:7]) |

Output:

| JAVATPOINTAVATVAJAVTPO |

Negative cutting in the sequence begins from the rightmost character. This is indicated as -1while the second rightmost character is shown as -2, and it continues in that order.Look at this figure below.Str = "HELLO"

| H | E | L | L |

-5           -4                    -3                -2                    -1Str[-1] = ‘O’                          str[-3:-1] = ‘LL’Str[-2] = ‘L’                          str[-4:-1] = ‘ELL’Str[-3] = ‘L’                          str[-5:-3] = ‘HE’Str[-4] = ‘E’                          str[-4:] = ‘ELLO’Str[-5] = ‘H’                           str[::-1] = ‘OLLEH’Look at this example

| Str = ‘JAVATPOINT’print(str[-1])print(str[-3])print(str[-2:])print(str[-4: -1])print(str[-7:-2])# Reversing the given stringprint(str[::-1])print(str[-12]) |

Output:

| TINTOINATPOITNIOPTAVAJIndexError: string index out of range |

How to Reassign StringsYou can reassign strings by renewing the contents and placing them in a new one. Assigning items is not supported by string objects. Strings are immutable and cannot be swapped. The content of strings is replaceable by new strings.See this example:

| Str = "HELLO"Str[0] = “h”Print(str) |

Output:

| Traceback - recent call lastFile "10.py", line 2, in <module>Str - String[0] = “h”;TypeError: 'str' or ‘string’ object doesn’t hold up item assignment |

In this sample, the (str) string can be transferred completely to a new content. Look at this second example:

| str = "HELLO"print(str)str = “helloprint(str) |

Output:

| HELLOHello |

How to Delete StringsAs I said earlier, strings maintain their immutable features in Python. Therefore, you cannot erase or take away the characters from the string. But you can delete the entire string using the del keyword.

| str = “JAVATPOINTdel str[1] |

Output:

| TypeError: 'str' object doesn't support the deletion of item |

Now, to delete an entire string, look at this example.

| str1= “JAVATPOINT”del str1print(str1) |

Output:

| NameError: name ‘str1’ is not defined |

What are String Operators?Several string operators exist in Python programs such as:

1.  Range Slice operator [ :] – this is used for accessing characters from a specified range.
2.  Slice operator [ ] – used for accessing the substrings of a particular string.
3.  Concatenation operator + - this is used for joining the strings given on either side of the operator.
4.  Membership operator (not in ) – used for reversing in. When a specified substring is not present in a specified string, the operator returns true.
5.  Repetition operator = - used for concatenating numerous copies of similar string.
6.  String formatting operator % - used to format strings. It also uses format specifiers applied in C programmings such as %f and %d. These specifiers are used for mapping values in Python.
7.  Raw string specifier  (r/R ) – for specifying raw strings used in situations where we should print the real signifiance of escape letters such as “C://python.” Before you can classify any string as unprocessed string, the letter should be followed by the particular string.
8.  Another membership operator (in ) – this operator returns true if an individual substring is available in a particular string.

Check out these operators in the following examples:

| str = “Hello”str1 = “world”print(str=3) # prints HelloHelloHelloprint(str+str1)# prints Hello worldprint(str[4]) #prints oprint(str[2:4]); # prints IIprint(‘w’ in str) # prints negative or false as w is not available in strprint(‘wo’ not in str1) # prints false as wo is available in string1 or Str1print(r’C://python37’) # prints C://python37 as it is written |

Output:

| HelloHelloHelloHello worldOIIFalseFalseC://python37The string str : Hello |

String Formatting in Python using Escape SequenceIf we need to write a text such as, He said, “Hello, where are you going?” This expression could be written in single or double-quotes. This will raise the SyntaxError in both quotes.Let us check out this example.

| str = “He said, “Hello where are you going?””print(str) |

Output:

| SyntaxError: invalid syntax |

This error could be handled using the triple quotes, although Python has an escape sequence. The escape sequence is represented with a backslash (/). If this is followed by a unique character, it is interpreted differently. In other words, the single quotes in the string must be escaped, and this pattern can happen in double-quotes.For example

| # using triple quotesprint(“””He said, “Who are you?”””# How to escape single quotesprint(‘He said, “What\’s happening?””)# How to escape double quotesprint(“He said, \”What’s happening?\”” |

Output:

| He said, “Who are you?”He said, “What’s happening?”He said, “What’s happening?” |

Here is a list of escape sequence in Python

| S/N | Escape Sequence | Description | Examples |
| 1. | \’ | Single Quotes | Print(‘\’’)Output: ‘ |
| 2. | \a | ASCII Bell | Print(“\a”) |
| 3. | \\” | Double Quotes | Print(“\””)Output: “ |
| 4. | \\ | Backlash | Print(“\\”)Output: \ |
| 5. | \b | ASCII Backspace (BS) | Print(“Hello \b World”)Output: Hello World |
| 6. | \newline | This ignores the line | print(“Python1 \ Python2 \ Python3”)Output: Python1 Python2 Python3 |
| 7. | \r | ASCII Carriege Return (CR) | print(“Hello \r World!”)Output: World! |
| 8. | \n | ASCII Linefeed | print(“Hello\n World!”)Output: Hello, World! |
| 9. | \f | ASCII Formfeed | print(“Hello \f World!”)Hello World! |
| 10. | \xHH | Character or letter with hex value | print(“\x48\x5\x6c\6c\x6f”)Output: Hello |
| 11. | \v | ASCII Vertical Tab | print(“Hello \v World!”)Output: Hello, World! |
| 12. | \t | ASCII Horizontal Tab | print(“Hello \t World!”)Output: Hello, World! |
| 13. | \ooo | The character or letter with octal value | print(“\110\145\154\154\157”)Output: Hello |

String Functions in PythonThere are several built-in functions used for handling strings in Python. These include1.    center(width, fillchar) – It returns a space padded string with the original string. This is centered with an equal numbers on the right and left spaces.2.    casefold( ) – returns a version of string ideal for case-less comparisons.3.    count(string,begin, end) – this counts the frequency of times a substring occurred in a string between starting and concluding index.4.    encode( ) – it encodes String using the codec entered for encoding. The default encoding is ‘utf-8’.5.    expandtabs(tabsize = 8) – this defines tabs in sequence to numerous spaces. Here, the default space value is 8.6.    Endswith(suffix,begin=0,end=len(string)) – it restores a Boolean value if the sequence terminates with a given suffix existing between starting and finishing.7.    format(value) – this feature restores a configured edition of string using the passed value.8.    isalnum( ) – this restores true if the letters in the string are alphanumeric. That means it contains alphabets and numbers with at least one character. If not, the expression will return false.9.    Index(substring,  beginindex,  endindex) -  this throws an exception if the string is not found. It functions as find( ) method.10.                         Isalpha( ) – this function restores true if all the letters are alphabets with at least one character. If not, the expression returns false.11.                         capitalize( ) – this function capitalizes the first letter of the string. It is deprecated in Python312.                         decode(encoding = ‘UTF8’ errors = ‘strict’) – for decoding the string using codec listed or indexed for encoding purposes.13.                         isdecimal( ) – this feature restores true if all the letters of the string are decimals.14.                         isnumeric( ) – if the sequence has only figures as characters, it returns true.15.                         isuper( ) – if the letters of a string are in the upper case, it returns false. If not, the string is false.16.                         Isprintable( ) - if all the letters of a sequence are printable or the series are empty, it returns true. If not, it returns false.17.                         istitle ( ) – when the first letter of a string is in upper case and the other characters are in lower case. It is a titled string. But if the sequence is titled correctly, it returns true. If not, it is false.18.                         isdigit( ) – this functionality restores true if all the cases are digits with at least one number. If it is not so, the statement returns false.19.                         Islower( ) – if the letters in a string are in lower case, it returns true. If it is not so, the string is false.20.                         isidentifier( ) – when the sequence is the valid identifier, this statement returns true.21.                         Isspace( ) – if the letters of a string are whitespace, the string returns true. If not, it is false.22.                         join(seq) – this function merges the representation of sequence of a specific string.23.                         len(string) – the feature restores the length of a string.24.                         lower( ) – this alters all the letters of a string to lower case.25.                         partition( ) – locates the separator (sep) in the string and restores the initial part that is the separator and part. When this separator is not seen in the sequence, it returns Strings with double empty strings.26.                         istrip( ) – removes all the significant whitespaces of a string. It can also remove a particular letter from leading in a string.27.                         replace(old,new[,count]) – replaces the old sequence of characters with the new sequence. In this case, maximum characters are returned when the maximum is specified.28.                         rindex(str,beg=0,end=len(str)) – this works in a similar way to find. However, it traverses the string in a backward direction.29.                         rstrip( ) – removes all trailing whitespaces of a string. It stops a given letter from trailing.30.                         title( ) – converts the string into a title-case such as meEruT will become Meerut.31.                         Upper( ) – this feature transforms all the letters of a string to upper case.32.                         zfill(width) – this returns original string padded with zeros on the left to a sum of width characters. This is intended for numbers and retains any given sign that is less than zero.33.                         translate(table,deletechars = “) – this translates the string according to the translation table passed in the function.34.                         swapcase( ) – inverts the case of all letters in a sequence.35.                         rsplit(sep=None, maxsplit = -1) – this functions as split( ). However, it can process the string from backward direction and returns the list of words in the string. When the separator is not given, the string will split according to the whitespace found in the sequence.36.                         splitlines(num=string.count(‘\n’)) – returns the list of sequences at each line with newline removed.37.                         startswith(str,beg=0,end=len(str)) – restores a Boolean value if the string begins with given string from the beginning to ending.What are the lists and their functions?A python list is used for storing the sequence of different types of data. Lists are mutable in Python. That means the elements can be modified after it is created. There are six different types of data used for storing sequences. However, lists are accessible and reliable types of data in Python.Therefore, a list is a collection of items or values of various types. These items are separated with a comma but enclosed with [ ] square brackets.This definition could be explained further, as shown below:

| L1 = [“James”, 102, “USA]L2 = [1, 2, 3, 4, 5, 6] |

I can print L1, L2, and L3 using type( ) functionality to make it a list. This will become

| print(type(L1))print(type(L2)) |

Output:

| <class ‘list’><class ‘list’> |

Features of Lists

1.  Lists are mutable types of data.
2.  It can store the number of various elements or characters in a sequence.
3.  Factors in a list can be accessed by index.
4.  Lists appear in an ordered form.

Let us analyze the statement in (d) above that lists are ordered.

| a = [1,2,”Peter”,4.50,”Ricky”,5,6]b = [1,2,5,”Peter”,4.50,”Ricky”,6]a = =b |

Output:

| False |

List1 and list2 contain the same elements. However, the second list altered the index point of the fifth element. This process breaks and abuses the order of lists. Therefore, in comparison, both lists return the false.In Python, lists uphold the sequence of elements for a lifetime making it the prearranged and structured assortment of objects.

| a = [1, 2, “Paul”,4.50,”Richard”,5,6]b = [1, 2, “Paul”, 4.50,Richard”,5.6]a = = b |

Output:

| True |

A detailed analysis of the list example

| emp = [“James”, 102, “USA”]Dep1 = [“CS”,10]Dep2 = [“IT”,11]HOD_CS = [10,Mr. Henry”]HOD_IT = [11, “Mr. Benson”]print(“printing employee data ….”]print(“Name    :     %s,   ID:   %d,     Country:   %s”% (emp[0],emp[1],emp[2]))print(“printing departments…”)print(“Department 1:\nName: %s, ID: %d\nDepartment 2:\nName: %s, ID: %s”%(Dep1[0],Dep2[1],Dep2[0],Dep2[1]))print(“HOD Details ….”)print(“CS HOD Name: %s, Id: %d”%(HOD_IT[1],HOD_IT[0]))print(type(emp),type(Dep1),type(Dep2),type(HOD_CS),type(HOD_IT)) |

Output:

| printing employee data …Name : James, ID: 10, Country: USAPrinting departments …Department 1:Name: CS, ID: 11Department :Name: IT, ID: 11HOD Details ….CS HOD Name: Mr. Henry, Id: 10IT HOD Name: Mr. Benson, Id: 11<class ‘list’> <class list’> <class list> <class ‘list’> <class ‘list’> |

The above example consists of lists of employees and departments with other corresponding information. You may go through the table above for a better understanding.Built-in Functions in Python ListsPython lists come with several built-in functions such as:

1.  len(list) – used for determining the length of the list. Examples include L1 such as [1,2,3,4,5,6,,8] print(len(L1))8
2.  max(list) – for returning the maximum element in a list. For example L1 = [12,34,26,48,72]print(max(L1)) 72.
3.  list(seq) = this function converts any sequence to the list. For example,

str = “Joseph”s = list(str)print(type(s))<class list>

4.  cmp(list1,list2) – for comparing all the factors of both lists but cannot work in Python3.
5.  min(list) – restores the lowest element of a list sequence. For example L1 = [12,34,266,48,72]print(max(L1))72

Here are some more examples of Python lists.

1.  Removing a duplicate element in the Python list sequence.

| List1 = [1,2,2,3,55,98,65,65,13,29]# Declare an empty list that will store unique values.List2 = [ ]For i in list1:if i not in list2:list2.apend(i)print(list2) |

Output:

| [1, 2, 3, 55, 98, 65, 13, 29] |

What are Multiple Assignments and Multiple Return Values?Multiple assignments enable a person to assign multiple variables simultaneously in one line of code. This feature becomes easy after an initial attempt, but you should learn about it. However, recalling multiple assignments when you need them, most could be very difficult.Multiple assignments mean the same thing as iterable unpacking and tuple unpacking. These three expressions could be used together in Python programming, but they say the same thing.Look at an example of multiple assignments in Python:

| >>> x,   y = 10,  20 |

In this sample, x is set to 10 while y is set to 20 . At a lower level, we have created tuples of 10 and 20. We can circle over the tuple and take each item from the looping and transferring them to the variables x and y serially.This is clearly expressed in this syntax:

| >>> x,   y = 10,  20 |

In Python, parenthesis are applied as optional features in tuples and optional in multiple assignments. This functions with a tuple-like syntax.Therefore, in these expressions below all the figures are equivalent.

| >>> x,  y = 10, 20>>> x,  y = (10, 20)>>> (x, y) = 10, 20>>> (x, y) = (10, 20) |

Multiple assignments are also known as tuple unpacking, as they are commonly used with tuples. However, multiple tasks could be used with any iterable and not just tuples.Using Multiple Assignments with a List

| >>> x,  y = [10, 20]>>> x10>>> y2o |

Using Multiple Assignments with a String

| >>> x,  y = ‘hi’>>>  x‘hi’>>>  y‘i’ |

As I explained before, objects that can be looped over are unpacked with multiple assignments or tuple unpacking.Let’s consider another pattern for demonstrating that multiple assignments function with variables and other items including objects.

| >>> point  = 10, 20, 30>>> x,  y,  z = point>>> print(x,  y,  z)10  20  30>>>  (x,  y,  z)  =  (z,  y,  x)>>> print (x,  y,  z)30 20 10 |

On the last line, we swapped variable names. This is something multiple assignments allows you to do quickly.Multiple assignments can improve the legibility of your codes and the accuracy of such codes. That means it can make the code more descriptive with embedded statement about the size and shape of the iterables for unpacking.Uses of Multiple Assignments in Python

*   Multiple assignments are used for replacing hardcoded slices.
*   It replaces hard-coded indexes.
*   It uses a tuple like a syntax but functions on any iterable.
*   Multiple assignments clarify your codes to human beings for the codes to be readable and computer devices for improved code correctness.
*   Multiple assignments are used for in-depth unpacking.
*   It is an alternative to slicing.
*   It helps you to use a list like a syntax.

Multiple Return ValuesIn Python, a function may restore multiple numbers by returning a sequence. You can assign the values to different variables using multiple local assignments or multiple assignments. This occurs when the sum of figures that will be returned is known.For example:

| i1 : f = I -> (I, 1^2, 1^3);i2 : (x,y,z) = f  3o2 =  (3, 9, 27)o2 : Sequence |
| i3 : xo3 = 3 |
| i4 : yo4 = 9 |
| i5 : zo5 = 27 |

When the frequency of numbers to be returned is unknown, use a simple assignment.

| i6 : s = f 4o6 = (4, 16, 64)o6 = Sequence |
| i7 : #so7 = 3 |
| i8 : s_0o8 = 4 |
| i9 : s_1o9 = 16 |
| i10 : s_2o10 = 64 |

Summary of FunctionsIn Python, functions are blocks of organized and reusable codes used for performing single-related actions.  They provide better modality for your software with a greater level of code reusing.Python comes with various integrated functionalities such as print ( ) functions, type ( ) functions, etc. However, define and create your tasks by customizing your software according to the projects you have at hand. These are known as user-defined functions.Defining and Identifying Function Keys in Python

*   Function blocks start with a keyword such as def . This is trailed by the function name including parenthesis ( ( ) ).
*   Every function has a code block starting with a colon ( : ), and this sign is indented.
*   A function is exited using the statement return expression. This can pass back an illustration to the caller optionally. Return statements could have no arguments as a return None.
*   Place arguments or parameters within parentheses, and these could be defined inside the brackets.
*   An optional statement can form the initial expression of a function. That is the docstring or documentation string of the function.

An Example Using Syntax

| def  functionname( parameters  ):“function_docstring”function_suitereturn  [expression] |

Parameters have a positional performance by default. That means you should place them serially as they were defined.An Illustration is

| def printme( str ):“This prints a passed string into this function”print strreturn |

You can define a function and give it a name. With this, you can specify the parameters to be embedded in the function, and also structure the blocks of letters.  If you finalize the basic structure of a task, you can execute it by calling it from another feature. This process is done by following the prompt from Python.Numbers and StringsIn Python, data could be represented using objects such as numbers and strings. These are built-in objects that you can create with external language tools known as X extension libraries. In most cases, Python provides these objects.Integers, complex numbers, and floating-point numbers are accepted in the programs. These are expressed as

*   int for integers
*   floating-point numbers, and
*   multiple classes in Python.

The separator of floating-point numbers and integers are the absence or presence of a decimal.An example of a floating-point figure is 2.0, while 2 is an integer. You can represent complex numbers using variables such as x _ yj. In this expression, x is the first or significant part, while y is the secondary or unreal part.Defining the values and variables in an expression is possible by using the type ( ) function. This enables you to know the class a value or variable belongs. Another method is using the isinstance ( ) function to see if it pertains to a specific class.For example:

| e =7print(type(f))print(type(7.0))g = 7 + 3kprint(g + 3)print(isinstance(g, complex)) |

Output:

| <class  ‘int’><class  ‘float’>(8+3j)True |

Integers can have any length in an expression. A floating-point number is only accurate if it has 15 decimal places. If you notice a 16th decimal place, the expression is not correct.These numbers have decimal numbers in base ten number system. Programmers usually work with binary (base 2) numbers and base 16 (hexadecimal) numbers. They can also work with base 8 (octal) numbers.                                       You can place a prefix before the numbers to represent numbers in Python.Prefixes Used for Numbering Systems

| S/N | Number System | Prefix |
| 1. | Binary Numbers | ‘0B’ /   ‘0b’ |
| 2. | Octal numbers | ‘0O’ /  ‘0o’ |
| 3. | Hexadecimal numbers | ‘0X’ /     0x                                                                                                      |

Look at these examples

| # Output : 107print(0b1101011)#Output : 253  (251 + 2)print (0xFB + 0b10)#Output : 13Print(0o15) |

Output:Run the program, you will have an output such as:

| 10725313 |

Types of Number Conversions in PythonNumbers can be converted through coercion. This is a process of converting one number into another. You can use operations like additions and subtractions to coerce integers to float automatically. This operation happens successfully if one of the operational figures is a float.For instance:

| >>> 1 + 2.03.0 |

In the statement above, I integer is coerced into 2.0 float through addition. The result of this coercion is also a floating-point number, 3.0.Another process is through integrated functionalities like int ( ), float ( ), and complex ( ). We can use these functionalities to convert numbers between types. Also, these functionalities can convert numbers from strings too.Examples

| >>> int(2.3)2>>> int(-2.8)-2>>> float(5)5.0>>> complex(‘3+5j’)(3+5j) |

The numbers are truncated, making the decimal parts to be removed if you are converting from float to integer.Using Python DecimalYou can make some amazing calculations using a built-in class float in Python. In Mathematical calculations, the sum of 1.1 and 2.2 = 3.3. However, in Python there is disagreement and discrepancy.

| >>> (1.1 + 2.2) = 3.3False |

This result implies that floating-point numerals are executed in computer hardware like binary fractions. This is the only type of figure the computer system understands: binary numbers 0 and 1 . Therefore, it will be complicated to store decimal fractions in your computer system.For instance, the fraction 2/6 cannot be represented in a computer as a decimal number. It will give us 0.33333333….. and this result is long. But the answer can be approximated.However, the decimal fraction 0.1 will give us an incredibly long binary fraction of 0.0001100110011001100 …But there are the highest numbers of figures that the computer can accept and store. For this reason, we can approximate 0.1, and it cannot be equal. It is worthy of note that this shortfall is not an error from Python but due to limitations of the computer hardware.

| >>> 1.1 + 2.23.300000000000003 |

But, you can handle this discrepancy using the module for decimals built-into Python. Floating-point numbers have precision up to fifteen decimal places. It has a decimal module with user-settable accuracy.The difference between both results will show:

| import decimalprint(0.1)print(decimal.Decimal(0.1)) |

Output:

| 0.10.100000000000000055511151231257827021181583404541015625 |

You can use this module to perform the decimal calculations as we learned in the school. This format maintains the significance of values.Lists and DictionariesAs I said earlier, lists are like arrays used in other languages. It is a homogenous tool in Python making it significant in the program. A list contains datatypes known as integers, objects, and strings. Lists are mutable features in Python and can be altered after they are created.For example

| # Python program to demonstrate# Lists# Creating a List with# the use of multiple valuesList = [“Books”, “For”, “Books”]print(“List containing multiple values: “)print(List[0])print(List[2])# Creating a Multi-Dimensional List# (By Nesting a list inside a List)List = [[‘Books’, ‘For’ ] ,  [‘Books’ ]]print(“\nMulti-Dimensional List: “)print(List) |

Output:

| List containing multiple values:BooksBooksMulti-Dimensional List:[[ ‘Books’ , ‘For’], [ ‘Books’]] |

DictionaryIn Python, the dictionary is an unorganized compilation of data values for storing values and characters like a map. Therefore, unlike different data types holding only a one value as an element, a dictionary contains the key:value pair. This is used for optimizing a dictionary. In a dictionary, each key-value pair is separated using a colon (: ). But each key in Python is divided by a comma (,).For example:

| # Python program to demonstrate# dictionary#creating a Dictionary# with Integer KeysDict = {1: ‘Books’ , 2:  ‘For’ ,  3:  ‘Books’}print(“Dictionary with the use of Integer Keys: “)print(Dict)# Creating a Dictionary# with Mixed keysDict = {‘Name’ : ‘Books’ ,  1:  [1,  2,  3,  4]}print(“\nDictionary with the use of Mixed Keys:  “)print(Dict) |

Output:

| Dictionary with the use of Integer Keys:{1:  ‘Books’ ,  2:  ‘For’ ,  3:  ‘Books’ }{1:  [1,  2,  3,  4],   ‘Name’ :  ‘Books’} |

Variations of List and Dictionary

| S/N | List | Dictionary |
| 1. | Indices of lists are integers beginning from 0.  | The keys of the dictionary are organized from any data type. |
| 2. | You can create lists by placing elements in [ ] separated by “, ” comma. | Create a dictionary by placing elements in {} as “key”:” value,” each key-value pair is separated by commas “, .” |
| 3. | Lists sustain and support the order of elements entered in the program. | The order is not maintained. |
| 4. | Elements in lists can be accessed through indices. | Elements in the dictionary are accessed through key-values. |

CHAPTER FOURUNDERSTANDING CLASSES, METHODS, AND MODULESIn python, classes are templates that can help you in creating or customizing your objects.  Variables and functions are encapsulated as a single entity. But objects generate their variables, features, and functionalities from classes.Some of the ideas to note for creating classes are that classes enable you to build a template for classifying things or objects generally. The classes created can be worked on or customized. Classes are objects used for producing samples of those templates where you can apply methods and other operations. You can organize, conceptualize, and build an organogram or hierarchy for any organization.Classes are used for defining procedures and relations for company, industrial, social, and other settings. This is an online data technology position.Here are features to consider before using classes in Python.

1.  Create or develop a class and apply it.
2.  Create or design a module before moving the class and launch to the module.
3.  Go to a new program and call the module before using the class.

After creating a class, create a module, and transfer the codes you created in the class into it. With this, you can create a common group of x,y synchronizations in any program.What is a Module?A module is a file with Python statements and definitions. It is also a Python code sourced from other programs. Modules are used for everyday tasks, and you don’t have to enter them in every program where you could use them.You can call a package module using “matplotlib.plot.” Without this module, you must state the functions of the plot in every program where a plot graph is used.In Python documentation, if you exit from Python interpreter and open the software again, the definitions, which are variables and functions, are lost.  But writing a more extended program requires you to use a text editor in preparing the data for the interpreter. Then, run the file as input.This process is known as scripting. Splitting long programs into several files is recommended to maintain the application. Apply a handy function written for several applications. In this case, you don’t need to copy the description into all programs before working.Python can help you arrange descriptions in a folder or file and apply them in a script. It could also be used in a relational occasion of the interpreter.  Data organized in that manner are called modules . The descriptions from a module are extracted into different modules or the main module. This is a collection of variables, which you can access in a script. They can be performed at the upper level or in the calculator mode.From the analysis above, you can understand that it takes class creation and features to transfer an instance from the program into a specific class. You can apply this function in your current program just by working and referencing this newly created module.Summary of what we did above:

1.  We developed and start the class.
2.  Created a function that moves a case of the class in four significant directions, such as right, left, up, and down. Here, the increments become the parameters or arguments for functioning.
3.  In a module, creating a function for calculating the distance between two requests of the class using the formula for graph distance.

What are the modules in Raspberry PI?A Raspberry Pi contains the compute module1\. This device is designed for industrial applications in a flexible form.The Specifications of a Computer ModuleThe module is the backbone of your Pi device as it contains 512MB RAM, BCM2835 processor, and a 4GB eMMC Flash device. It is comparable and similar to the SD card in a microcomputer. All these specs are included into a board measuring 67.6 × 30 mm. This board fits into a standard connector such as DDR2 SODIMM. This connector is also used in the memory of a laptop computer.This memory is coupled straight to the processor on the board.  Other processor interfaces could be accessed through the connector pins, and you will enjoy the flexibility of the BCM2835 SoC. In this case, more interfaces and GPIOs are available if compared to the Raspberry Pi making it possible to design and customize the system in a straightforward way.Libraries in PythonIn Python programming, you can limit using codes by adopting Python libraries and packages. These are a collection for relevant modules and functions valuable for programming instead of codes. You will find over one hundred thousand libraries and one hundred and ninety packages in Python. They have been designed and developed to make programming easy for beginners, including Pythonistas and Pythoneers, to offer solutions to various challenges in society.Python libraries are useful for machine learning, including data visualization, image, and data manipulation, and data science for different applications. Python packages include a collection of Python modules, and libraries are a collection of Python functions used for performing specific tasks.Here are some Python libraries and their features:Matplotlib libraryMatplotlib is a library that a programmer can use in writing two-dimensional graphs and plots through Python Script. You may need more than single axes in a version to handle scientific or Mathematical programs.You can also create numerous plots at a time using this library. It is useful in manipulating several figures and characteristics. Features of Matplotlib

1.  Easy to integrate several third-party libraries with Matplotlib software. The applications include ggplot, seaborn, and base map for mapping and projections.
2.  Features a dynamic group of people dedicated to handling your requests professionally.
3.  Matplotlib enables you to track new patches, bugs, and features requirements on the problem of tracker page from Github. That is the official page for handling various problems concerning this library.
4.  It can function with GUIs and diverse toolkits such as Jupyter Notebook, IPython Shells, and Python Scripts.
5.  This Python library can create quality figures suitable for publication. These figures could be available in hardcopy designs on various interactive platforms.

Requests LibraryThis is released under the Apache2.0 license and serves as a loaded Python HTTP library. It helps to make HTTP requirements user-friendly and responsive. This lib is made for beginners to help them to use most features of HTTP. It is easy to configure, customize, authorize, and inspect HTTP requests.Features of Requests Library

1.  Enjoying the benefits of HTTP proxy support. It helps your users to locate your files and pages faster and quickly.
2.  It features thread safety, connection pooling, Unicode response bodies, basic or digest authentication, value cookies, and other functionalities.
3.  Requests help to upload numerous documents at once. With this, you can work in an efficient and faster environment.
4.  Requests contain several features that can enable you to tackle custom headers, sweep parameters towards URLs, and perform SSL certificate verifications.
5.  It offers automatic decompression that helps you in restoring and reviving compressed data into the original format quickly.
6.  This Python lib enables you to use basic Python Dictionaries, add parameters, form data, complex documents, and headers.

Theano LibraryTheano could be used for compiling available computer programs. Programmers also call it an optimizing compiler. This library applies multi-dimensional arrays, making you not to about the outcome and perfections of your projects.It is designed for describing, analyzing, influencing, and optimizing various Mathematical operations simultaneously.Features of Theano Library

1.  It makes computation 140 times faster and easier. It can handle data-intensive applications.
2.  It offers various essential tools for detecting and analyzing dangerous bugs and other issues in the system.
3.  Theano helps you to work successfully on expressions without hassles or delays. With this, you can avoid nasty bugs as you work with illustrations.
4.  The features and functionalities are similar to Numpy’s own. Therefore, Theano integrates numpy.ndarrys in its system.
5.  Works directly with GPUs and complete diverse emblematic differentiation of many parts or at least one section.

Pillow LibraryPillow library depends on the PIL code configuration. It is a division of Python Image Library (PIL). It was transformed into a better and more-friendly version of PIL. This is your reliable firm while working with different types of image formats.Features of Pillow Library

1.  You will get more support from active community users that will answer your inquiries and provide solutions.
2.  This Python library helps you in creating thumbnails for descriptions. It carries most of the important parts of your figure.
3.  Supports a group of image filters such as smooth, smooth_more, blur, contour, sharpen, and find_edges.
4.  The ability to open and save images and influence the image environment.
5.  It supports various documents such as GIF, ICO, PCX, PDF, BPM, EPS, PNG, JPEG, WebP, IM, and PSD.

Keras LibraryKeras is suitable for beginners or programmers learning deep neural networks. It is an open-source, profound neural network library printed in Python. This is a user-friendly library with a better modular structure providing proper inspection policy for detailed networks.Features of Keras Library

1.  Keras library enables you to build deep models for smartphones such as iOS, Android, and including Java virtual machines.
2.  It features useful tools for creating different images and texts quickly.
3.  Supports recurrent and convolutional neural networks.
4.  This Python library can function on PaidML, TensorFlow, Microsoft Cognitive Toolkit including other platforms.
5.  Keras contains various implementations from the neural networks to form blocks such as levels, objectives, optimizers, functions, and other features.

Fire LibraryFire library can generate command-line interfaces (CLIs) instantly. This is an open-source Python library requiring less shapes of code.  It is a dominant library capable of deriving CLIs from any object in Python. Google also applies it to creating a command line. It is relevant for developing various experiment board paraphernalia.Features of Fire Library

1.  It features a linear output, and no docstrings are needed.
2.  It comes with CLIs capable of adapting to changes you bring to your code. This will be updated instantly, as you change your codes.
3.  Fire libraries can write and send commands automatically, as you call Fire ( ).
4.  Fire libraries are suitable for various Python objects such as classes, lists, modules, dictionaries, and objects.
5.  It has CLIs in a complete form featuring automated help-pages and completion of tab in an interactive system.

Natural Language Toolkit (NLTK)This is a renowned Python NLP library. It involves a group of language handing out libraries with several applications that cumulatively offer a emblematic and numerical language processing solution only for English.This library is printed in Python language. With Natural Language Toolkit, processing natural language using Python is now standard and ideal.Features of NLTK (Natural Language Toolkit)

1.  It contains a picture of data science. A handbook is also attached for guidance through the ideology of language dispensation for NLTK.
2.  Various structure methods, formation strings parsing, re-entrance, and different pathways are featured in NLTK.
3.  Features a vibrant discussion forum for analyzing issues affecting your program and NLTK.
4.  It contains more than fifty corpora and lexical properties such as question classification, stopwords corpus, SEMCOR, SentiWordNet, and open multilingual WordNet, and others.
5.  It allows semantic reasoning, classification, tokenization, tagging, stemming, and parsing using text processing libraries.

Scipy LibraryThis library is useful for technical as well as scientific computation. Scipy is a complimentary Python library appropriate for machine culture. It is also renowned for image manipulation.Features of Scipy

1.  Scipy is a high-level library containing nump.lib.scimath as well as NumPy. Using them from the direct source is preferable.
2.  It features a community of active members that are ready to answer your questions and resolve your issues.
3.  It has two ways of handling 1-d polynomials.

Arrow LibraryThis is a practical and user-friendly library in Python that functions with times and dates. It features a smart API that supports general schemes making it an exciting library. The library is well-suited for beginners with a basic knowledge of coding.Features of Arrow Library

1.  Suitable for various versions of Python such as Python 2.7, 3.5, 3.6, 3.7, and 3.8.
2.  Capable of resolving and eliminating strings in a natural process. Arrow is a time-sensitive library that is set to UTC by default.
3.  It converts timezones and offers timestamps as a feature. This library could be extended for your arrow derived kinds.
4.  Arrow offers timeframes ranging from microseconds to years. It also helps in creating a ceiling, time-spans, the floor, and range for time frames.
5.  Possible to create various input scenarios with Arrow with the simplest creation method.
6.  It generates, removes, influences, and converts times and dates. It is needed for executing quick updates of date-time type and plugging gaps.

FlashText LibraryIf you are searching for words and documents easily or replace the same in Python programs, you need the FlashText library. It functions with a collection of words and string. In this case, it will identify some words as keywords and replaces from Text Data . It is practical and suitable for programmers that are struggling wit word replacement processes.Features of FlashText Library

1.  It is suitable for extensive inquiry if the amount of keywords is above 500.
2.  This library is not used for searching unique letters such as -, #, *,^, etc. it is not used for pointing fraction of words too.
3.  Reserves keywords as Trie Data Structure, making it very dynamic and efficient.
4.  It uses an updated string for keyword replacement. FlashText will return lists of the keywords to the string while performing a search.
5.  It functions as a quick library and offers different string manipulation.

TensorFlow LibraryThis is a free, open-source machine learning collection in Python. TensorFlow contains a handful of useful tools, which are easy to learn. This library is relevant for different programs and dataflow. Before using TensorFlow in a computer device, install Colab Notebooks in the browser.Features of TensorFlowThese include

1.  It contains an easy to discover structural design. With this library, you can develop your ideas into codes before printing or publishing your projects.
2.  TensorFlow has eager execution enabling you to create and manipulate machine learning structures. It makes debugging more natural and better.
3.  The library functions with instant productive APIs such as Keras. It provides a quick iteration of mechanized learning representation.
4.  TensorFlow offers a solution to every machine learning problem.  It is straightforward to implement and use.
5.  It can transfer your ML representations in clouds and other devices, including on-premises in various browsers.

What is object orientation?Object orientation is a way of solving programs through computations using objects. The object is a component of a program used for performing specific actions and interacting with other elements of the program. The basic components of object-oriented programming are objects.An example of an object in a program is a person. Therefore, logically, such a person must have a name. The name becomes a property of that person who can carry out different functions such as eating, drinking, walking, etc. these functions become the methods of that person (objects)In object-oriented programming (OOP), codes are organized around objects, which can interact with each other making things happen. Designing a program where someone is driving a car, firstly requires you to describe the objects involved, which are a person and car.You will now specify the methods. These are: how a person can drive a car, how the vehicle is to be driven. After organizing the objects, you can bring them together and create a diagram of a vehicle being driven by a person.Therefore, a class is a model of an object, which is an idea. The object becomes an embodiment of that concept. A class is created before designing an object. After creating objects, you are ready to design something. This involves methods.In object-oriented programming, a method is a process associated with a class. It defines the behavior of objects created from the class. Actions performed by objects are known as methods. The interaction between class and method is known as binding.CHAPTER FIVEHOW TO USE FILES AND INTERNET WITH RASPBERRY PI![Using Internet.png](Image00017.jpg)Using Files and Internet on Raspberry PiYou can easily use files and the internet on your Pi. This will allow you to complete tasks and handle multiple projects on a virtual basis. Some of the ways to accomplish this are:

1.  Port forwarding – the best method of handling this issue is through port forwarding. You can access the internet through your router. Arrange for port forwarding feature on your router. That means you will configure the router to forward all inbound internet traffic on a particular port to the local IP address of your system.

Various routers are designed with this feature. But varieties of routers are available with different configurations, follow the directions on your router’s user manual to configure it properly. You may find it difficult to manipulate if you’re your Raspberry Pi has more than one router, or it is behind a firewall.A significant disadvantage of the port forwarding feature is that it renders a system port on the personal LAN to the free internet. It is advisable to manage this feature carefully because it is a security threat.

2.  Third-Party Online Port Forwarding Services – several alternative solutions for port forwarding are available through third party services. They can offer various categories of functionality.

What are the files in Raspberry PI?In a Raspberry Pi, files are the data or documents you save on your system for future references. These files are kept in folders for proper organization and management. A folder may contain several files or even other folders too. Raspberry Pi has file management software known as File Manager. This app is located at the right-part of the browser logo on the taskbar of the Pi system and represented with a battered filing cabinet.If you want to launch the file managing app, click the icon. Various file and folder lists will appear at the left-part of your window. Click on any folder to view the files inside. When you click on a folder, the files will appear on the right part of the window.You can view the files in a folder by tapping the small triangle beside the description of the folder. This action will cause the folders to open and display the folders or files inside, causing the triangle to point downwards. If you close the folder, the triangle will face the right beside the folder’s name.The full lists of folders in a Raspberry Pi are called a directory tree. This appears like a tree in an upside-down position. It begins to grow from a root in the folder. This folder has great significance in a Pi, and it is called a single backslash \ .This folder incorporates other folders that make using and navigating through your Raspberry Pi easily. If you check the list of folders on the window, you will notice one referred to as pi at the upper part of the list. This one is known as the home folder. Every user on the Raspberry device has this folder called Pi folder, which is the home folder. The programmer spends much time at home on the window. It is located and placed in the directory tree, and you don’t have to navigate to the main tree before seeing it.The home folder could be traced in the file manager with a quick click. Another method to locate the home folder is by scrolling and clicking many files and buttons before seeing it. This often regarded as the long way, but you should know the short cut.Navigating in File ManagerEvery file in your Raspberry Pi has an address assigned to them by the file manager. This appears as a list of folders you need to click before accessing the file. These addresses are called paths in the filing system. So, obtaining an address in your system is like strolling down a path. The pathway could have bends and alleyways before reaching your destination.Step-By-Step Method of Accessing a File in a Raspberry Pi

1.  Open the system and click the Home Folder.
2.  Tap on the pi folder within the home folder.
3.  Continue clicking on various folders and viewing them until you arrive at the desired folder.

Navigating through the device is easy since the File Manager will always direct you to the right file and folder.This is an example of an address that can take you to already installed apps in your Pi.

| /usr/share/raspi-ui-overrides/applications |

You can try this address to access files in your Raspberry device. Scroll down the list of files and folders in the tree to locate your file within /usr/share, as it contains a lot. By double-clicking on any app or folder in the file manager, you can launch and open them.How to manage the file system![Internet on Raspberry.png](Image00018.jpg)Organizing the file systemThe terminal in your Raspbian is used for manipulating and managing files in the system using specific commands. Here are some of the ways to manage the file system.How to Create FilesYou have several ways of creating a file in the terminal. But the easiest method of handling this process is by applying the Touch control. This command is used for creating and updating timestamps in a file. It involves a very simple syntax.  Type only “touch, ” followed by the filename.If a document with the description of the specified file does not exist, the command will quickly create a new file. Create a new file called textfile.txt in the /home/pi/ directory by following the command.

| pi@new-hostname – $ touch /home/pi/textfile.txt |

Deleting FilesDeleting a file is simple using the rm command . To delete the file you created above, just type rm before the file name on your window, and the data are removed.

| pi@new-hostname – $ rm textfile.txt |

How to Copy FilesCopying files is a straightforward commands on the Raspberry Pi and you can do this using the cp command. Two parameters such as copy directory and destination directory can help you to handle it.Now, if you want to copy the /home/pi/textfile.txt to the /tmp/ directory, you can use this command:

| pi@new-hostname – $ cp /home/pi/textfile.txt /tmp/pi@new-hostname – ls /tmp/ |

How to Show the Content of a FileContents in a file on your system could be displayed using a text viewer or text editor. In Raspbian, various programs can help you to view the contents of your files and folders.One of them is called less program. It can show the contents of your files on the screen one after another. It functions using the syntax ‘less.’ Go to your keyboard and type the command, less, followed by the title of the document you want to display.If you want to show the content of the document you created above, use this command.

| pi@new-hostname - $ less /home/pi/textfile.txt |

After entering this command, the content will be shown in the less program window. However, quitting the less program is simple by pressing the q button on your keyboard.You can also show the contents of your file by applying the cat command . Here, the content will be displayed at the terminal directly. For example:

| pi@new-hostname - $ cat textfile.txtHello, world! |

Reading and Writing FilesIf you want the output of your program to be readable by humans, you can present your data in several ways. You can even file the information for future use.Ways to Write ValuesYou can write values through

1.  Write ( ) system of file objects. Here, the regular output document can be referenced as sys.stdout .
2.  Expression statements.
3.  The print ( ) function.

Most times, you should format your output properly instead of printing separated values. You can format your output or writings in two ways such as

1.  String slicing and concatenation operations. With this, you can design any possible layout. It has some procedures for performing essential services for stuffing strings to specific column width.
2.  Using the str.format ( ) process.

The string element has a template class that provides another way of alternating value strings. Python program can help you in converting values to strings and transfer it to the str ( ) function or repr ( ) function.A string may contain a filename or few characters. This will define the way (mode) the file may be used. The mode could be ‘r’ indicating data meant to be read while ‘w’ for files that will be written. It could also be used for data marked for deleting.‘a’ opens the doc for attaching or appending any info written to the file. This is added automatically to the end. If you see the codes ‘r+’, it means the files are available for interpreting and writing.When docs are opened in text mode, you can read and write sequences from the file or read and write sequence to the file. These are preset in a particular encoding. But if the programming is not specific, the default is dependent on the stage. The code ‘b’ attached to the method opens the doc in a binary mode. Here, the data will be written and read like bytes objects. The pattern is suitable for files without text.If you are reading in text format, the default will convert the platform-specific line endings such as (\r\n on Windows, n\ on Unix) to just \n. If you are writing in text mode, the default will transfer episodes of \n back to the platform-specific line endings.These modifications are suitable for text data but can corrupt binary data such as the JPEG or EXE docs. Be cautious about using binary modes when reading and writing such files.What are the differences between the Internet and Pickling?#![Remote connection on Raspberry Pi.png](Image00019.jpg)Internet Connection on Raspberry PiThe internet is used for accessing the web from a mobile device or computer. As I mentioned above, you can do this through port forwarding. This involves changing the configuration of your router to forward all inbound traffic from the internet on a port to a local IP address. It could also be done through third party agencies handling port forwarding.Pickling is the process of using a module to implement a fundamental and robust algorithm for serializing and de-serializing a Python object structure. This involves converting a Python object hierarchy into a byte stream. Wherefore, unpickling is the inversion of this operation, causing a byte stream to be reconverted into an object chain of command.These two terms, pickling and unpickling, are also referred to as marshaling, flattening or 1, and serialization. The pickle module maintains a pathway of the objects already serialized. This will prevent the serialization of the same objects in future references.CHAPTER SIXHANDLING GRAPHICAL USER INTERFACES IN RASPBERRY![GUIs on Raspberry.png](Image00020.jpg)GUIs on Raspberry PiGraphical User Interfaces on a Pi is a type of interface that enables programmers and users to interact with your systems using visual indicator representations such as TVs and monitors. It was developed by Xerox Palo Alto in the late 1970s but deployed commercially by Apple’s Macintosh, including Microsoft windows OS.GUIs are the model of user-based blueprint in software, as it offers users the capacity to operate computers and various electronic gadgets intuitively. This is possible through direct application of graphical emblems such as buttons, tabs, menus, scroll bars, mouse, cursors, and windows. Nowadays, graphical user interfaces come with touch-screen and voice-prompt (command) features and functionalities.The best programming language for GUIs includes Java or C#, Python, C/C++, and HTML5/Javascript.Various GUI libraries are available for different languages. Some renowned GUIs include Windows 10 Mobile, BlackBerry OS, Microsoft Windows, Ubuntu Unity, macOS, Firefox OS for smartphones, GNOME Shell for desktop setting, Android, Apple’s iOS, and Palm OS-WebOS.What is Tkinter Module in PythonTkinter module in  Python is the de-facto library for Python programs. This module is supported by all platforms such as OS X, Linux, and Windows. Some widgets you can see in Tkinter include check button, canvas, frames, text, scrollbars, progress bars, labels, buttons, and combo boxes.In Python, Tkinter is a programming package in GUI. It involves a built-in library providing the TK GUI toolkit. It has a potent object-oriented interface. Tkinter and Python are the cheapest and easiest ways to create GUIs on any application.The Approach on How to Use TkinterThe first step is to import the module, such as Tkinter and functools, from partial. Then, create the main window. Add the desired amount of widgets to the basic window, such as labels, buttons, and entry.At this stage, display the message. Lastly, apply an event prompt on the widgets.A brief explanation of the fifteen widgets found in TKinter include

1.  Entry widget – for displaying a single-line text ground that can accept figures from a user.
2.  Checkbutton widget – ideal for displaying several options as checkboxes. With this, the user can choose many alternatives at a time.
3.  Frame widget – it serves as a bottle widget for organizing other widgets.
4.  Button widget – useful for showing buttons in your application.
5.  Canvas widget – for drawing shapes such as rectangles, polygons, lines, and ovals within your application.
6.  Listbox widget – for providing several options to the user.
7.  Menubutton widget – is used for providing different commands to the user. These commands are within the Menubutton.
8.  Label widget – available for providing a single-line description for other widgets in the application. It comes with various images.
9.  Text widget – helps you to display text in multiple lines.
10.  Spinbox widget – this is a deviation of the Tkinter Entry widget for choosing from several fixed values.
11.  Toplevel widget – for providing a separate window container.
12.  tkMessageBox widget – the module is for displaying message boxes in your applications.
13.  PanedWIndow widget – a container widget with many panes that are organized vertically and horizontally.
14.  LabelFrame widget – this is a simple bottle widget acting as a container or spacer for compound casement layouts.
15.  Scrollbar widget – for scrolling through various widgets such as listboxes.
16.  Scale widget – for providing a slider widget.
17.  Radiobutton widget – some options are displayed as radio buttons using this feature. But the user can choose and work with only one option at once.
18.  Message widget – for showing multiline text fields and accepting values from the user.

How do Hello World and Temperature Converter operate in GUIA proper understanding of the GUI will enhance your knowledge of how a temperature converter works. This project involves converting Celsius to Fahrenheit.Follow this process in the application and copy the codes into your Python editor for implementation.

| introduce  Tkinter  as  tk# Declare global variablestemp_c = Nonetemp_f = None# This function is called whenever the button is presseddef convert ( ):global temp_cglobal temp_f# Convert Celsius to Fahrenheit and update label (through textvariable)try:val = temp_c.get( )temp_f.set((val * 9.8 / 5)  + 32) |

Call it a name such as tkinter_temp_converter.py before running it. A new window will show with a part for typing in a number (in lieu of degrees Celsius). Tap the “Convert button,” and the corresponding temperature in Fahrenheit will appear. This will be shown in the label next to degrees Fahrenheit.Understanding Listbox and SpinboxThe Listbox doodad is for displaying a list of things from which the user can choose various items.The Simple Syntax for Creating ListboxThe syntax includes

| w = Listbox ( master, selection,  …  ) |

The Parameters for Using ListboxThe parameters for using Listbox involves master and options.

1.  master – used for the parent window.
2.  options – the most frequently used options for Listbox widget include the following, which are represented as key-value pairs with commas to separate them.

1.  height – this is the rate of lines displaying in the Listbox. The default number is 10.
2.  font – indicates the characters applied for the content in the Listbox
3.  highlightcolor – represents the color appearing on the focal point highlight when the widget is central.
4.  relief – for choosing the 3-dimensional border shading effects, as the default is sunken.
5.  selectmode – for determining the items that could be selected and how mouse drags can affect your choice. These options incorporate other features such as single, extended, multiple, and browse.
6.  highlighthickness – displays the thickness of the focus highlight.
7.  Selectbackground – shows the background color for displaying the chosen text.
8.  bd – the size of the border surrounding the indicator.
9.  yscrollcommand – with this, the user can scroll the Listbox vertically. It links your Listbox widget to a perpendicular scrollbar.
10.  cursor – appears whenever the mouse is placed over the Listbox.
11.  fg -  the color of the text within a Listbox.
12.  xscrollcommand – helps the user for scrolling the Listbox horizontally. With this, you can link your Listbox widget to a horizontal scrollbar.
13.  bg – represents the standard background color showing behind the label with an indicator.

The Methods of Listbox ObjectsThese methods include

1.  delete ( initial, end=None ) – this method eliminates the lines with key in the first and last ranges. If the succeeding row is removed, the solo line bearing the index first is chosen.
2.  get (initial, end=None ) – this method returns a tuple with the text of lines containing keys from first to last. It replaces the text of the line next to the first line if the second row is omitted.
3.  index ( i ) – tries to position the noticeable element of the Listbox if possible. This makes the column with the index i to be at the upper part of the widget.
4.  curselection () = this method returns a tuple with the line figures of the chosen elements/element, starting from 0\. It returns an blank tuple if nothing is selected.
5.  Activate ( index ) – helps in selecting lines specified by the given box.
6.  size ( ) – for returning the amount of lines in the Listbox.
7.  xview() – makes the Listbox scrollable horizontally. It sets the command option of the associated horizontal scrollbar to this format.
8.  xview_moveto ( fraction ) – the method scrolls the Listbox in a way the leftmost part of the width of its longest column is outside the left side of the Listbox. The portion is within the ranges of [0,1].
9.  yview() – makes the Listbox vertically scrollable. It sets the command option of the associated scrollbar to this method.
10.  yview_moveto ( fraction ) – this method scrolls the Listbox to the upper fraction of the width. If the top line is outside the left-side of the Listbox. The fraction is within the ranges of [0,1]
11.  see ( index ) – adjusts the location of the Listbox, making the line referred to by index visible.
12.  yview_scroll (number, what ) – helps in scrolling the Listbox vertically. It uses either unit to scroll by the lines for what arguments. It uses pages to navigate by pages by the elevation of the Listbox while the number argument tells how many to scroll.
13.  xview_scroll ( number, what) -  this method scrolls the number horizontally. It uses either unit for scrolling by characters for what arguments by the breadth of the Listbox. However, the number argument tells how many to scroll.
14.  nearest ( y ) – it places the noticeable element of the Listbox in a way the line with i is at the upper part of the widget.

The SpinboxThis is an alternative of the usual Tkinter Entry widget used for selecting a fixed number of elements.The Syntax of SpinboxThe simple syntax for creating this widget involves

| W = Spinbox( master,  selection,  … ) |

The Parameters for Spinbox include

1.  master – representing the parent window.
2.  options – containing the list of commonly used alternative for this widget. The options are applied as key-value pairs and separated by commas.

Detailed analysis of these options includesCHAPTER SEVENHARDWARE INTERFACES IN RASPBERRYThis device is designed with hardware interfaces for proper functionality. This is a low-cost single-board computer device for learning. The Raspberry Pi Foundation, a non-profit organization built this system.This device has different models from Raspberry Pi Zero to Raspberry Pi 3 is made with a 40-pin heard connector. They offer entrance to the GPIO pins with some other functionality. The header offers accessibility to 26 GPIO pins with 5 volts and 3.3 volts, including other individual pins for an  ID EEPROM function.Pin Connections in GPIOThese 26 GPIO pins could be configured especially as input pins or output pins. The system uses 3.3 volts, which is the nominal volt. Higher voltage, such as 5 volts, is dangerous to your device. Unconnected pins come with undefined levels of logic, but you can force separate pins to high or low level using pullup or pulldown resistors.This exercise is carried out in hardware with external resistors, but you can apply it to the software too. GPIO pins and GPIO3 pins are designed with permanent pull-up resistors on the board. However, other GPIO pins are configured in the software for providing a pull-up or pull-down resistor. In most cases, they offer no resistance at all.Functions of PinsThe general purpose input and output (GPIO) pins are configured to provide various functions even beyond the primary digital input and output. All pins display similar functions, but some have unique features and services. These pins can help a programmer to design various projects such as robots, retro games, weather stations, and other mighty machines with a Pi.These pins make it possible to use motors, lights, sensors, and other peripherals. You can connect these pins to your system through the SoC located within the Raspberry Pi. This will facilitate secure collaboration between your system and external components.It has about 40 pins, including UART, 12C, and SPI connections for the newer models.Let’s look at some of the functions of pins in a Raspberry Pi.1.GPIO (General Purpose Input Output) pins – these are digital pins that can send or receive current, and you can regulate their state using Python, node-Red, Python, and other programming languages. It operates with a voltage of 3.3 volts and draws about 16 mA of current.These pins interface with various devices using SPI, UART, and 12C protocols. GPIO3 use SCL and SDA 12C pins to connect to systems through 12C protocols. Before using these pins, you should enable the interfaces that can function with them by configuring your system using the Raspbian operating system.12C PinsThis is a serial protocol with low speed for connecting devices through the 1C standard. These devices operate on a master-slave relationship basis. They function through addresses given by the manufacturers using Linux commands such as 12C detect.These pins function with two connections, such as SDA and SCL, and send data to or from the SDA connectivity with its speed regulated by the SCL pin. 12C pins enable you to add temperature sensors, analog, digital converters, OLED, and LCD screens to your projects.Universal Asynchronous Receiver or Transmitter (UART) PinsThese pins send GPIO14 and receive GPIO15 with a console or terminal login headless setup. It links your PI device without a mouse or keyboard. This is possible through a network or direct USB connection. It can also be regulated using a serial cable or USB to serial board from a computer operating a terminal console.This pin is reliable and offers instant right to use your Pi without extra tools. You must enable this function by configuring the serial console in your Pi device.Serial Peripheral Interface (SPI) pinsThese pins help you to connect well-matched devices to your Pi. It functions through a master-slave relationship with devices just like the 12C pins.SPI pins are used for sending info over short ranges between microcontrollers and other components such as sensors, SD cards, and shift registers. The data is synchronized using a clock such as SCLK at GPIO11 from the master, which is the Pi. This is transmitted from the device to the SPI component through the MOSI pin, which include GPIO GPIO10 pins. MOSI means Master Out Slave In. This component replies to Pi by sending back data through the Master In Slave Out - MISO pin (GPIO9).3.3V Pins3V pins provide a stable power supply to your electrical components and enable you to test LEDs. You can connect the anode, and the long leg of the LED to the 3.3V pin through a resistor while the shorter leg and cathode are connected to the GND pins. This connection will enable your lights to shine for you to build your projects.Ground (GND) PinsThis is also called GND or gnd. All voltages are measured from this pin, and it completes an electric circuit. It refers to a zero point and connects LED to a source of power, making the GND part of the circuit system. The current can flow through this LED to produce light.A Pi is designed with 8 gnd connections through the GPIO connecting to a single ground connection.5V PinsThese pins enable direct access to the supply of 5 volts from the mains adaptor ensuring less power required by the Pi. It powers your unit directly but ensures a stable and moderate voltage before connecting your system.5V pins can bypass safety features such as fuse and voltage regulator. They could avoid these regulators from damaging your device.Other functionalities of these Pins include

1.  Pins GPIO12, GPIO13, GPIO18, GPIO19 supports pulse width modulation (PWM) on the hardware of Raspberry Pi. The software of any pin can also support this functionality.
2.  GPIO2 and GPIO3 pins support the 12 C interface.
3.  The serial interface of GPIO14 and GPIO15 pins can be used as a serialized console.
4.  GPIO8, GPIO7, GPIO10, GPIO9,GPIO11, GPIO17, GPIO18, GPIO1, GPIO21, GPIO20 pins provides serial peripheral interface (SPI) ports.

Pins in Serial InterfaceAs I stated above, the pins in the serial interface include GPIO8, GPIO7, GPIO10, GPIO9, GPIO11, GPIO17, GPIO18, GPIO1, GPIO21, and GPIO20.Prototyping Boards in RaspberryPrototyping boards are used for attaching some electronic components and sensors to a Raspberry Pi. Examples of prototyping boards in a Raspberry Pi include PiBreak Plus. This board provides labeled escaping pins for all GPIOs. It is a huge prototyping surface with solder pads and power bar for a secure connection to a power source. This board is well-suited with all models of Raspberry Pi and other boards with a 40-pin extension header such as Raspberry Pi Model A+, Raspberry Pi Model B+, and Raspberry Pi Model 2.Features of Prototyping Boards in Raspberry PiThe features of these boards include

1.  It comes with a large prototyping surface to connect your parts.
2.  The board has pinout markings on the top and bottom.
3.  It has bolts, nuts, washers, and spacers for proper mounting.
4.  There are 3.3volts and GND power rails.
5.  The board is gold-plated (PCIB) ENIG for durability.

CHAPTER EIGHTLEAD FADER AND PROTOTYPING PROJECTSThe Pi is a microcomputer and also regarded as a single-board computer (SBC). It can function with Linux operating system and other applications. This device is useful for various digital projects, such as lead fader projects and prototyping projects.A fader is a necessary component required for mixing console. It helps you to control your source through the movement of a fader. You can use pushbuttons in your projects by hacking the keyboard and mouse. It could also be done through gainer, Arduino, and MCK. This offers an alternative means of using faders with audio input and output.Lead fader provides efficient sampling resolution and frequency than 16bit to 8-10bit, including 44.1KHz to 1KHz.Requirements for Lead Fader ProjectsThe requirements for lead fader projects are fader, software, and soldering. Others include 1 heat shrink tube, 1 twin cable, 2 3.5mm Mono plug, wire strippers, nippers, solder-sucker, multimeter, clipped cables, and helping hands.These requirements can function only on variable resistor type faders but not on the optical type.Now, a Fader is sourced from a broken mixing console and electronic components store. Some local electronic component stores include Digi-Key, RSin, Maplin, Tokyu-Hands, and RadioShack.How to Assemble the HardwareGet a fader with three or more connectors and modify its resistance using the arrangement of the fader, which is a changeable type of resistor. Most mixing consoles come with optical fader, especially for DJ crossfader.The 2 3.5mm mono plug is for acoustic input and output, and one twin cable is used as the loudspeaker cable. You can make the length according to your choice. Get one heat shrink tube for connecting the fader.Get two pairs of cables and strip the ends. Check the connector of the fader before soldering. Some faders have three connectors. Two functions as resistors and the other one for the ground pin. By changing the resistance with a multimeter, you can find a proper connector.Solder the fader to the cables. Each side of the two wires should be soldered to each resistor side of the connector. Use the side of the resistor with one marker for one side. Add your heat shrink tube before soldering to make it firm.Twist the cutting side of the cable to avoid expansion. Cover the connector with heat shrink tube after soldering.After this, solder the ground side, but ensure that each cutting side of the cables is twisted to prevent expansion. Attach your heat shrink tube.Solder the plugs to the last part of each cable but install the plug cover. The cutting side of the cable should be twisted to prevent expansion. Attach the cover of the plugs after soldering.Use a multimeter on the resistance between the plugs. The upper side should be modified with the location of the fader. The gnd (lower side) should be zero. Now, you have a set of switch, a cable, and two plugs.Connect the acoustic input and output to make complete working hardware.Running the SoftwareOpen the window or environment of the program in your Raspberry Pi. That could be Flash, Pure Data, MaxMSP, and SuperCollider. Anyone that can handle the audio input and output is needed.You should assign an audio signal such as a 10000Hertz sine wave for audio output. Set the volume calculator for audio input. Peakamp object is needed for this project.Add a receiver for the calculator such as a multislider object.Begin the audio, move the fader to receive the connection. With this, you are set to use a fader with your projects. Use a sine wave oscillator for the acoustic input and output.Requirements for Prototyping ProjectThe requirements for this project include power, 555 astable, Cd4029 decade counting, diode, capacitor, and 9-Volt battery.How to Assemble Prototyping HardwareThe first thing here is using the ground rails and hooking up to the power stage. This will feed the circuit with power from the power source. The diode prevents reverse polarity to the system while the capacitor is used to even out the current. The circuit can be connected using a brick wall through a 9-V battery.After this setup, the astable 555 timer stage sends a regular pulse to the CD4029 from pin3\. This is connected to the capacitor and Potentiometer and attached to the 7,2, and 6 pins. These multiply the pulses coming from pin 3.The Potentiometer helps in charging the capacitor more or less quickly. If the capacitor voltage is at 1/3 of the main charge and the main charge is that of the battery. This can set pin 3 high. When pin 6 gets 2/3 charge, it causes pin 3 to be low making the capacitor to reduce low through pin 7\. With this, the charge can dissipate.If the capacitor voltage is at 1/3 of the base charge, it regulates the pin 3 to high. In this way, the process is repeated.Running the SoftwareThe NE555 Timer controls a regular pulse towards the CD4029 from pin 3 connected to the 15 pins of the device. The vibration begins from pin 2 and measures 1/3 of the base voltage, which is 3volt. The vibration stops when the pin detects 2/3 base voltage, which is 6 volts.The counter stage functions in binary mode and produces 4bit binary numbers between 0 and 15\. Each bit is transferred to one of the Q pins. A 1 turns on a LED since A turns it off.They can cause the LED to fade in and out rather than blinking on and off. This causes the 10k resistors to delay in charging and discharging of the capacitors and LEDs.What are in Phase Two of the Prototyping Project?The second phase is a quick design or preliminary design. This helps to create a simple model of the system, but not a complete design. However, the user will get an idea of the project. This phase requires a quick design, building a prototype, user evaluation, refining prototype, and product implementation and maintenance.There are four types of prototyping project models, such as evolutionary prototype, extreme prototype, incremental prototype, and rapid throwaway prototype.CHAPTER NINEPROJECTS IN RASPBERRY PIRaspberry is a pocket-size device used in unimaginable ways. You can design various projects such as electronic projects, full-fledged arcade machines, and other digital programs.One of these projects includes a weather station. Let us see how to construct a weather station.How to Construct a Weather StationThis project demands that you use a choice Pi board with a built-in wireless support. You can also use a Wi-Fi dongle for this project. Another essential hardware choice for this project is the BME280 sensor. This device can help you to analyze pressure, humidity, temperature, anemometer, wind vane, and rain gauge.You also need other common prototyping tools, including a 3D printer for crafting purposes. The Oracle Raspberry Pi Weather Station Software could be used for leveraging various Python API in the system.Beginners find this project an interesting one, as it helps them in collecting and analyzing atmospheric data. Also, this will boost your experience in using Pi projects. Apply sensors and Python libraries of choice to control their functions.Building a BotA Bot is a web software developed and designed on a Pi board. Go to the Twitter APIs and register a twitter application. Then, install and write the bot on your device using the programming language. Using the Twython documentation is recommended for the best performance and efficiency for the API bit.After this, automate the bot. This process will cause it to upload the CPU temperature of your Pi if it spreads to a certain temperature threshold.If you are an open-source enthusiast, this project can help you to explore the Twitter API. You can use this method to build a personal twitter bot. This is the recommended Raspberry Pi projects.How to Craft a Security SystemWith this device, you can design a motion capture security device. It is an HD surveillance camera system that can capture live videos and imageries if people or objects cross the monitored environment.A standard camera is used for time-lapse projects, or any other one could be used for this project. Most persons build this security apparatus for monitoring their driveways or checkmating on their dogs while they are away.Do a live stream of the videos using any mobile devices or from a browser. This camera can record motions and images into a video doc automatically or on-demand. However, you should operate the camera through the Pi camera module.[Motion detection software](https://motion-project.github.io/) could be used for configuring the system through the motion capture functionality.Some programmers configure their devices to send notifications to them whenever suspicious images are captured or recorded for examination.CHAPTER TENHOW TO PROGRAM GAMESAs a programmer, Raspberry Pi offers you an opportunity of learning the methods to program games. This is open-source software for kids and Pythoneers for creating fun games on the device. This project begins with the LÖVE game engine using Lua, a scripting language.This is often regarded as hackable fun on a cheap computer device made for learners of all ages. LÖVE is renowned for modern game programming.  If you must produce video games, you should learn the Lua language requested in major game studios all over the globe. It is a complimentary resource in the proprietary Unity and Unreal game engines. This is evident in different places in the world.LÖVE engine functions as the pygame framework in terms of features, since it has no IDE. This game engine is lightweight and not complicated like Godot. The program can work on any platform containing the Lua language. Platforms functioning with Linux, Mac, Windows, Android, and iOS can work with LÖVE programs.Step-by-step Process of Games Programming in Raspberry PILet us learn the systematic processes of game programming in Raspberry Pi.

1.  Install the LÖVE Program – the first step is to install the LÖVE program following an easy command on the device.

| $ sudo apt install love2d |

If you are running [Fedora](https://opensource.com/article/17/3/how-install-fedora-on-raspberry-pi) on your Pi, you can use dnf instead of LÖVE software

| $ sudo dnf install love2d |

However, by installing either of these applications, you have introduces Lua, SDL, or other apps that LÖVE needs to run on your device.Begin with Hello, World! ProgramThe LÖVE engine exists as a framework enabling you to use any text editor of your choice in programming your games. Begin with the “hello world!” program. Ensure this program launches on your device and introduces the basic syntax of both the LÖVE framework and the Lua language.Go to your system, open a text editor, and enter this text:

| Cwide = 520Chigh = 333love.window.setTitle(‘  Hello World ‘)love.window.setMode(cwide, chigh)function love.load( )love.graphics.setBackgroundColor(177, 106, 248)-- font = love.graphics.setNewFont(“SkirtGirl.ttf” , 72)endfunction  love.draw( )love.graphics.setColor(255, 33, 78)love.graphics.print(“Hello World”,  cwide/4, chigh/3.33)end |

Save those entries above as main.luaA standard zip file with .love extension is a distributable LÖVE package. The main file should be labeled as main.lua, and it should be on top of the zip file. You can create it in this form:

| $ zip hello.love main.lua |

Then, launch the app after creating the extension. This should be like this:

| $ love  ./hello.love |

This will give you an out, such as:“HELLO, WORLD!”This is an understandable code. The cwide and chigh variables are universal and could be seen in the whole script.The first block of code is called a function that sets the background shade of the program. The second block of code gets the “hello world!” printed on the screen.The line containing two dashes (--) is the comment section. It also includes a .ttf in the .love package . This leads to the new line text setNewFont with no comment. In this case, you should not use the Skirt Girl font. Get a font from [FontLibrary.org](https://fontlibrary.org/) . This will enable you to adjust the codes accordingly. You will now have codes such as:

| $ zip hello.love main.lua SkirtGirl.ttf |

Then, launch this program.

| $ love  ./hello.love |

Types of Games in Raspberry PIYou can install and play various games on your system. These include

1.  Minetest
2.  Widelands
3.  Duke Nukem 3D
4.  Beneath a Steel Sky
5.  Micropolis
6.  Freeciv
7.  Which-Way-Is-Up?
8.  Openrena
9.  Quake III Arena.
10.  Star Wars by Jedi Knight
11.  Battle for Wesnoth.
12.  Funny Boat
13.  Littlecrane
14.  Flight of the Amazon Queen.
15.  Abuse
16.  SuperTux
17.  Angry Drunken Dwarves.
18.  RailWorld
19.  PyDance
20.  OpenTTD
21.  Simutrans
22.  Quake 3 “other”
23.  Monsterz
24.  PrBOOM, and more.

Pygame and Hello pygamePygame means a Primer on Game. This is game programming in Python. If you understand the pygame as a programmer, use it in writing games on every platform and language quickly.This is a Python covering for SDL library. It means Simple DirectMedia Layer, which provides cross-platform accessibility for your Pi’s system underlying multimedia hardware components. These components include a keyboard, joystick, video, sound, and mouse.Pygame began as a substitute for the PySDL project. This program comes with a cross-platform nature convenient for pygame and SDL. In other words, you can write games and other python programs on any platform that supports these applications.Hello, pygame is another version of pygame.What are the coordinates?Coordinates serve as Raspberry Pi location tracker. It functions without GPS and can be attached to any vehicle. It is connected to Google Maps, making it easier for you to track and know the location of your car or other moving objects anywhere and anytime.Vehicle tracking or location tracking using this RPi is done using a sim card cell tower location.All you need for this feature to work in your Raspberry Pi are the hardware and software.Hardware

*   Sim card with a data connection.
*   USB dongle or USB power bank.
*   Ubuntu or Raspberry Pi.
*   Raspberry Pi with memory card for installing an Operating System.
*   5 volts or 1 A powerpoint from a moving vehicle.

Software

*   Google Maps Geolocation API private key.
*   Supported OS or Raspbian installed onto a Raspberry Pi.
*   weaved.com account for regulating Raspberry Pi on the internet.
*   Knowledge of computer programming for handling Python codes, HTML, and JavaScript codes.
*   The private key for uploading coordinates onto online storage platforms.

Using One RaspberryDo you know that you can apply one Raspberry Pi device as a multi-tool? Instead of using two Raspberry Pi devices, this feature helps you to manage different projects on one device.This is possible by installing the [balena cloud](https://github.com/balena-io-projects/balena-sound) in your system. The software can combine different projects and run them on one device. This feature enables you to accomplish more with your Pi.How to follow the MouseYou can move the mouse on a Raspberry Pi with the arrow keys on your keyboard.CHAPTER ELEVENWHAT IS RASPBERRY PI ROBOT?![Controlling Robots.png](Image00005.jpg)Raspberry Pi RobotsRaspberry Pi robot is a programmable robot kit that is done using a Pi. An example of Raspberry Pi robots is an Arduino robot. Raspberry Pi devices function like a desktop computer system but smaller and cheaper. Experienced programmers, students, hobbyists, and other enthusiasts can use it for building robots.Requirements for Raspberry PI RobotThe requirements for building a Raspberry Pi robot include

1.  2 five-volt DC motors.
2.  6 AA batteries in a holder – for powering the motors.
3.  Small breadboard – a device for building simple circuits without soldering.
4.  Sticky tack adhesive.
5.  Chassis - a flat and squared material measuring 6 inches, such as laser-cut plastic, legos, and cardboard. Additional two feet are needed for stabilizing the droid.
6.  L293D motor controller.
7.  Two wheels with grippy rubber tires – these tires snap onto the motor shafts.
8.  5-volt USB mobile phone battery pack – for powering the Pi device.
9.  Jumper wires for connecting all the equipment.
10.  microSD card – for loading the BOT’s software before it can function.

The Methods for Setting up a Raspberry Pi RobotConnect the WiresAfter mounting your device and the breadboard on top of the chassis, you can use an adhesive like a Sticky Tack to hold them together. Fix the L293D motor controller in the breadboard. Connect the jumper circuit to the right pins on your Raspberry device, including the breadboard.Then, attach both wires on each DC motor to the output pins of the motor controller.Connect your System to the Power SourceInstall the motors, wheels, and battery box to your robot’s underside. Connect the power cables and run them up to your breadboard. Then, connect them to the motor power input of the L293D. Attach the 5-volts battery pack and plug it into the Raspberry Pi.Download the SoftwareYou need to prepare the card by downloading the software that can help you to control your robot through the Pi. The software for running and powering your Pi is [NOOBS](https://www.raspberrypi.org/downloads/raspberry-pi-os/) . Go to the website and down it.Unzip and copy the OS of NOOBS into the microSD card. After this, slot in the card into your Pi. Connect your mouse, keyboard, and monitor to the Raspberry Pi. Follow the system prompts and install the Raspbian software to your system.Hook up to the InternetIf your system does not have Wi-FI, you can hook up to the internet with an Ethernet cable. Then, type this command into the terminal

| git clone [https://github.com/the-raspberry-Pi-guy/wired](https://github.com/the-raspberry-Pi-guy/wired) |

After that, you can type in

| cd wired |

You can also view at the simple 10-line Python program in the terminal with this command:

| nano first_move.py |

This command will open the code in Nano, which is Pi’s native text editor.Run the Python ProgramAt this stage, it is time to install the program and make your new robot move around. You should use this command to execute the code.

| Python3 first_move.py |

After entering the code, your robot will begin to move around in a square. Return to the program using Nano editor. Change the time delays and change the commands for backward, forward, right, and left to create your desired movements, actions, and responses in the robot.Add Sensors and Write New CodeIt is time to grow your robot’s potentials by adding sensors and writing new codes. That’s the essence of using the Pi platform for controlling your robot.Attach an infrared sensor to the robot’s nose. Program the bot to trail a black line on the floor. You can also add a camera with an integrated computer-vision code. This will help to get the droid in chasing after a ball or any other object you desire.How to Handle Autonomous RoverYou can build an autonomous rover that can function with your system. This device is useful for competitions and various activities. You can create this device by following simple rules and approaches.How to Assemble the HardwareThe equipment needed for this project includes Raspberry Pi 3, Pi camera V2, Arduino Mega 2560, and Tensorflow object detection API. Others are custom 3D chassis model, voltage regulators, pickup servo motors, custom Mr. W stepper motor controller, and batteries such as custom-made 4x Lithium 18650 rechargeable cell that can generate 21 volts.Running the SoftwareThe device is designed with software for processing and controlling all the movements of the rover. This software functions as the intelligence unit of the robot. It contains specific movement instructions and communicates with the Arduino. The motions could be like the move left thirty degrees or go to the right twenty inches.  The mobility of your robot depends on its serial communication.CONCLUSIONIf you are a Pythonista or Pythoneer, this book provides an incredible opportunity for you to understand how to navigate a Raspberry Pi platform successfully. You can play games and control technological devices such as robots, drones, and other machines easily with your Pi.The revolution in technology has enhanced the development of this pocket-size computer that can function like your desktop or laptop computers. However, it is cheaper and smaller in size.The Raspbian is its operating system and works with Linux OS. All you need to use this device properly is the right equipment such as a screen like monitor, HDMI, power source, adaptor, mouse, keyboard, internet connection, a television, and the Raspberry Pi itself. You also need knowledge of how to interconnect them for effective performance.The Raspberry Pi can operate all your smart home appliances. You should upgrade your IT skills by reading this book extensively and mastering the information loaded inside. With this, you can become a programmer capable of handling a microcomputer device and performing multiple assignments and technological projects.