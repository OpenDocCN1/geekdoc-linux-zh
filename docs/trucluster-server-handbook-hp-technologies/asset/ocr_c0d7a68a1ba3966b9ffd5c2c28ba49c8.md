![](bbox=[0.254, 0.084, 0.735, 0.374])

# **Figure 24-7: CAA Informational Popup**

In our simple application resource we will take all of the default values except that we will add a resource description (the DESCRIPTION profile attribute). After adding the text for the resource description, click the **OK** button – this will return you to the Resource Setup popup window (Figure 24-5). Click the **OK** button again and the resource will be created (see Figure 24-7).

You will then be prompted to register the resource as shown in Figure 24-8.

There will be another informational popup letting you know that the registration was successful. It will look similar to the one shown in Figure 24-7 before the reminder to start the resource (the far right popup in Figure 24-8).

# 24.9.1.2    Modify the Action Script

Before we can start the “memberUP” resource, we need to make a couple of minor changes. The application that we chose to use — xhostname — is a typical X Window System application that is designed to run in the foreground; therefore we will need to modify the action script to launch xhostname in the background. Failure to do this would result in an action script timeout and would return an error to the resource manager, a condition that should be avoided. Furthermore,

![](bbox=[0.132, 0.765, 0.878, 0.898])

# **Figure 24-8: CAA Resource Registration Popup and Start Resource Informational Popup**