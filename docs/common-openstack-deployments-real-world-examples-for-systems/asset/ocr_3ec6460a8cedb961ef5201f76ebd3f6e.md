# 1

What Is OpenStack?

> > *If I could remember the name of all these particles,*
> > *I would have been a botanist.*
> > 
> > Enrico Fermi

As an infrastructure project that has a variety of options available for various types of deployments, answering the question “What is OpenStack?” can take some time. Simply put, OpenStack is a series of independent, yet related, software pieces that can be used to build an infrastructure for deploying and managing servers and storage arrays of various types. These software pieces include projects for web– or API-based control, compute, networking, object storage, block storage and more.

Whole books can and have been written covering each of these components. In this chapter, we talk about some of the basics around cloud, and you are provided with an overview that will serve as a reference for the various components as you begin working on sample deployments in the next several chapters. Further detail about each component, and how it relates to the deployment you’re working on, will be provided as you go through each deployment scenario.

The Preface explained that the target operating system for this book is Ubuntu. The chapter will conclude by talking about the Ubuntu Cloud Archive, which always provides the latest version of OpenStack to each supported Ubuntu Long Term Support release as well as the Puppet modules we will use for the deployment scenarios.

# The Cloud

The term “cloud” has become very overloaded in recent years. To the layperson it may mean the place where all of their music and photos are kept where they use syncing and storage applications for their phones. A developer working for a payroll accountant may view the cloud as a platform against which applications for the financial department can be written. To a systems administrator it may specifically mean where a virtual machine, able to be scaled and deployed on demand but otherwise almost indistinguishable from any other basic server to which they’ve deployed applications, resides. This is where we get to the distinction of different “as a Service” models.