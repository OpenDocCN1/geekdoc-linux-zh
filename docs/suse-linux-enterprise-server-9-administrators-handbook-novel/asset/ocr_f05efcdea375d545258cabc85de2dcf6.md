We have seen in this section that we are able to control the resources consumed by an end user. Application of such measures is required only in cases of abuse, but it is good to know that this can indeed be achieved. Keep in mind that these limits are on a per-account basis and are not restricted to simple logins. Other applications that use PAM can also make use of the `pam_limits.so` module.

# Access Time Management

In many mission-critical applications, it is important to restrict application and content changes to specific well-controlled change windows. A method for enforcing such an environment is to use the `pam_time.so` module. This module allows you to control the access to specific services based on where the access is being requested from, the account requesting the access, as well as the time the request is being made.

Because you are now introducing time restrictions into the login process, you must inform PAM that this additional step is required. To do this, you must add a line to the PAM login configuration file `/etc/pam.d/login`. The new version of this file should now look like Listing 5.7.

# **LISTING 5.7**

A Typical PAM `pam_time.so` Module Configuration File

```
 #%PAM-1.0
auth requisite  pam_unix2.so       nullok       #set_secproc
auth required   pam_secure.so
auth required   pam_nologin.so
auth    required   pam_homecheck.so
auth required   pam_env.so
auth required   pam_mail.so
account required   pam_time.so
account required   pam_unix2.so
password required pam_pwcheck.so  nullok
password required pam_unix2.so    nullok use_first_pass
~use_authok
session required   pam_unix2.so    none
session required   pam_limits.so
```

Listing 5.8 shows a snippet of a configuration file for the time module `/etc/security/time.conf`. In this example, the login application is denied to users eric and hart during the evenings.