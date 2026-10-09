![](bbox=[0.73, 0.06, 0.95, 0.17])

# CHAPTER

# Creating a High-Availability Network

# In This Chapter

In this chapter, you learn about design considerations for building a Web network. A Web network is a network of Web server nodes that create a Web service. For example, Yahoo! uses a large number of Web servers, application servers, and database servers to create a multitude of Yahoo! Web services.

+   Understanding the features of a Web network

+   Enhancing DNS reliability

+   Load balancing a Web network

+   Managing Web storage

+   Creating a back-end network for maintenance

If you have decided to integrate the Web into your business, you must consider a Web solution that can grow beyond a single Web server or a shared Web drive space on an ISP. A Web network is one solution. In this chapter, you learn to use proven networking and system management concepts regarding design considerations for building successful Web network. Although the chapter focuses on Apache-on-Linux-based solutions, most of the solutions are applicable to other platforms as well.

+   Fortifying your Web network

# Features of a High-end Web Network

A high-end Web network serves thousands to millions of pages per day. To serve a large number of Web requests it must have these features:

+   ✦ **Reliable DNS servers.** If your Domain Name Service (DNS) servers are down, no one can easily access your Web sites. So, reliable DNS is a big consideration in Web network design.