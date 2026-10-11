# How I made:
RasPiViv

How can you keep poison dart frogs cozy?

![](bbox=[0.11, 0.12, 0.33, 0.24])

**So, what do you keep in the vivarium?**
Right now I have seven poison dart frogs – they’re frogs from South America that, in the wild, excrete poison alkaloids, but in captivity, because their diet is just fruit flies, they can’t produce any poison. They’re something I’ve been interested in for quite a long time. I think I saw them first when I was in grade school at a trip to the Denver zoo, and I just thought they were the coolest animals I’d ever seen in my life. I’ve wanted to keep them since then but the opportunity never came up – they’re kinda rare – until I found a breeder on CraigsList who has an incredible collection and he breeds them to support his hobby. So right now I have a total of seven: two blue poison dart frogs, which I think could be a breeding pair, and I recently obtained five yellow-banded poison dart frogs.

**What kind of requirements do you have for the vivarium, then?**
The temperature is really important, which a lot of people have trouble with because your house temperature is going to be about the same as an enclosed box, give or take, as lighting can heat things up. But you have to maintain specific temperatures between about 75 and 85 degrees. The humidity is even more important because the frogs use it to thermoregulate similar to how we sweat.

So basically, what I needed was a way to monitor and regulate the humidity. I looked around online for a couple of days trying to come up with a solution – a lot of people use little timers, and there are a couple of systems that are made for this but they don’t do very much.

**What hardware did you use to make your own solution?**
Well, the Raspberry Pi is set up as a LAMP server. I started playing around with the DHT22 temperature-humidity sensor – originally I just wanted to monitor that, the temperature and the humidity, but then I got into using relays to control the lighting and it just progressed further and further. I was just making this for myself and I posted on a forum. Then a lot of people seemed really interested, so I said I’d clean things up and throw together a guide (see www.raspiviv.com).

So the temperature and humidity sensors are read every 60 seconds and logged into a database. Using WiringPi and Adafruit’s DHT22 sensor (and the driver for it, which works really well), lighting is controlled by regular relays or relay modules, and the fan is just a basic transistor switch. The main idea behind the fan is that the atmosphere is too saturated with water than the frogs can’t thermoregulate. So the database is read every five minutes, and when it reaches 95% humidity it then kicks on the fan to blow in some fresh air.

**Do you SSH in to control all this or do you have a web interface?**
Yeah, there’s a whole web interface where you can check out the current readings. Check out the Demo section on my website and the first thing that pops up is my blue poison dart frog vivarium. It gives you the current temperature and humidity, and the readings for the last hour. If you click on the icon that looks like a grid of buttons (manual controls), you can manually control your lighting, any misting system or fans you have – essentially, for any component that you want to control, it’s just a matter of getting a relay module and wiring it up.

**Are you planning to upgrade the RasPiViv software at any point?**
I hope to. I started work on this in my downtime and got insanely busy, so unfortunately I haven’t been able to do a lot with it. I’m hoping to get some RF power outlets soon so that, rather than wiring up a little power outlet box, you can just use these prebuilt outlets that you plug into your wall. I am hoping to implement some wireless stuff and I’d definitely like to make it more user friendly, rather than people manually adding cron jobs to things. I’d like them to be able to do it through the browser interface, stuff like that.

What you don’t see in the demo is that there’s also a login system – you can make an account and keep it secure – so I want to give people that and I’ll run a tutorial for setting it up. I’ve been playing around with the Raspberry Pi camera module and hoping to include it, so now we have a Raspberry Pi that is a lot more capable, it could potentially put off some kind of live camera that you can watch as well as all the other stuff that it does.

![](bbox=[0.82, 0.31, 0.92, 0.36])

### Nate Bensing
Is a marketing consultant, photographer and graphic designer for Wharton Design in Northern Colorado. He enjoys learning about electronics, creating automation projects, and contributing as much as he can to the Raspberry Pi and Linux communities that have made all this possible.

### Like it?
Fancy building your own Vivarium controls? Check out the excellent step-by-step guide on Nate’s website that takes you from NOOBS to the humidity regulation cron job. (bit.ly/HTHyvK).

### Further reading
Looking for more inspiration for sensor-driven projects? There are some great ones featured on The Raspberry Pi Foundation blog, like this Feeder and the PIPlanter. bit.ly/1A5c7mu.

![](bbox=[0.35, 0.7, 0.79, 0.91])

**Left:** The RasPiViv web interface shows you the temperature and humidity readings over time