
# Forward

Bernard Golden, Navica

Open source software is a hotbed of innovation. Because the source code of a product is available for inspection and modification, users have the opportunity to change and extend the open source products they use.

Using the released version of a product as a foundation, open source developers can implement new functionality important to them and their organizations. Rather than being forced to live with the limitations of a product, open source users can improve it and make it better suited to their needs. They can even submit their code changes to the project managers for inclusion in the main code of the product, ensuring that subsequent releases of the product will already include their changes, easing migration to newer versions of the product.

Because open source evolves so rapidly through user extension, it's critical for open source developers to adhere to standards for interoperability between applications. With the use of standards-based integration mechanisms, applications can evolve independently at their own pace, yet still be assured of being able to operate with other products.

A vibrant example of this open source characteristic can be seen in the Linux® desktop. Dozens of products are shipped in a Linux distribution, progressing according to specific project goals and on project-timelines; however, products are able to interoperate based upon standards.

The innovation and creativity of open source can be seen in the diversity of products. While Firefox is a very well-known open source browser released by the Mozilla Foundation, there are several other browsers included in a typical distribution, each focused on delivering an Internet experience in its own fashion.

This combination of rapid evolution, use of standards, and richness of alternatives is in direct contrast to the practices of the proprietary software world. In the proprietary world, vendors attempt to provide an integrated, sole source, single alternative software offering. Standards are often bypassed or only loosely implemented; the vendor focuses on owning the entire stack; enabling other offers conflicts with its business model.

While the convenience of an integrated, closed single offering can seem quite beneficial, it inevitably begins to fail under the stress of growth. As the vendor attempts to add more products to the integrated software stack, each of which must be integrated and delivered in a bundled offering, delivery dates begin to recede into the far distance, repeatedly delayed to allow each product in the bundle to be completed. To draw an analogy, integrated offerings resemble a convoy of ships, with progress to market paced by the slowest vessel.

The benefits of open source development seem quite obvious in comparison to the slow-moving convoy that is integrated proprietary software.

However, the embarrassment of riches that is open source development can pose problems as well. The innovation and experimentation characteristic of open source leads to situations like the challenge of the current Linux desktop: two strong efforts — KDE and Gnome — are strongly represented in user usage. Each provides its own way of enabling software applications to interact with the desktop environment.

While users are well-served by being able to select which desktop best suits their needs, Independent Software Vendors (ISVs) are faced with a dilemma: one or the other, or double invest to support both. In a world where Linux desktop holds a small market share, this dilemma inhibits ISVs from supporting the Linux desktop at all. Clearly, if the Linux desktop is to achieve its potential, software applications are critical.

Based on this, the Portland Project¹ was born. The Portland Project represents an initiative by both the KDE and Gnome developers to create a common set of application interfaces — a de facto standard — that application writers use to ensure that a single version of their application will run in both environments.

The Portland Project provides a common set of tools that application writers can make use of to ensure application portability. Each of the desktops can continue to evolve, adhering to a set of interfaces enables application vendors to achieve low-cost portability. In this way, the Portland Project supports the open source characteristics of innovation and integration through standards.

Open source on the desktop faces a number of challenges, and the desktop development community is focused on working through them in a methodical way, with an end goal of enabling the Linux desktop to be a convenient, inexpensive, and easily-used computing environment.

> Chief Executive Officer, Navica

Bernard is a recognized authority and consultant on the use of open source software, particularly in enterprise settings. He is the author of Succeeding with Open Source², which is used as a course text in a dozen university computer science and business programs throughout the world.

¹ http://portal.freedesktop.org/wiki/
² Succeeding with Open Source, by Bernard Golden (Addison-Wesley Press, 2005):
http://www.navicasoft.com/pages/overview.htm

# Greg Kelleher, IBM

The Open Desktop community is defined by the people involved. It is a world-wide community of individuals who share a deep passion for technology and frequently a great sense of humor as well. They are individuals who thrive on collaborating with their peers in the Open Source Software community, accomplishing real progress toward creating and delivering technical innovations, and in freely sharing the value of those innovations with the rest of the world. Those innovations — coming from the highly cohesive efforts of the technology focused sub-groups within the Open Desktop community and their passion to create something new and highly flexible — are the source of the momentum that drives this migration book project, as well as every other Open Desktop project.

This second version of the Linux Client Migration Cookbook is intended to help the Open Desktop community continue to move forward — to enable more people to grow the community by leveraging the amazing work happening right now in Open Desktop development around the world. More than anything else, those individuals and sub-groups within the community — who are working diligently on printing, GUI design, power management, sound, multimedia, GNOME, KDE, x.org, the kernel, drivers, applications, internationalization, fonts, sound, accessibility, Laptop support, and so forth — are the heart and soul of the Open Desktop community. What exists is the Open Desktop community's passion for a new and highly flexible client platform. There are no solo players or rock stars that I want to shout out. Instead, my deepest respect and thanks goes to all of the contributors within the Open Desktop community.

> — Greg Kelleher
Senior Program Manager, WW Linux Strategy and Market Development
IBM Corporate Linux & Open Source

# Preface

This second version of the Linux Client Cookbook builds on the content strategy we started with the first version. Although anyone interested in using Linux on the desktop could benefit from different portions of this book, our primary audience for this book is existing business IT environments that need to begin an evaluation of desktop Linux.

For this version, our goal was to complete an end-to-end refresh of existing content, and add as much new content as possible. Some key areas that we have focused on the following:

- The future viability of desktop Linux strategies is starting to brighten considerably. A key reason for that is that the desktop developer communities have started collaborating on projects and standards in a way that is now achieving unprecedented levels of cooperation. We highlight that in the Forward section of this book, as well as a new section in Chapter 1: 1.7, "Desktop Linux futures" on page 7.
- We have added keys to the book focus on illustrating the differences between Linux and Windows®. See 2.3, "What makes Linux different" on page 42, and this new chapter: Chapter 5, "Linux architecture and technical differences" on page 109. When coming from a Microsoft® Windows orientation, these sections will provide important technical background for readers in understanding why a strategy based on open software and standards can yield so many new, different, and potentially more efficient ways to design, deploy, and manage client computing systems.
- Once you settle on an online computing strategy you still have to deploy it. Because of the extreme flexibility of the Linux software stack, IT organizations will have many options for how to design their deployment model. When migrating from Windows based environments, often the best way to approach this process will be to step back and evaluate whether or not makes sense to continue a strategy of providing users with dedicated high powered computers, running operating system images that by default have many applications loaded than they actually need. We have focused on adding content that illustrates the flexibility we have in Linux for designing operating system images and deployment models for these images. The Multi-Station computing deep dive provided in section 7.5, "Multi-station client architecture" on page 162 and in Appendix D.
