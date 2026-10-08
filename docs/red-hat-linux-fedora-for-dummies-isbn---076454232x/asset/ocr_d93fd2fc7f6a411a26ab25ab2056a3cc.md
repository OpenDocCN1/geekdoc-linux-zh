Interactive communication is effective for performing tasks on remote machines. For example, the primary way to work on Linux machines originally was via the CLI. The CLI is often the best way to perform remote tasks.

CLI-based communication used to be primarily carried out over the insecure Telnet, FTP, and rsh connections. All services use unencrypted connections, and passwords were readily detected. The rsh service also used a system of intermachine trust. That trust allowed hackers, like the infamous Kevin Mitnik, to "own" a network by breaking into one machine and then logging in to additional ones without authentication.

Open Secure Shell (OpenSSH) provides an encrypted channel to perform all those tasks. Red Hat Linux bundles OpenSSH by default. We describe how first to use the OpenSSH client to communicate with other machines and, second, create an OpenSSH server.

You should (dare we say *must*?) use encrypted channels when you're communicating over the Internet and wireless networks. Both the Internet and Wi-Fi connections are inherently insecure, and you have to protect your communications.

# Connecting to a Secure Shell server

Start by using OpenSSH as a client. Suppose that you want to log in to your ISP server, `ssh.mysp.com`, with OpenSSH:

+   1.  **Open a GNOME Terminal session.**

+   2.  **Enter this command:**
    ```
    ssh ssh.mysp.com
    ```
    Your mileage may vary, of course. You may have to use the `-1` option if, for example, your ISP user account name is different from your local computer. If your username on your local machine is `lidia`, but it's `lmaura` at your ISP, enter this line:
    ```
    ssh -1 lmaura ssh.mysp.com
    ```
    The first time you connect to a remote server, you're prompted to accept the remote server's fingerprint.

+   3.  **Enter yes when you're prompted.**

+   4.  **Enter your password when you're prompted, and you're logged in.**
    For example, you can now use a text-based e-mail client, like pine, to read your messages. This program is useful if you want to read your e-mail securely but can't connect to your ISP with an SSL-enabled Mozilla or Evolution e-mail client.