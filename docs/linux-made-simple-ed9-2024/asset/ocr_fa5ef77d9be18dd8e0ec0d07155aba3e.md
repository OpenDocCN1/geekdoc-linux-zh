# # TruPax: Easy file encryption

Introducing the versatile Java utility that can encrypt your files in just three simple steps in a large container file.

For non-crypto nerds, VeraCrypt is a program that enables you to create encrypted containers of any size, inside which you can place your personal photos, bank details or any other data for which you're not ready. VeraCrypt mounts these containers with a password, which means only you can access your files. For the uber-paranoid there are even options to combine multiple encryption ciphers and use key files in addition to a password.

![](bbox=[0.52, 0.3, 0.92, 0.47])

VeraCrypt does require you to have some idea in advance of the size of all the files you need. Once an encrypted container has been created, it's not possible to resize it. What's more, if you create a container in the full belief that there's enough room for all your files and then find you don't have enough space, there's nothing to do but start the volume creation process all over again. This is a nuisance at the best of times but is particularly frustrating if you choose to store your encrypted container with a cloud service such as Dropbox, as the upload process has to be restarted.

> > **Quick tip**
> Before clicking 'Add folder', be sure to check the box marked 'Include Subfolders' to copy any directories inside it into a new container too.

TruPax posts a solution to creating redundant, huge blobs of data on your machine. This Java app can be used to select files or folders before creating a volume and will create one of exactly the right size. There is even an option to add some more free space if you think you'll need it.

In this tutorial, we will explore how to use TruPax to create an encrypted container of exactly the right size, then open it in VeraCrypt. In order to proceed, you'll need Java installed on your machine (either the vanilla variety from Oracle or OpenJDK – keep reading for more info). Once the volume is created, you'll also need VeraCrypt pre-installed on your system to mount it.

If the world isn't ready to know you're a military history buff, create a secure container for your magazine collection. Check 'show password' to display as you type.

VeraCrypt can be downloaded from **http://veracrypt.codeplex.com**. The website itself has some excellent documentation on getting started or you can see our previous tutorial in *Linux Format* issue 218.

This tutorial was written for Ubuntu Linux but both Java and VeraCrypt are compatible with all Linux versions, so you should have no trouble running TruPax regardless. Another great advantage of TruPax is that admin privileges are not required simply to create a volume or

# ## TruPax Plus

As convenient as TruPax is for creating volumes of just the right size, this comes at the price of extra security. If you wish you can also add a key file. This means in order to mount your TruPax volume, VeraCrypt would use both your password and a file. This is a form of Two-Factor Authentication (something you have and something you know) and hugely reduces the chance that an attacker can access your volume. VeraCrypt also has a random keyfile generator. Go to Tools > Keyfiles to launch this. You can use one or a number of files. Remember that the first 64 kilobytes of the file must not change, or the container can't be opened. This is why images and music files work better. VeraCrypt doesn't alter the file, so if for instance you choose an MP3 of Aqua's Doctor Jones as your key file, there's no way from examining the file itself to know that it's been used this way. In VeraCrypt choose Volumes > Change Volume password to get started. Enter your password in the field in the Current section, then again in the New section. Check 'Use Keyfiles' then click the 'Keyfiles' button to select the actual files. The order in which you select them doesn't matter at all.

Before clicking 'OK' at the top right, move to the dropdown menu marked 'PKCS-5 PRF' in the New section, and choose 'HMAC-Whirlpool' to use a hash that has been developed entirely independently of our friends in the NSA.

![](bbox=[0.65, 0.85, 0.92, 0.92])