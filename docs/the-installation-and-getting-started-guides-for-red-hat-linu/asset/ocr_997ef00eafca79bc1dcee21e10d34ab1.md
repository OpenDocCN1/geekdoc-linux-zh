password is case-sensitive. Write down this password and keep it in a secure place.

**Please Note:** The root user (also known as the superuser) has complete access to the entire system; for this reason, logging in as the root user is best done only to perform system maintenance or administration. Please see Chapter 8 for instructions on how to add a user account for yourself after you reboot your system. A more basic method of creating a new user account can also be found in the Red Hat Linux Getting Started Guide in the Welcome to Linux chapter.

# Authentication Configuration

After you have set up your root password, you will have the option of setting up different network password authentications:

+   - **Enable NIS** — allows you to run a group of computers in the same Network Information Service domain with a common password and group file. There are two options here to choose from:
+     - ✓ **NIS Domain** — this option allows you to specify which domain or group of computers your system will belong to.
+     - ✓ **NIS Server** — this option causes your computer to use a specific NIS server, rather than "broadcasting" a message to the local area network asking for any available server to host your system.

+   - **Enable Shadow Passwords** — provides a very secure method of retaining passwords for you. The /etc/passwd file is replaced by /etc/shadow which is only readable by root.

+   - **MD5 Password** — allows a long password to use up to 256 characters, instead of the standard eight letters or less.

**Please Note:** To configure the NIS option, you must be connected to an NIS network. If you are unsure whether or not you are connected to an NIS network, please ask you system administrator. Unless you are setting up a NIS password, you will notice that both Shadow password and MD5 are selected. We recommend you use both to make your machine as secure as possible (see Figure 6-17).