Not previously covered in this book is the Red Hat Network (https://rhn.redhat.com—see Figure 7.4). RHN has not been covered because it is not free to the users of this book (or to users of the freely-available FTP download version) and it is limited to managing only the software that is provided by Red Hat. Other alternatives are now available.

![](bbox=[0.11, 0.17, 0.84, 0.57])

**FIGURE 7.4** The Red Hat Network provides automated update subscription services. It only works with software provided by Red Hat and is designed for commercial users.

The RHN service is a client-server mechanism through which a user subscribes to a channel on the server (a repository of software for a specific release of Fedora Core). The local client (identified by a round icon at the right of the desktop panel) can manually or automatically connect to the Red Hat Network server, obtain a list of updates, errata, and security fixes and install them; one subscription is required for each client.

> **NOTE**
> If this client-server model appeals to you and you want to use it for your network, you can sign up for subscriptions or consider one of two Open Source Up2Date server alternatives: Current at http://current.tigrr.org/, or NRH-up2date at http://www.nrH-up2date.org/index.html. These two projects are attempting to provide RHN-like services under your control so that you can use non-Red Hat and non-Fedora packages with the service. Bear in mind, though, that Fedora is in the process of deprecating up2date as a method of package management in favor of Yum.