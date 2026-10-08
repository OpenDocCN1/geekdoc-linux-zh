Customers are recognizing the need for management tools, and enterprise management framework providers — such as Hewlett-Packard, with its IT/Operations (IT/O), and Computer Associates, with its Unicenter TNG — are feeling pressured to provide low-cost alternatives. Both HP and CA have announced intentions to bundle low-cost versions of their software with HP-UX servers. Enterprise SyMON is a low-cost management station available on Sun systems, but because it currently lacks a developer’s kit, it is not a true monitoring framework.

According to a recent Network Computing Review of enterprise frameworks, the products “...are as complex as the problems they are meant to solve.” Monitoring frameworks can be difficult to set up and are very expensive, but the benefit is that you can monitor heterogeneous components and systems through a common interface.

This chapter describes some of the frameworks available for UNIX fault management. It identifies some of the monitoring capabilities provided or available with each framework. Hopefully, these descriptions will help you to determine which framework, if any, is best for your environment.

You may need to use multiple monitoring frameworks in your environment. Chapter 9 briefly describes how to integrate different combinations of these tools.

# Distinguishing Monitoring Frameworks

We have selected a variety of frameworks to discuss in this chapter. Each has different strengths and weaknesses. Describing all the available products would be difficult, but this chapter should give you insight into the capabilities you should expect from any product that you choose to evaluate. This chapter is meant to give you a very high-level overview of features; later chapters go into more detail on product differences.

For each product, we describe its breadth of monitored components, general monitoring features and capabilities, ease of setup, approach to extensibility (developer’s kits), notification flexibility, and diagnostic capability. These attributes are generally described in this opening section.

# Monitored Components

Each product’s breadth of coverage is described in this chapter. You should ensure that all the components that you need to monitor are available before you select a framework. Some products, such as CA’s Unicenter TNG, have a smaller set of metrics available than other products, such as BMC PATROL with its set of Knowledge Modules (KMs).

# Monitoring Features

This section on monitoring features describes the framework’s general monitoring capabilities, making special note of any unusual capabilities, such as IT/O’s event-correlation capability.

# Monitor Discovery and Configuration

The first step toward actually using a monitoring framework is to determine its set of available resource monitors. The methods of doing this vary depending on the framework being used.