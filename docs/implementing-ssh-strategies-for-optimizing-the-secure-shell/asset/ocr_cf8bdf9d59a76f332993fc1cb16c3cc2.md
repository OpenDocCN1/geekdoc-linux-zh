| **Table 4.3 (continued)** |  |  |
| :--- | :--- | :--- |
| **OPTION** | **DESCRIPTION** |  |
| User-key directory | Specifies the directory where the user's public key will be stored. The default is `%D\.ssh2`, which is the users' home directory in the .ssh2 folder (for example, `/home/<username>/.ssh2` on Unix and Documents and Settings\<username>\.ssh2 on Windows). |  |
| Authorization file | Stores a valid list of public keys that will be authorized for public-key authentication. The default is the authorization file, which is stored in the users' home directory (/home/<username>/.ssh2 on Unix and Documents and Settings\<username>\.ssh2 on Windows). |  |

# SSH Communications' SSH Server (Unix)

The SSH server for Unix offers authentication options similar to the Windows platform. One difference is that the Windows Server configuration screen is simply a GUI that points to the SSH configuration file, which is sshd_2_config; the Unix version of the SSH Communications' server does not use a GUI but directly uses the configuration file itself. To view the authentication options, enter the following commands.

```
#cd /etc/ssh2
#more sshd_2_config
```

Options in the authentication section are listed in Table 4.4, along with a description of each option.

| **Table 4.4** | Authentication |  |
| :--- | :--- | :--- |
| **OPTION** | **DESCRIPTION** |  |
| BannerMessageFile | Denotes the location of the file that contains the banner message, such as "The only way to win is not to play." Default path is /etc/ssh2/ssh_banner_message. |  |
| PasswordGuesses | Specifies the number of attempts a user has in order to enter the correct password. |  |