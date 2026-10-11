You need to learn more about how you can harden the user spaces. You can use different hardening tools and applications to do this. A common option is to use a compiler flag when you build a tool or application. This is especially true if you use the kernel to launch the application. You can add additional features to the application or tool if you need to. It is important to remember that these additional features can be added to all applications on the server, not just the operating system's official apps.

# ## Using Secure Boot

When Linux developers launched Ubuntu, they included a secure boot to the operating system. The developers added the secure boot option, enforced it in the bootloader, and switched on the kernel's non-enforcing mode. With this setup, the versions that could not authenticate secure boot failed to boot, and the kernels did not validate the authentication, either.

# ## Setting Up Two-Factor Authentication

If you want to add an additional protection layer to your server, you can set up multi-factor or two-factor authentication on the server. You need to be careful about setting this up, because you can lock yourself if you incorrectly enter the password. To do this, follow the steps below:

+   **Step One**
+   Access the server through SSH and run the following command to use Google as your authentication mechanism.
+   
+       apt-get install libpam-google-authenticator

+   **Step Two**
+   You should now run the command google-authenticator to create a secret key in your server's home directory .
+   
+   google-authenticator

*Do you want authentication tokens to be time-based (y/n)* y

*Your new secret key is: 73GRSXVJNUXZWN2T*

*Your verification code is 389485*

*Your emergency scratch codes are:*