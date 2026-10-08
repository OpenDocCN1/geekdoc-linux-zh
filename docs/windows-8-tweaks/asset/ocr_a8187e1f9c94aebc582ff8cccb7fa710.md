+   16. Navigate through Local Policies and Security Options and locate User Account Control: Run All Administrators In Admin Approval Mode. Right-click this policy and select Properties.
17. Select Disable and click OK to save the changes.

You are now finished setting up UAC to not run for your system configuration account.

After you are finished with these steps, you can easily switch to the configuration account with higher rights by pressing and holding Ctrl+Alt+Delete. Then click Switch User and select the configuration account. When you are finished doing work that requires higher rights, press Ctrl+Alt+Delete again and switch back to your low-rights session.

# Using File Encryption

Do you have important documents on your computer that you don’t want anyone else to see? Sure, you can set file permissions on files so that only your account can read them. Is that enough? Is that enough? Unfortunately, it is not, because file permissions can be manipulated in many ways and your account password replaced if someone has physical access to your computer. If your computer is stolen or if someone breaks into your office or home, the only way truly to protect important data is to encrypt it.

Windows 8 includes two different levels of encryption: file level and hard-drive level. The file-based encryption is a feature of NTFS, whereas the drive-level method is a feature in Windows 8 called *BitLocker Drive Encryption*. The main difference between the two is that BitLocker Drive Encryption can encrypt your entire drive or partition so that even the filesystem is protected. Everything on the drive, including the operating system, is encrypted so that no one will even be able to see a list of files. The security of BitLocker Drive Encryption comes at the price of performance and requires certain hardware, which is why file-level encryption is often preferred. Therefore, I am going to cover that first.

# Encrypting Your Files

File-level encryption in Windows 8 is very easy to do. However, some steps are required before you start encrypting files to make sure that you can always decrypt your files at a later time no matter what happens. This next section shows you why it is important to set up a Recovery Agent in Windows 8.