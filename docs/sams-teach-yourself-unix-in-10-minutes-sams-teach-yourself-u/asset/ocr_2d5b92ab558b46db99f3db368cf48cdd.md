![](bbox=[0.22, 0.15, 0.8, 0.62])

FIGURE 18.1 KDE provides several graphic network clients, including an email client.

# The .forward File

If you want email that comes to your account to automatically send itself somewhere else, you can make use of the .forward file. Not only can the .forward file be used to forward your email to another email address, but it can also be used to forward your email into programs if you want to use software to process your email.

The format of the .forward file is simple:

+   - To forward your email to another email address, create a file named .forward in your home directory. Into this file, put a single line containing the address to which you want your mail forwarded. Execute the command `chmod 644 ~/.forward` to set the permissions properly (some flavors of UNIX are particular about this), and you're done. All email coming to your account is forwarded to the new address.
+   - To forward your email into a program for automatic processing, create the .forward file in your home directory. In the .forward