
## INTERVIEW PAVEL BAIBORODIN

### Build an app in ten minutes

This new platform aims to give you all the tools you need to build an app for your Arduino project in ten minutes or less. Pavel Baiborodin gives us the lowdown on why Blynk is a game changer for budding developers

![](img/6866071e033820549b214c239744aaa0_11_0.png)

**Pavel Baiborodin**  
Has a history in development with microcomputers and experience with UX design. His desire to create Blynk comes from wanting to take the complexity out of developing for both Arduino and the Raspberry Pi. A get started guide is available on the website at www.blynk.cc

![](img/6866071e033820549b214c239744aaa0_11_1.png)

Four years ago and I was blown away with how quickly you can start prototyping physical interactive objects these days. Having a background in user experience and design, I quickly realised that I needed some sort of a visual interface to control my projects, but I was frustrated to discover that there is no easy way to do that. So, you just got your first LED blinking (by making baby steps in coding) and then you realise that you need to learn PHP, Xcode, Android and all the other things. Not to mention that most of the tools in this space were made by developers and for developers.

This is where I decided to fix that. I told Dmitry, my co-founder and CTO, about the idea, and we started building it for ourselves. The first project ever made was a watering system to keep my plants alive while I'm travelling. Of course it could have been automated, but I just enjoyed pressing the button to start the pump in another part of the world. Then we had a Kickstarter campaign, grew to a community of more than 200,000, and got billions of requests on our servers every month.

Blynk is the easiest and most adopted platform to build mobile applications for IoT projects and connected products. There are three major components: firmware, server and mobile apps. First of all, we provide libraries that can get almost any hardware online (currently more than 400 models) no matter what connectivity you choose. Wi-Fi, cellular, Ethernet and XBee are all already online, and for local connection you can use BLE and USB. Plus, I've forgotten to mention the likes of Node.js, Python and C.

Blynk also supports industrial communication protocols like RS232, RS485, UART, CAN, ModBus and OneWire. When your hardware is online, it would connect to our Blynk Cloud Server, which is open source and was built on Java. Access to Blynk Cloud Server is free, however you can also run it locally. In essence, the server connects your hardware and smartphone together.

The local Blynk server can even run on a $5 Raspberry Pi, where it will handle up to 1,000 requests per second. It's secure, lightweight and pretty damn fast. Then comes the mobile apps for iOS and Android where one can quickly snap together an interface to control things remotely and visualise sensor data. We've made it super-easy to use: you just drag and drop widgets like buttons, sliders, gauges, charts, maps and many others to create the interface you need. No coding or design skills are required as all the major UI configurations are made on the app side.

![](img/6866071e033820549b214c239744aaa0_12_0.png)

Blynk is packed with features designed specifically for the IoT, such as controlling multiple devices and groups, easy sharing access to hardware with other people, syncing physical and HMI states, real-time updates of UI on all the connected clients, push notifications, emails and other great stuff. Blynk does a lot, as you can probably tell.

**Developing a product like this seems like it's remarkably complex. Was it difficult getting it from concept to reality?**

It was, and still is incredibly challenging, but on the other hand, it is remarkably interesting and exciting. From the very beginning we set a really high bar for every component of the system. The first challenge I would mention is maintaining the same level of simplicity and flexibility in UX when such a complex product like Blynk continues to evolve every single week.

Secondly, there are thousands of devices with their own specifics and protocols, and being completely hardware and connectivity agnostic means a lot of work on the firmware. Volodymyr, who is our embedded solutions architect, has developed a solid basis for it and now it's pretty easy to add new hardware, but there are always small details we need to keep track of. Even a few of our competitors are using it.

In general, 'connecting the dots' and providing a seamless developer experience is the biggest challenge.

> Blynk is the easiest and most adopted platform to build mobile applications for IoT projects and connected products.

![](img/6866071e033820549b214c239744aaa0_12_1.png)

## OpenSource

Your source of Linux news & views

**Are there any requirements (hardware or software-based) that users need to be wary of before starting their projects?**

Blynk can work on almost any microcontroller or microcomputer. From Arduino and Raspberry Pi to Particle Photon, Intel Edison and the like. You can check the list of supported hardware on our website (www.blynk.cc) for starters. You would also need some sort of connectivity that would enable the connection to the internet, which you’d be surprised how many people forget. Luckily, today there are all sorts of devices with connectivity on board. In case you don’t have one, BLE is also supported. And if you want to go wired, USB is your choice, however it’s a bit tricky for novices.

If you would like to run your own Blynk server, the only requirement for the hardware is to install Java 8+. For Linux we recommend using our Node.js module.

Blynk apps are running on all iPhones with iOS 8 and above and the Android app requires OS 4.0.3 and above.

We don’t have a tablet version yet, however you can still launch Blynk on iPads and Android Tablets – it will just be zoomed in.

**Does Blynk offer compatibility for different types of Linux-based hardware?**

As for Linux compatibility, we support single board computers like Raspberry Pi, BeagleBone, CHIP, Omega, and Intel boards out-of-the-box. You can also run Blynk on regular distributions like Fedora and Ubuntu, and we hope to expand this library in the near future.

The Node.js module for Linux installation would be our recommendation to use, because it proves to be way easier to implement simple projects using JavaScript, however, a pure C++ library is also available as well.

I would also like to mention that Blynk provides an installation package for OpenWRT, expanding to hundreds of Linux-based network devices.

**Is Blynk suitable for those coming across to Arduino development for the first time?**

When we started Blynk, Arduino and Raspberry Pi were the only two target platforms, and we wanted our users to be able to get first results in under five minutes. I think we did a great job with a really simple start. All that is needed is to paste the special key (we call it Auth Token) to the example code we provide, and upload the firmware to the device. After that you instantly get access to sensor data from analog inputs, and you can control digital pins and send PWM signals straight from the app. No coding is involved at all.

As you explore more features, you might need to refer to documentation or the tons of tutorials on Hacker, Instructables, YouTube and so on. Our community page is full of smart and positive folks who are always ready to help as well.

**We saw some mention of the Virtual Pins system Blynk can use, could you tell us a little more about this?**

![](img/6866071e033820549b214c239744aaa0_13_0.png)

![](img/6866071e033820549b214c239744aaa0_13_1.png)

### The wonderful world of widgets

The core of most projects created through Blynk will be primarily made of widgets. Many of the widgets already designed for Blynk offer triggers for certain features, with others connecting and syncing to your smartphone. Perhaps what makes the choice of widgets in Blynk so intriguing is that the team has also introduced a variety of sensors. So if you find your project requires the use of GPS, an accelerometer, or perhaps a gyroscope, there’s a pre-programmed widget to get it up and running. The team is planning to bring out further widgets in new updates to really start exploring some of the hardware possibilities they’ve yet to cover. We recommend heading across to the Blynk forums to see some of the unique ways that users have introduced widgets into their projects.
