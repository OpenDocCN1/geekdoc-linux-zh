| Control flag | Description |
|---|---|
| required | If the module returns a fail status code, a final fail status will be returned to the application, but only after the rest of the modules within the configuration file run. |
| substack | Forces the included configuration files of a particular type to act together returning a single status code to the main module stack. |
| sufficient | If the module returns a success status code and no preceding stack modules have returned a fail status code, a final success status is immediately returned to the application without running the rest of the modules in the configuration file. If the module returns a fail status code, it is ignored. |

The /etc/pam.d/ configuration files' module stack process of providing a final status is a little confusing. A simplification to help you understand the progression is depicted in Figure 16.1.

# **FIGURE 16.1**   The PAM module stack process

![](bbox=[0.17, 0.5, 0.84, 0.69])

Using Figure 16.1 as a guide, imagine that the application subject (user) needs authentication to access the system. The appropriate /etc/pam.d/ configuration file is employed. Going through the authentication module stack, the user passes through the various security checkpoints. At each checkpoint, a guard (PAM module) checks a different requirement, determines whether or not the user has the required authentication, and issues a fail or success card. The final guard reviews the status cards along with their control flags listed on a clipboard. This guard determines whether or not the subject may proceed through the “System Access” doorway. Of course, keep in mind that if any of the checkpoints are listed as requisite, and the user fails that checkpoint, they would be immediately tossed out.