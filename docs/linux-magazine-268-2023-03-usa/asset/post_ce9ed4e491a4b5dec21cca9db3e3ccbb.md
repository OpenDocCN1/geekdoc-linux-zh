
it is closed again automatically a short time later. Small paddles act as the closures to avoid a shaft remaining permanently open and ensure that the desired amount of feed is delivered (Figure 4).

The 160-liter aquarium with low fish stock levels does not need more than a heaped teaspoon of dry food every day. The supply in the vending machine will be fine for a three-week vacation. If you need a larger reserve, adjust the setup to your needs in terms of diameter and height of tubes.

## Control

The feeding process starts automatically after applying the supply voltage. As specified in the Raspberry Pi crontab, the vending machine feeds the fish once a day. On Saturdays, feed is taken from the second shaft by rotating the servo at the same angle, but in the opposite direction. Once a minute the housing LED flashes a visual ready signal. To track all events on the device, the LED uses various flash codes (Table 1).

What you can’t see in the circuit diagram (Figure 5) are the two push buttons on the case, which are connected to the Zero W general purpose input output (GPIO) pins to trigger a feed in the first shaft and for a controlled system shutdown.

Because the feeder is on the local network, it can be maintained over the network, as well. To do so, log in to a terminal over SSH with:

```
ssh pi@feeder
```

You can then make changes to the crontab or control script. If needed, you can disable the automatic feeder by calling:

```
python3 /home/pi/scripts/feed.py 4
```

The 4 option tells the device to enter maintenance mode without any further actions.

## Observations

One interesting and positive side effect is the ability to see whether the fish are getting any feed from the feeder. The control script triggers a snapshot through the aquarium glass with a delay of 10 seconds after operating the servomotor. The simple Pi Cam Rev 1.3 serves this function well. Because I only need to grab an image of a section of the front of the aquarium, image quality is secondary.

The connection from the vending machine on the top of the aquarium to the Pi cam on the front of the aquarium requires a long camera cable (about 30cm for my setup) that depends on the height of the aquarium cover. A narrow aluminium plate fixes the small camera housing a few centimeters in front of the screen.

To get sharp images, you need to set the shortest possible focal length on the Pi cam. To do this, turn the adjustment ring of the small lens very carefully with a tool and grab a few test images to check the setting.

![](img/e3f454b04d121b3b3750fddfda8dd21e_59_0.png)

Figure 3: The feed tower has two separate chambers, which are operated by a mechanical system.

![](img/e3f454b04d121b3b3750fddfda8dd21e_59_1.png)

Figure 4: The outlet mechanism: Depending on the direction of rotation, feed is delivered from one of the two chambers.

**Table 1: LED Flash Codes**

| Signal | Status |
| --- | --- |
| 1x long | Live, flashed every minute |
| 1x medium | Shaft 1 opening (plus photo) |
| 2x medium | Shaft 2 opening (plus photo) |
| 3x short | Single snapshot |
| 3x very short | Shutting down |

![](img/e3f454b04d121b3b3750fddfda8dd21e_60_0.png)

three buttons, is implemented in PHP and resides in the Raspberry Pi's `/var/www` directory. The code for this and the Python script to control the feeder is on the project's GitHub page [3], and an English version is on the Linux Magazine download site [4].

To access the web interface on the local network, simply enter the local IP address of the Zero W in a web browser. To monitor the system remotely while on vacation, you need to enable the server on the Zero W in your router for the web and assign a permanent IP. However, if you already use a website with FTP access, you can alternatively upload the current feeding image to your own web space and view it there.

## Conclusions

The automatic feeder has already fed my fishy friends without any glitches during two short trips. My goal was a DIY solution from the outset, so competing with commercially available solutions was never important. Instead, I wanted to build a device optimally adapted to my own needs: one that worked reliably and allowed me to check how it was working. I definitely did not want to compromise on the care of my pets.

However, even the best Internet-based feedback is of little use if you have no one onsite who can intervene in an emergency. It’s always great to have the support of your family or neighbors to water the flowers or even take care of the pets in your aquarium if you’re in a pinch.

## Info

- [1] crontab(1) man page: https://linux.die.net/man/1/crontab
- [2] lighttpd: https://www.lighttpd.net
- [3] Project on GitHub: https://github.com/swenae/feeder
- [4] Download page for English code: https://linuxnewmedia.thegood.cloud/s/6RZx9IQW2FJ6N32

## Author

Swen Hopfe works for a medium-sized company with a focus on smart cards and near-field communication (NFC). When he is not taking photos, in the great outdoors, or in his garden, he focuses on topics such as the Raspberry Pi, Internet of Things, and home automation.

## MakerSpace

### Solar Power Leashed

A forecast service and some Perl magic help predict the solar power yield of a residential photovoltaic array. By Rubén Lorente

The current energy crisis has led many homeowners to invest in solar power. More people than ever are choosing to install photovoltaic generation systems on their rooftops for domestic use. Depending on how much money is invested on such systems, homeowners could see their power bills cut in half or even have them reduced to nothing.

Solar is not all advantages, though: Power generation represents a huge upfront investment that will take more than a decade to recoup. Another huge disadvantage, however, is that photovoltaic arrays are only productive if the weather is willing to cooperate (Figure 1).

A house equipped with a photovoltaic set (Table 1) might become truly self-sufficient, as long as it is well managed. However, to optimize the use of solar power, it is important to predict the daily power yield of the system. If you have access to an accurate forecast, you can plan ahead.

Imagine, for example, that you are planning to turn your yearly fruit yield into jam in a given week. That undertaking is an energy-intensive task. If you know tomorrow’s weather is not going to cooperate with your solar, but the day after tomorrow you will have favorable conditions, you can adjust your schedule and take advantage of the sun. On the other hand, if your photovoltaic installation is off-grid (in island mode), you will need to know in advance which days are going to be bad and how long a generator would need to run to compensate for cloudy weather.

Keep in mind that using power-hungry appliances while the sun is not shining might still make some sense. See the “Solar Power Without the Sun” box for more information.

![](img/e3f454b04d121b3b3750fddfda8dd21e_61_0.png)

**Figure 1:** Two photovoltaic arrays provide more power than a regular house needs — but only if the weather cooperates.

### Solar Irradiance Forecast

Forecast services that give you an estimation of the power yield of a solar array are great for two reasons. First, they allow you to simulate the performance of a solar array you intend to install before you make the investment. It is much better to know that the panels you intend to install are going to under perform or over perform before you spend your money. Second, they allow you to schedule your power expenditure so as to optimize the usage of your system.

A very useful forecast service free of charge for hobbyists, students, and academic research is Solcast [1]. The biggest advantage of the service is that it allows you to download solar irradiance predictions in machine-parseable formats, which can then be fed to scripts and programs to extract meaningful data.

After signing up with Solcast, you are expected to define a Site before you start using the service (Figure 3), which is just a fancy way of saying you need to provide your location to Solcast so they can send you that location’s forecasts. To complete your information on the Site tab, you need to provide the orientation angle of your panels, their nominal power output, the vertical angle of the panels, and an efficiency estimation. It is safe to assume 90 percent efficiency for new systems, with a 2 percent efficiency loss per year.

Solcast also provides an API key (Figure 4) you can use to download forecasts automatically. Your site’s page on the Solcast website will provide plenty of documentation and a wizard for generating valid HTTP calls. To save time, the following example downloads 72 hours of forecast data for the specified site:

```
https://api.solcast.com.au/rootloop_sites/$YOUR_SITE_ID/forecasts?hours=72&format=csv&spl_key=$YOUR_KEY
```

![](img/e3f454b04d121b3b3750fddfda8dd21e_62_0.png)

Figure 2: A Turbo Energy hybrid inverter (1) paired with a battery bank in a rack (2). The photovoltaic panels charge the batteries with excess production, so the owner can use battery power after the sun sets.

## Solar Power Without the Sun

Solar systems usually work alongside the traditional power grid. The idea is that the house will pull power from the solar system and, if solar yield is not enough to satisfy the demand, get as much power from the grid as necessary to have the sum of solar power and grid power equal to the load.

Solar systems only generate power while the sun is shining, but people often need electricity during off-productive hours. Two main strategies are used by homeowners to benefit from solar arrays after sunset. The first is signing a contract with a power supply company, which will buy the power you produce while you are not using it. This way, if you are not home during the day, your solar arrays will produce power for your power supply company. When you return home at night and turn on an electric stove, you will buy power straight from the grid, but the hope is that the money generated during the day will offset the cost of purchasing electricity during dark hours. This approach has the advantage of being cheap (i.e., it does not require the owner to build out a special infrastructure); however, it is more beneficial for power suppliers than for homeowners. Typically, power distributors buy your power for much less than they sell it back to you.

The second strategy is to add a battery set to the solar system (Figure 2). The objective is to have the solar arrays charge the batteries during the day so you have energy stored for when you need it. The advantage of this approach is that it is more flexible and makes you less dependent on regular power suppliers. If your area experiences regular blackouts or power (load) shedding (a temporary reduction in supply of electrical power), you will be able to use battery power. The main disadvantages are the huge upfront cost of battery banks and the increased complexity of the deployment. Also, not all solar systems equipped with batteries are black-out proof, and some will cease operating if the grid goes down because of the way they are designed.

Both strategies benefit from proper planning of power consumption. Somebody who sells power to the grid will still find it preferable to use electricity while solar is working at its best, instead of doing so at night and having to buy power – even if the costs are partially offset by the power sold earlier. On the other hand, the owner of a solar system with a battery bank will be better off using electric power at noon rather than draining energy from the battery needlessly at night.

**Table 1: Hardware Budget***

| Item | Quantity | Total Price (EUR)¹ |
|---|---|---|
| Hybrid inverter | 1 | 1,730.30 |
| Panel (450W) | 13 | 3,303.30 |
| Battery module (5kWh) | 3 | 7,314.45 |
| Total | | 12,346.05 |

- \* 5.910W photovoltaic system, wiring excluded.
- \* Prices are roughly equivalent in US dollars.
