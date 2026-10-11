# # MakerSpace

Predicting the productivity of a solar array with Perl

# # Solar Power Leashed

A forecast service and some Perl magic help predict the solar power yield of a residential photovoltaic array. By Rubén Lorente

The current energy crisis has led many homeowners to invest in solar power. More people than ever are choosing to install photovoltaic generation systems on their rooftops for domestic use. Depending on how much money is invested on such systems, homeowners could see their power bills cut in half or even have them reduced to nothing.

Solar is not all advantages, though: Power generation represents a huge upfront investment that will take more than a decade to recoup. Another huge disadvantage, however, is that photovoltaic arrays are only productive if the weather is willing to cooperate (Figure 1).

A house equipped with a photovoltaic set (Table 1) might become truly self-sufficient, as long as it is well managed. However, to optimize the use of solar power, it is important to predict the daily power yield of the system. If you have access to an accurate forecast, you can plan ahead.

Imagine, for example, that you are planning to turn your yearly fruit yield into jam in a given week. That undertaking is an energy-intensive task. If you know tomorrow’s weather is not going to cooperate with your solar, but the day after tomorrow you will have favorable conditions, you can adjust your schedule and take advantage of the sun. On the other hand, if your photovoltaic installation is off-grid (in island mode), you will need to know in advance which days are going to be bad and how long a generator would need to run to compensate for cloudy weather.

Keep in mind that using power-hungry appliances while the sun is not shining might still make some sense. See the “Solar Power Without the Sun” box for more information.

![](bbox=[0.08, 0.62, 0.6, 0.9])

**Figure 1:** Two photovoltaic arrays provide more power than a regular house needs — but only if the weather cooperates.

# ## Solar Irradiance Forecast

Forecast services that give you an estimation of the power yield of a solar