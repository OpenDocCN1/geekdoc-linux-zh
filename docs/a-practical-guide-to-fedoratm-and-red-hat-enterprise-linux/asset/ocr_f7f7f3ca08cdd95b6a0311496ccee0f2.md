Table 15-3 Machine log

| Entry | Function |
| :--- | :--- |
| Hardware modifications | Keep track of the system hardware configuration: which devices hold which partitions, the model of the new NIC you added, and so on. |
| System software modifications | Keep track of the options used when building Linux. Print such files as /usr/src/linux/.config (Linux kernel configuration). The file hierarchy under /etc/sysconfig and /etc/default contain valuable information about the network configuration, among other things. |
| Hardware malfunctations | Keep as accurate a list as possible of any problems with the system. Make note of any error messages or numbers the system displays on the system console and identify what users were doing when the problem occured. |
| User complaints | Make a list of all reasonable complaints made by knowledgeable users (for example, “Machine is abnormally slow”). |

# Keeping the System Secure

No system with dial-in lines or public access to terminals is absolutely secure. Nevertheless, you can make a system as secure as possible by changing the passwords of the root password frequently and by choosing passwords that are difficult to guess. Do not tell anyone who does not absolutely need to know the root password. You can also encourage system users to choose difficult passwords and to change them periodically.

+   * **Passwords** This section contains a technical discussion of passwords; see “Password Security” on page 136 for a more practical discussion.

By default, passwords for Fedora/RHEL use MD5 (page 1260) hashing, which makes them more difficult to crack than passwords encrypted with DES (page 1159). Of course, it makes little difference how well encrypted your password is if you make it easy for someone to find out or guess what the password is. The system-config-authentication utility allows you to specify a local password hashing algorithm: Select the Advanced Options tab and make a selection from the drop-down box labeled Password Hashing Alogrithm.

A password that is difficult to guess is one that someone else would not be likely to think you would choose. Do not use words from the dictionary (spelled forward or backward); names of relatives, pets, or friends; or words from a foreign language. A good strategy is to choose a couple of short words, include some punctuation (for example, put a ^ between them), mix the case, and replace some of the letters in the words with numbers. If it were not printed in this book, an example of a good password would be C&cyGram5 (candygrams). Ideally, you would use a random combination of ASCII characters, but that would be difficult to remember.

You can use one of several password-cracking programs to find users who have chosen poor passwords. These programs work by repeatedly hashing words from