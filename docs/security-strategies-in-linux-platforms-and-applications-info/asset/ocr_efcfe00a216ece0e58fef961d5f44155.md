# Make Sure Security Does Not Prevent Legitimate Access

It is possible to configure too much security on a system. In the area of passwords, if the requirements are too strict, users are more likely to forget their passwords. Users will either overload administrators with password-reset requests or they will write their passwords next to their workstations. Neither situation promotes true security. In the following sections, you'll look at reasonable password policies, how they can be implemented in the shadow password suite with the change command, and how access can be regulated with pluggable authentication modules.

# Reasonable Password Policies

In an ideal world, users will change their passwords frequently. If the lifetime of a password is less than the time it takes for a black-hat hacker to decrypt the password using tools like those described earlier in this chapter, then it doesn't matter if password-authentication databases are out in the open.

Of course, you may not want to publish a password-authentication database. Black-hat hackers can get access to some powerful systems. Some companies sell rainbow tables, which can speed the process of decrypting a.

To that end, the best passwords are phrases, which can be complete sentences. But many authentication systems do not support such options as spaces in a password. Other than a passphrase, the best password is a combination of upper- and lowercase characters, along with numbers and punctuation.

With such policies, the next question is how frequently you make users change their passwords. You want users to remember their passwords without having to write them down. One U.S. governmental guideline is based on the Federal Desktop Core Configuration (FDCC), as mandated by the U.S. Office of Management and Budget (OMB). While the password guidelines allow for Microsoft Windows systems, the listed policy suggests that:

+   - Have a minimum of 12 characters
- Be changed every 60 days

While these policies do not apply to Linux systems, they are reasonable minimum requirements. On the other hand, in organizations where security is important, such as intelligence agencies, users generally have a greater understanding of the need for password security. You should be able to set more rigorous limits in such cases.

> One way to help users remember such passwords is based on a sentence. For example, a password such as OT,Is3ba1! could stand for "On Tuesday, 3 birds and 1 eagle!"

The standard for configuring password policies is based on options in the /etc/shadow file. It can be configured with the change command first described in Chapter 4. The current settings are defined in the output to the -l username command. The output and associated change command options are shown in Table 13-4.

![](bbox=[0.056, 0.915, 0.356, 0.966])