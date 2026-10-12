To enable SWAT in Red Hat 6.0, the technology department used the “inetd” method, which doesn’t require a Web server. Under this method, the various components of Samba can be configured and maintained via a Web browser. Though Red Hat 6.0 provides Samba and SWAT, the system administrator must configure it.

The Samba Web Administration Tool provided considerable challenges to the relatively new Linux network managers. When installing Samba 2.05, the installation program automatically puts an entry in the system’s inetd.conf file.

When configuring Samba, the administrator must open the configuration file and remove the comment symbol (#) in front of the SWAT entry in this file. Removing the comment allows Samba to be called during the system initiation process.

Next, the administrator must enter swat as a service in the system services file. The name of this file is simply services and it lives in the /etc directory. Using a text editor, the administrator opens the files and locates a section where the port numbers allow for a “900” series entry. The entry that SWAT requires in this configuration file is swat 901/tcp #swat.

Once the entry is made, the administrators must restart the services for the changes to take effect. By using the command /etc/rc.d/inet.d/inet restart the system enables SWAT for use. On execution of this command at the root user’s command-line prompt, he or she will see a series of entries similar to those seen on booting the computer. Then the administrator can open his Web browser and access the SWAT interface.

The administrators typed http://localhost:901 and the SWAT interface opened in the browser. A sense of astonishment usually accompanies the first site of the SWAT interface and in Centennial’s case, this occurred.

Suddenly, light could be seen at the end of the proverbial tunnel. The small group consisting of Dave and his team became even more intrigued with the remote administration possibilities when they went to a workstation in another room and accessed SWAT from a remote browser.

Once the administrators configured Samba on Centennial’s Compaq server, they enabled printing services for their Windows workstations.

# Global Printing Services Using Samba

The Linux administrator configured a Public directory on the Samba server. The administrator created a public share and private shares on a per-user basis, and gave all users access to a shared printer controlled by the Samba server. This allowed one computer with the Linux operating system to provide shared Samba printing along with other services, such as secure Web services and user authentication to access the network.