
# Chapter 28 Green IT

- Equipment recycling – once or twice a year, hold equipment recycling during which staff can pile up their unwanted, unused, or underutilized equipment for your favorite recycling company to haul off. If you're really eco-friendly, let staff add equipment from home to the pile.

- Equipment life extension – once a workstation becomes too old or too slow to be used by staff with the most intense computing demands, cycle it to staff who have lower requirements. They'll see it as an upgrade, and you'll squeeze another year or two of life out of it.

- Workplace recycling – start a workplace program for used paper. Many recycling companies also accept office plastics (soda bottles, etc.) in the same stream.

- Recycled paper and printer cartridges – become a consumer of recycled goods. Purchase 100% recycled paper for your printers and copiers, and buy recycled toner cartridges as well. We've had outstanding luck with Boise Aspen 100 as general-purpose recycled paper that's inexpensive and having outstanding ecological characteristics.

- Telecommuting – encourage staff to telecomm one or more days per week by installing and supporting technologies that facilitate remote access, such as VPNs, VOIP service at home, and web-available applications. In addition to the benefits for the staff involved, telecommuting reduces the use of transportation and office support services. Make sure, though, that teleuters turn off their equipment at whichever site they're not occupying on a given day. Otherwise, this policy can carryback, from an energy conservation perspective.

## 28.5 GREEN IT FRIENDS

If you're looking to do even more in the green IT space, you can find camaraderie and guidance from a variety of organizations and resources. Table 28.2 lists some of the groups that we are familiar with and recommend.

Table 28.2 The green mafia

| Organization | Web site | Description |
|---|---|---|
| Energy Star | energystar.gov | Consumer product standards |
| EPEAT | epeat.net | Green electronics manufacturing |
| French Green IT | greenit.fr | French Green blog |
| Green IT Observatory | greenit.bf.rmit.edu.au | Australian green IT research |
| Green IT Promo Council | greenit-pc.jp | Green IT for Japan and Asia |
| Green Standards Trust | greenstandards.org | Office equipment recycling |
| IT Industry Council | itic.org | General best practices for IT |
| Less Watts | lesswatts.org | Saving power for Linux |
| The Green Grid | thegreengrid.org | Data center focus |

## 28.6 EXERCISES

- E28.1 Use a Watt meter to measure the power consumption of your desktop workstation under various load conditions, including sleep mode or power-save mode. How much power would be saved if you turned your workstation off every night?

- E28.2 Write a script that emails the system administrator when CPU load indicates that a new server should be spun up.

- E28.3 Make a list of the main applications that your organization uses. Which ones have overlapping functionality?

- E28.4 Visit greengrid.org and determine if your location could benefit by using outside air for cooling.

- E28.5 Organizations such as TerraPass and Carbonfund.org CO2 "offsets" through which organizations can compensate for their carbon emissions. For example, one common strategy used by offsetters is to subsidize the development of carbon-neutral energy sources (e.g., land and wind power), with the goal of reducing emissions.

These programs proved controversial. Some observers doubt the reality of the claimed emission reductions, while others question the programs on philosophical grounds.

Select a specific carbon offset provider and assess the plausibility of the strategies it is pursuing. Are the programs sufficiently well documented that you could make your own evaluation of their quality? Has any impartial group evaluated this provider, and if so, what were their conclusions?

> WordPress developer Mark Jaquith wrote, "It's like killing a person, and then convincing a murderer to kill one less person. You didn't negate your murder. Convincing someone else to reduce their emissions doesn't make up for your emissions." We don't necessarily endorse this view, but it is representative the anti-offset perspective.

# 29 Performance Analysis

Performance analysis and tuning are often likeneded to system administration witchcraft. They're not really witchcraft, but they do quite qualify as both science and art. The “science” part involves making careful quantitative measurements and applying the scientific method. The “art” part relates to the need to balance resources in a practical, level-headed way, since optimizing for one application or user may result in other applications or users suffering. As with so many things in life, you may find that it's impossible to make everyone happy.

A sentiment widespread in the blogosphere has it that today's performance problems are somehow wildly different from those of previous decades. That claim is inaccurate. It's true that systems have become more complex, the baseline determinants of performance and the high-level abstractions used to measure and manage it remain the same as always. Unfortunately, improvements in baseline system performance correlate strongly with the community's ability to create new applications that use all available resources.

This chapter focuses on the performance of systems that are used as servers. Desktop systems typically do not experience the same types of performance issues that servers do, and the answer to the question of how to improve performance on Performance Analysis a desktop machine is almost always "Upgrade the hardware." Users like this answer because they get fancy new systems on their desks more often.

One of the ways in which UNIX and Linux differ from other operating systems is in the amount of data available to characterize. Detailed information is available for review. Many applications can be tuned to yield tremendous performance improvements. However, performance tuning isn't easy. One of the ways is to check the configuration of the system and of individual applications. In all cases, you may find that it's impossible to make everyone happy.

As in physics, the more information you collect with monitoring utilities, the more you affect the system you are observing. It is best to rely on something simple and lightweight that runs in the background (e.g., sar or vstat) for routine observation. If those feelers show something significant, you can investigate with other tools.

- Tune your system in a way that lets you compare the current results to the system's baseline.

- Always sure you have a rollback plan in case your magic fix actually things worse.

- Don't intentionally overload systems. The kernel gives each process the illusion of infinite resources. But once 100% of the system's resources are in use, the kernel has to work hard to maintain that illusion, delaying processes and often consuming a sizable fraction of resources itself.

- Collect and review information:

- Ensure the system has enough energy. As we see in the next section, memory size has a major influence on performance. Memory is inexpensive these days that you can usually afford to load every performance-sensitive machine to the gills.

- If you are UNIX or Linux as a web server or some other type of network application, you may want to spread traffic among systems with a commercial load balancing appliance such as Cisco's Content Services Switch (cisco.com), Nortel's Alteon Application Switch (nortel.com), or Brocade's ServerIron (brocade.com). These boxes map several physical servers to be one logical server to the outside world. They balance the load according to one of several user-selectable algorithms as "most responsive server" or "round robin".

These load balancers also provide useful redundancy a server go down. They're really quite necessary if your site must handle unexpected spikes.
