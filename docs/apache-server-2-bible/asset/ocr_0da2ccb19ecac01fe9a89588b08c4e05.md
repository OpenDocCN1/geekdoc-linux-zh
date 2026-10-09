# Running mod_perl applications on a partial set of Apache children

When you start using many mod_perl scripts, you will notice that your Apache child-server processes become larger in size. You can witness this phenomenon by using the top command. Now, as long as you have plenty of RAM you should be fine. However, no one ever has enough RAM, and so it is a good idea to not rely on having lots of memory as the solution and to consider how you can address this problem more effectively.

If you find that Apache child processes are becoming larger and larger because many mod_perl scripts are being loaded into them, consider having a dedicated script server that only serves dynamic contents. Figure 22-6 shows how this can work.

![](bbox=[0.18, 0.36, 0.82, 0.78])

When a user requests the home page of a site called www.domain.com, the Apache server responsible for static pages returns the index.html page to the client. The page contains embedded links for both static and dynamic contents. The figure