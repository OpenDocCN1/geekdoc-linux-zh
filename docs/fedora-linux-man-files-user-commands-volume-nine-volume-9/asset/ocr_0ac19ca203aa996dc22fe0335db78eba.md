Enables compression (via ssh's -C flag).

+   - **-c** *cipher*
+     Selects the cipher to use for encrypting the data transfers. This option is directly passed to (1).

+   - **-D** *sftp_server_path*
+     Connect directly to a local sftp server (rather than via (1)). This option may be useful in debugging the client and server.

+   - **-F** *ssh_config*
+     Specifies an alternative per-user configuration file for (1). This option is directly passed to (1).

+   - **-f**
+     Requests that files be flushed to disk imidately after transfer. When uploading files, this feature is only enabled if the server implements the “” extension.

+   - **-i** *identity_file*
+     Selects the file from which the identity (private key) for public key authentication is read. This option is directly passed to (1).

+   - **-l** *limit*
+     Limits the used bandwidth, specified in Kbit/s.

+   - **-o** *ssh_option*
+     Can be used to pass options to **ssh** in the format used in ssh_config5. This is useful for specifying options for which there is no separate **sftp** command-line flag. For example, to specify an alternate port use: **sftp -oPort=24** For full details of the options listed below, and their possible values, see ssh_config5.

+   **AddressFamily**
+   **BatchMode**
+   **BindAddress**
+   **CanonicalDomains**
+   **CanonicalizeFallbackLocal**
+   **CanonicalizeHostna**
+   **CanonicalizeMaxDots**
+   **CanonicalizePermittedCNAMEs**
+   **ChallengeResponseAuthentication**
+   **CheckHostIP**
+   **Cipher**
+   **Ciphers**
+   **Compression**
+   **CompressionLevel**
+   **ConnectionAttempts**
+   **ConnectTiout**
+   **ControlMaster**
+   **ControlPath**
+   **ControlPersist**
+   **GlocalKnownHostsFile**
+   **GSSAPIAuthentication**