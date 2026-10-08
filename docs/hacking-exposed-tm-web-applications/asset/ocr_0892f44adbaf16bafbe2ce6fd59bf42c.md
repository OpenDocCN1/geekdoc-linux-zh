# Chapter 1: Introduction to Web Applications and Security

| Data | Data |
|---|---|
| Application | Application |
| Service | Service |
| System | System |
| Network |

**Figure 1-2.** A layered model for network, system, service, application, and data-related vulnerabilities

housekeeping issues such as packet reassembly, and on through what we call the services layer where servers like the HTTP daemon live, through application logic, and finally to the actual data manipulated by the application. At any point during the path, a vulnerability existence in one of the layers could be exploited to cause system or network compromise.

However, over the OSI model, the abstraction provided by lower layers gives the appearance of communicating logically over one continuous medium. For example, a properly implemented attack against an HTTP server would simply ride unobtrively through the network and system layers, then arrive at the services layer to do its damage. The application and data layers are none wiser, although a successful exploit of the HTTP server may lead to total system compromise, in which case the data is owned by the attacker anyway.

Once again, our focus throughout this book will primarily be on the application layer, with occasional coverage of services like HTTP. We hope this clarifies a bit going forward.

# ## The Web Application

The core of modern Web site is its server-side logic (although client-side logic embedded in the Web browser still does heavy lifting). This so-called “n-tier” architecture extends what would normally be a previously unsophisticated thing like a HTTP server and turns it into a dynamic engine of functionality that almost passes for a seamless, stateful application that users can interact with in real time.

The concept of “n-tier” is important to an understanding of a Web application. In contrast to the layer presented in Figure 1-1, the Web app layer itself be comprised of many distinct layers. The stereotypical representation is three-layered architecture, comprised of presentation, logic, and data, as shown in Figure 1-3. Let us discuss each briefly.

The presentation layer provides a facility for taking input and displaying results. The logic layer takes the input from the presentation layer and performs some work on it (perhaps requiring the assistance of the data layer), and then hands the result back to