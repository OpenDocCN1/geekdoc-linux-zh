requested service, so they ignore the request. The third SA, however, has information about CLE-TREE, so it sends the appropriate URL back to the UA using a unicast transmission.

![](bbox=[0.14, 0.16, 0.7, 0.39])

# FIGURE 5.5

Requesting service locations from Service Agents.

This is how your NNLS system is configured by default. It works acceptably well for small networks that have less than 25 or so servers. For networks larger than this, however, it may not be the best option. Even though SLP uses multicasts instead of broadcasts, the traffic from the multicast requests can still use excessive amounts of your network bandwidth.

If your network is large, you may need to configure one or more DAs.

# DA Mode

By implementing one or more DAs on your network, you can significantly reduce SLP traffic on your network. As discussed earlier, a DA acts as a central repository for SLP information. As in SA-Only mode, each server in the network runs a UA and an SA. Each client workstation runs a UA. In DA mode, however, you select one or more servers to run a DA as well as an SA and a UA.

When you do this, the SAs on the network change their behavior. They still register SLP-aware applications and services on their individual servers, but they no longer respond to requests from UAs.

In DA mode, SAs send out a DA discovery multicast packet when the SA is first started. If a DA responds, the SA will register all the services it knows about with the DA using unicast transmissions. After that, the SA will no longer respond to UA requests. If the SA does not discover a DA, they will default to SA-Only mode and will respond to UA requests.

In DA mode, you configure your client workstation UAs with the IP address of the DA (or DAs) you want them to send their requests to. When a UA needs to locate a service, it will send a unicast request directly to the