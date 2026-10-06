# Username Field

This field is also referred to as the login field or the account field. It stores the name of the user on the system. The username must be a unique string and uniquely identifies a user to the system. Different sites use different methods for generating login names.

A common method is to use the first letter of the user’s first name and append the user’s last name. This usually works, because the chances are relatively slim that an organization would have several users with the same first and last names. For example, for a user whose first name is "Ying" and whose last name is "Yang," a username of "yyang" can be assigned. Of course, several variations of this method are also used.

# Password Field

This field contains the user’s encrypted password. On modern Linux systems, this field contains a x to indicate that shadow passwords are being used on the system (discussed further on, in this chapter). Every regular user or human account on the system should have a password. This is crucial to the security of the system—weak passwords make compromising a system just that much simpler.

# How Encryption Works

The original philosophy behind passwords is actually quite interesting, especially since we still rely on a significant part of it today. The idea is: Instead of relying on protected files to keep passwords a secret, the system encrypts the password using an AT&T-developed (and National Security Agency-approved) algorithm called Data Encryption Standard (DES) and leaves the encrypted value publicly viewable. What originally made this secure was that the encryption was computationally difficult to break. The most folks could do a brute-force attack, where automated systems would iterate through a large dictionary or on the natural tendency of users to choose English words for their passwords. Many people tried to break DES itself, but it was an algorithm that anyone could study, and it was much more bulletproof before

When users entered their passwords at a login prompt, the password they entered would be encrypted. The encrypted value would then be compared against the user’s password entry. If the two encrypted values matched, the user was allowed to enter the system. The actual algorithm for performing the encryption was computationally cheap enough that a single encryption wouldn’t take too long. However, the tens of thousands of encryptions that would be needed for a dictionary attack would take prohibitively long.