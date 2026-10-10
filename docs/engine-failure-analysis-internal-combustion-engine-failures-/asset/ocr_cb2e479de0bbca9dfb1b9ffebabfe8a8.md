# AT A GLANCE (CONT.)

| How Do I | See This Entry | Example |
| :--- | :---: | :--- |
| Create a key pair (public key and secret key) for encrypting files and e-mail messages? | **gpg** | `gpg --gen-key` |
| Compress all the files in the specified directory and all its associated subdirectories? | **gzip** | `gzip -r /home/suzanne/documents` |
| Encrypt a file so that no one can read it unless they know the passphrase and compress it so that it takes up the least possible storage space? | **mcrypt** | `mcrypt -uz mysecrets.txt` |
| Create a **tar** archive containing all the files in my home directory that have the `*.sdw` extension? | **tar** | `find /home/suzanne -name '*.sdw' -print | xargs tar -cvf backup.tar` |
| Update an existing **tar** archive by adding only those files that are not already present in the archive? | **tar** | `tar -uvf backup.tar /home/suzanne` |
| Extract files from a compressed tarball (`*.tgz` or `*.tar.gz`) that I downloaded from the Internet? | **tar** | `tar -xvzf kdatabase.tgz` |