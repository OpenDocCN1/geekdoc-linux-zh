Though the PowerCLI product has grown over the various releases, there still will come a time when you won't find a cmdlet to do the task you have in mind. That's when you start looking at the vSphere APIs. These APIs give you full access to all the vSphere management components. Working with the vSphere APIs might appear to be an obscure black art, but rest assured, once you find your way around, you will find them easy to use.

Now, would you write a book on PowerCLI bother with the vSphere API? The answer is simple. With the help of the vSphere API, your scripts can get that extra mile. The PowerCLI cmdlets cover a large part of the functionality that's available in a vSphere environment, but not everything. There are, for example, properties that you cannot retrieve or get through the PowerCLI cmdlets. And that's where the vSphere API comes in. Luckily, the PowerCLI developers realized from one day that it would be difficult to offer a product that could only do part of the job. That's why they provide access to the vSphere API through specialized cmdlets Get-View and Get-VObject.

This chapter will show you how to use the vSphere API to perform functions that otherwise not be available to you.

# Work with the vSphere SDK

The full name of this beast is the vSphere Web Services SDK, but most of the time we will refer to it as the vSphere SDK or just the SDK. While the SDK is a collection of documents, Web Service Definition Language (WSDL) files, Java libraries, and sample, we will most of the time refer to one specific document, the vSphere API Reference. This reference document provides all the information concerning the data structures that are available through the vSphere API. This section provides a short summary of how the vSphere Web Services are implemented and how you can use them from your PowerCLI scripts.

# WANT TO KNOW MORE?

This chapter only scratches the surface of what is available in and what you can do with the vSphere Web Services. The summary should be enough to give you a rough idea of how the web services work. If you want to delve deeper, consult Steve Jin's excellent book VMware VI and vSphere SDK (Prentice Hall, 2009).