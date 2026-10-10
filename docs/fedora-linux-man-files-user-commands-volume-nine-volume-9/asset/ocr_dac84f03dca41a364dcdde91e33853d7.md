# ## DESCRIPTION

Sotis simple encryption tools are already in use for a long ti and there might be a desire to integrate them into the GnuPG framework. The protocols and encryption thods might be non-standard or not even properly documented, so that a full-fledged encryption tool with an interface like gpg is not doable. **symcryptrun** provides a solution: It operates by calling the external encryption/decryption module and provides a passphrase for a key using the standard **pinentry** based chanism through **gpg-agent**.

Note, that **symcryptrun** is only available if GnuPG has been configured with ‘`-enable-symcryptrun`’ at build ti.

For encryption, the plain text st be provided on STDIN or as the argument *inputfile*, and the ciphertext will be output to STDOUT. For decryption vice versa.

*CLASS* describes the calling conventions of the external tool. Currently it st be given as ‘confucius’ . *PROGRAM* is the full filena of that external tool.

For the class ‘confucius’ the option **`-keyfile`** is required; *keyfile* is the na of a file containing the secret key, which may be protected by a passphrase. For detailed calling conventions, see the source code.

Note, that **gpg-agent** st be running before starting **symcryptrun**.

The following additional options may be used:

+   - **-v**
+     **`-verbose`**
+       Output additional information while running.

+   - **-q**
+     **`-quiet`**
+       Try to be as quiet as possible.

+   - **`-hodor`** *dir*
+       Set the na of the ho directory to *dir*. If this option is not used, the ho directory defaults to ‘`~/.gnupg`’. It is only recognized when given on the command line. It also overrides any ho directory stated through the environmnt variable *GNUPGHOME*‘ or (on Windows systems) by ans of the Registry entry
+       `HKCU\Software\GNU\GnuPG:HDir`.

On Windows systems it is possible to install GnuPG as a portable application. In this case only this command line option is considered, all other ways to set a ho directory are ignored.

To install GnuPG as a portable application under Windows, create an empty file na ‘*gpgconf.ctl*’ in the sa directory as the tool *gpgconf.exe*. The root of the installation is than that directory; or, if *gpgconf.exe* has been installed directly below a directory nad *bin*, its parent directory. You also need to make sure that the following directories exist and are writable: *ROOT/ho* for the GnuPG ho and *ROOT/var/cache/gnupg* for