# Why use enterprise management tools

Just like you need to automate certain tasks when using other operating systems, it is also advantageous to do this when using Linux. Red Hat and Novell SUSE both provide options for automating client management tasks. These tools and a few others are introduced and discussed in this appendix.

You might might not have used these tools, but you might want to consider their use when you migrate to Linux. These system management services enable a client or set of clients to be configured and remotely monitored using optionally available management frameworks or applications. In the case of client deployments based on Red Hat Linux and the RHN management framework, or SUSE Linux Enterprise Desktop and the Novell ZENWORKS framework, the management tools provide a set of key value-added options that can easily justify the subscription-based licensing fees.

The availability of enterprise management tools and how you plan on using can strongly affect the cost justification models in a migration scenario. This is discussed in 2.1.2,"Costs relate to Linux" on page 32.

# Internet standard technologies

There are published Internet standards that support community development of system management tooling. There are currently many active open source management tooling development projects that are based those standards. In the case of Web-Based Enterprise Management (WBEM), the goal is to provide a platform for unifying the management of distributed computing environments.

# Web-Based Enterprise Management (WBEM)

Web-Based Enterprise Management (WBEM) and the Common Information Model (CIM) are the object-based architecture standards and the data model promoted by the industry consortia Distributed Management Task Force (DMTF). The WBEM services described here are implementations of these standards. More information about these standards, refer to the DMTF Web site:

http://www.dmtf.org

WBEM services are made available for use by a system application through a CIM object manager or CIM server. Providers are written that gather and manage system resources. These providers register their classes with the CIM server to enable these objects to be used by a management application or even other providers. There are increasing number