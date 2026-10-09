# Setting up for the Web cycle

You can set up for the Web cycle in two ways: you can either use two new virtual hosts to implement the development and staging sites on your production server, or you can create three separate Apache configurations for the production server, the development server, and the staging server.

If your development work includes tweaking Apache configuration files or testing a newly released Apache server, you should use separate configuration files for the production Apache server and the other two Apache servers. If your normal Web development does not include Apache-related changes, however, you can use the virtual host approach.

A good Web cycle requires a well-planned Web directory structure. Figure 11-2 shows one such directory structure for a Web cycle.

![](bbox=[0.18, 0.39, 0.58, 0.66])

**Figure 11-2:** The directory structure used for public, staging, and developer sites for “my company”

This figure shows a good example of a directory structure because it enables you to keep the public, staging, and developer sites for each Web site under a single top-level directory (in this case, mycompany). Adding a new Web site means creating a similar directory structure for it.