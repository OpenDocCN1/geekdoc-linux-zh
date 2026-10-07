# Chapter 8 = Hub

![](bbox=[0.085, 0.098, 0.915, 0.497])

**Figure 8.5**
A simplified reset sequence involving the hub.

process for OTG devices is part of this path you can explore to improve the sequence.
The core functionality of the hub framework is the handling of events. Figure 8.7 illustrates the flow of activities inside the khbd while handling events.
The khubd waits in an infinite loop for any hub activity, which is notified through a kick_khubd interface routine. This allows the hub to come out of the wait state and process the new event using hub_events. After successful processing, the khubd thread hub_thread again waits for new events.
This section captured the basic functionalities of the hub framework.