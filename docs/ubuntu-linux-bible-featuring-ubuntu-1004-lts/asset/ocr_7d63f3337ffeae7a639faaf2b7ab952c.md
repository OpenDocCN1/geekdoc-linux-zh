# Part III: Ubuntu for System Administrators

+   - **Local delivery only:** The machine only delivers mail locally, and does not send mail over any network. This is the right choice if you are setting up a system on which you want system status messages to be delivered by local e-mail, or a system shared by multiple users who need to exchange mail only between themselves.
- **No configuration:** The installation process will not modify the generic Post configuration files. You will have to make extensive manual modifications to them to get Postfix to work correctly on your system.
- **Satellite system:** This machine does not receive mail and forwards all outgoing mail to another mail server for actual delivery.

If you are setting up a system that doesn't match any of the pre-supplied configurations, it's probably best to select the default value, *Internet Site*, because this will provide a reasonable template that you can customize to match your requirements.

During the installation process, you will see a screen like the one shown in Figure 30-1 if you are installing Postfix and friends via aptitude. (You'll see a similar screen if you're using Synaptic or Adept, but of course—it is graphical).

FIGURE 30-1
Available Postfix configuration models

![](bbox=[0.091, 0.513, 0.613, 0.786])

This screen displays the different configuration models that are are built into the Postfix package. In most cases, you will want to select the default configuration model, Internet Site, by pressing Tab to move the cursor to the OK option and then pressing Return. You can also use the up/down arrows to select another configuration model, press Tab to move the cursor to the OK option, and press Return to accept the highlighted choice. The screen in Figure 30-2 displays this.