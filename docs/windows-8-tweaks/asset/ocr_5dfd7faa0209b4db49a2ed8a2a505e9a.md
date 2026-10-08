Changing the UAC settings is easy to do with the Local Security Policy editor. Just follow these steps to modify the settings:

+   1. Open the Start screen, type secpol.msc, and hit Enter.
2. After the Local Security Policy editor loads, expand Local Policies and click Security Options.
3. Scroll to the bottom of the list to see all the UAC security policies. Right-click a policy and click Properties to modify it.
4. When finished, click OK to save the changes.

As you can see, editing the User Account Control's settings is very simple. If you are fed up with the UAC and want to disable it completely, all you need to do is set the User Account Control: Behavior Of The Elevation Prompt For Administrators In Admin Approval Mode and User Account Control: Behavior Of The Elevation Prompt For Standard Users policies to No Prompt and you will no longer have any annoying prompts. However, you will have just killed one of the best security features in Windows 8. That is why I believe that it is still possible to use User Account Control while decreasing some of the annoying prompts. The next section shows you how to configure UAC settings for a good balance.

# Compromising Between User Account Control and Security

Although many people want to disable UAC completely, I am against this because of the added security it provides to Windows 8. Instead, I like to configure my computer in a way that I can get the best of both worlds—being able to install applications and freely configure Windows settings without getting bothered with UAC prompts, while still getting the security of UAC. How is this possible? Use two accounts!

All too often people use their computer logged on with a user that is a member of the Administrator group. They do this accidentally or without even knowing it because when an account is created as part of the end of the Windows 8 setup, it automatically adds it to the local Administrator security group. The end result is a situation in which you have to be treated as a standard user and authorize every single change to secure the system. I offer a better solution to secure the system that greatly reduces the number of prompts you see. This set up is very simple and easy to use after you get the hang of it.

This is how it works: You have two accounts on your machine. One for day-to-day use that is a low-rights, standard user account with UAC running, and another account that has full admin rights with UAC disabled so that you can easily install and change system settings with it when needed.