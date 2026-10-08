72 Managing Threats, Vulnerabilities, and Risks

# Availability

Are you still wondering about the value of knowing the MTBF and the MTTR? Well besides the benefits mentioned earlier, you can also use them to calculate the availability of your service.

This is a very interesting metric that you can use to report the status of your systems to the upper management and justify any previous and future investments. For example, let's imagine that your web server went down twice in the last 400 days (MTBF = 200 days) and that the MTTR was 3 hours (MTTR = 0.125 days). Therefore, if the device failed every 200 days and it took 0.125 days to get restored, then it means that availability is equal to 200 / (200 + 0.125), which means that, in this case, the availability of our web server is 99.375%.

Availability = MTBF / (MTBF + MTTR)

Now, is your 99.9375 good? Well, that determines your business. However, data centers use a Tiers approach to determine their level of availability, so you can use those values as a point of reference:

+   * Tier 1: 99.671% availability (this is equal to 28.8 hours of downtime annually).

+   * Tier 2: 99.741% availability (this is equal to 22 hours of downtime annually).

+   * Tier 3: 99.982% availability (this is equal to 1.6 hours of downtime annually).

+   * Tier 4: 99.995% availability (this is equal to 26.3 minutes of downtime annually).

> Tip
are you looking for a way to objectively support the decision about having solution hosted in-house or with a third party? Well, you can analyze the current availability, and contrast against the availability offered by the vendor to determine which solution is best for your business.

A good way to enhance the availability of your infrastructure is by finding the devices that could jeopardize the uptime of your systems and infrastructure. Those devices are known as single points of failure.

# A single point of failure

As mentioned earlier, a key aspect to enhance the availability of your systems and infrastructure is by identifying the critical devices that could impact the uptime of systems. Once identified, you must ensure that these systems have the highest level of security to reduce the risk associated with them, and as you probably guessed, devices must have the lowest MTBF and MTTR.