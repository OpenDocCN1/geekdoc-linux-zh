![](bbox=[0.18, 0.08, 0.75, 0.44])

**Figure 4.8** Keys subcategory for SSH Communications’ SSH client.

+   11.  After selecting Upload Public Key, a new display should appear. The display should contain the name of the public key, the destination folder for the key to be placed, which is the folder on the SSH server to place the key, most likely /home/user/.ssh2, and the authorization file to add the key to, such as authorization. After verifying that all the items are correct, select Upload.

+   12.  After selecting Upload, you will see a successful completion of the upload, where you can select finish; however, if you want to require the use of public keys only, you will have to go back and edit the sshd2_config file to require only the use of public keys and to delete password or host-based authentication. Also, if you receive an error in the upload process, probably the SSH server you are attempting to connect to is not a SSH Communications’ SSH server, so the key-converting process will have to be followed, listed as follows.

+   13.  At this point, you should be redirected to the initial Key subcategory screen. To confirm that the keys have been generated appropriately, browse to Documents and Settings\username>\Application Data\SSH\UserKeys. There should be both the public key (*.pub) and private key located in this folder. Also, the Key subcategory screen should appear with the newly generated key in the Keys field, as shown in Figure 4.9.

+   14.  SSH Communications’ SSH keys have been generated!