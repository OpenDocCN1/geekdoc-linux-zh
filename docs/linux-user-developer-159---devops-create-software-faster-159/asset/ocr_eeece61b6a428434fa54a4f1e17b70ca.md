# OpenSource
Your source of Linux news & views

![](bbox=[0.27, 0.19, 0.93, 0.42])

Right it's not quite there yet, but Otto will soon be ideal for deployment as well as development

![](bbox=[0.27, 0.42, 0.56, 0.46])

Focus on your Application, Automate the Rest
Don't worry about what you need to build a development environment or how to deploy your application, Otto does this for you.

![](bbox=[0.56, 0.42, 0.92, 0.46])

Deployment
Otto manages your infrastructure and deploys your application to any cloud platform.

# How to use Otto
The following is an example use case for Otto, which illustrates both the development and deployment steps for a Rails application on AWS.

1  **Start your Rails project**
Initialise a new Rails application with out-of-the-box defaults:
``
$ rails new
``

2  **Compile and configure**
Otto's compile step automatically detects the type of application as Rails and then prepares Docker to manage your app's lifecycle. You can customise nearly every aspect of Otto's behaviour by writing an Ottofile.
``
$ otto compile
``

3  **Develop locally**
Otto builds and runs a local development environment, so you can easily test and make changes to your application:
``
$ otto dev
``

4  **Construct infrastructure**
Otto creates a base infrastructure according to industry best practices:
``
$ otto infra
``

5  **Build your application**
Otto packages your application and prepares it for deployment into your infrastructure:
``
$ otto build
``

6  **Deploy**
Your Rails application is converted to running infrastructure - your app is now readily available to the world:
``
$ otto deploy
``

and the idea is that you only need to customise the little differences above that. You don't need to re-code the common ground.
The second thing was deployment. Even years ago, as Vagrant 0.1 or 0.2, we got a feature request which was, 'Can I vagrant up to production?' We tried over the years to make that possible, and ultimately we found that the Vagrantfile isn't a good description of how to get something to production, because the Vagrantfile describes, for one, a lot of machine-level things that are hard to translate to something like AWS, but in addition it just describes a lot of development things that you don't want in production. So we tried a bunch of things but the one that felt the best was just recreating a whole new file - you would have your Vagrantfile for development and your other configuration for production, and it just felt weird. The main thing we're doing to address it is moving up an abstraction layer. By describing the application rather than the machine, I think we have the right configuration to do both development and production.
The third thing was microservices. Like I said, this isn't mainstream yet, but it's fast-growing. It's hard to describe all your dependencies in one Vagrantfile, and using multi-VM was too heavy for a microservice. If you have a half-dozen microservices then you're running six virtual machines, and that's going to take down a lot of basic development machines - multi-VM was never made for microservices anyway.
**A lot of people turned to Docker, right?**
Yeah, so we saw that a lot of people were trying to use Docker for development for microservices. Docker is great at packaging microservices - wrapping microservices up in a container is a great way to make it easy to run them. The main issue we saw, from a Vagrant perspective, was that using Docker didn't really

solve all the problems. You had the packaging problem solved, but the burden of what services to install and how to configure them was still on the end application developer. So if you're developing, an app, you'd have to know all the dependencies you had - which you still need to know - but then you would also have to know all their dependencies. The approach we took with Otto is that you only need to tell Otto your immediate dependencies - Otto will figure out your transitive dependencies and then it's up to that dependency to tell Otto how to install, run and configure it.
**What do you think the learning curve will be like?**
I think, from the development side, it'll be very familiar for Vagrant people. The Apple itself is different, so that will take some getting used to, but otto dev, otto vagrant up, otto dev git, is like Vagrant ssh. otto dev destroy is like vagrant destroy; there are a lot of similar things. At the same time, from the development side, Otto is going to do a lot of things for you that Vagrant developers are really going to like. It automatically finds a non-conflicting IP address and gives the machine a static IP, so you no longer need to configure networks. There's a command to get that address - otto dev address - so you don't need to remember it like you had to do with Vagrant.
The deployment side is new for us, so we've tried to build a workflow that's as easy as Vagrant. I think, though, that, unfortunately, the learning curve for Otto's going to be low. The cost of this simplicity is that Otto makes a lot of decisions for you - we fully expect that's going to make people uncomfortable. But if you're uncomfortable, and it's a legitimate reason, then we'd love to hear from you so we can encode that knowledge into Otto and make it do what make you comfortable with, if that's the best choice for the industry.

14