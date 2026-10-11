
![](img/c7771e8540507f2b00c088c7a411b57b_396_0.png)

FIGURE 8.43
The NetStorage home page.

iFolder can't help you in this situation. Because the file isn't a synchronized iFolder directory, you can't access it using iFolder tools. With a properly configured NetStorage service running on your server, however, users can get access to the Samba share using a browser and gain access to their files.

NetStorage leverages the CIFS protocol such that user permissions are enforced when accessing a Samba share with a web browser. Because of this, you have to LUM/Samba-enable users in eDirectory before they can access a Samba share with NetStorage.

As mentioned, NetStorage also allows users to access their iFolder files on the iFolder server in a browser window. As with Samba, users must be iFolder-enabled before they can do this.

As you can see, NetStorage truly complements iFolder and Samba rather than duplicating their functionality. Sometimes students new to NNLS express security concerns about transferring files over the Internet (or even over their organizational network) using browser protocols.

We’ve all heard horror stories about hijacked FTP and Telnet sessions. With NetStorage, you don't need to worry. You can configure NetStorage to encrypt file transfers using SSL. With that, let's talk about NetStorage storage locations.

## NetStorage Storage Locations

Refer back to Figure 8.43 and notice that there is a folder named **shared**. By default, NetStorage provides a shared storage location for all NetStorage users, even if they aren't LUM/Samba or iFolder enabled. This shared folder is located, by default, in the `/var/opt/novell/netstorage/shared` directory in your server file system.

Refer to Figure 8.43 again and notice that there's a folder for users' iFolder accounts. If users have been iFolder enabled, they can access their iFolder files from the iFolder server.

When the user clicks the iFolder folder, he or she will be prompted to provide an iFolder pass phrase. This is shown in Figure 8.44.

![](img/c7771e8540507f2b00c088c7a411b57b_397_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_397_1.png)

In Exercise 8.1, you configured iFolder for the DNelson.IFCLE user object. As a part of the exercise, you created a directory named MyFile.doc and entered some text into it. Using NetStorage, you can access the synchronized version of that file residing on the iFolder server. This is shown in Figure 8.45.

I mentioned earlier that NetStorage can also access Samba shares. Access to this kind of storage is configured through *Storage Location* objects.

A Storage Location object is a pointer object in the eDirectory tree that directs NetStorage to a Samba share that has already been defined in the `smb.conf` file. Users are associated with the Storage Location objects, providing them access to the Samba share through the NetStorage web interface. Because Storage Location objects rely on Samba, NetStorage users must be LUM/Samba enabled.

If you want to create a directory in the Linux file system and provide NetStorage users with access to it, you must first define a share for the directory in the `smb.conf` file and restart the novell-smb service. Let's look at how this is done.

![](img/c7771e8540507f2b00c088c7a411b57b_398_0.png)

FIGURE 8.45
Accessing iFolder files in NetStorage.

## Configuring NetStorage

Test Objective Covered:

- 6. Install and configure NetStorage.

As with iFolder and Samba, the CLE exam objectives specify that you be able to install and configure NetStorage. Just as we've done before, we're only going to touch the installation of NetStorage lightly because most of Chapter 5 was spent discussing NNLS installation procedures.

### Installing NetStorage

The only critical item you need to keep in mind about NetStorage is the fact that it can't be installed alone. If you perform a Custom NNLS installation, you'll notice that there's no option for NetStorage in the component-selection screen.

To install NetStorage, you have to install the NNLS Virtual Office component. When NNLS was in its early beta phase, this was not the case. NetStorage could be installed alone. During the mid-beta phase of the product, this was changed, and NetStorage was rolled into the Virtual Office product. I had the opportunity to speak with the NetStorage programmers at the time and asked them why this was done.

They explained that it simply was such an integral part of Virtual Office that it made sense for them to merge the two products into a single install. When we cover Virtual Office later in this book, I think you'll agree that this decision makes sense.

As with iFolder, if you performed an Express install, NetStorage was installed on your system. If you performed a Custom install, you had the opportunity to select the Virtual Office component for installation.

If you didn't select Virtual Office (and hence, NetStorage) during the initial installation of NNLS, you can perform a post-installation by completing the following steps:

- Mount your NNLS ISO image.
- Run the install.sh script.
- When prompted, specify a Custom installation.
- When prompted to select the products to be installed, deselect all products.
- Select Virtual Office.
- Finish the installation according to the instructions presented in Chapter 5.

Let's spend the rest of this chapter discussing how to configure NetStorage.

### Configuring NetStorage

Refer back to Figure 8.43 and notice that the only storage available through NetStorage is the user's iFolder directory and the common shared directory. This is because NetStorage hasn't been configured with Storage Location objects in the eDirectory tree.

### Configuring Storage

To create a Storage Location object, complete the following steps:

- Create the directory in the Linux file system you want NetStorage users to be able to access.
- Edit your smb.conf file to create a Samba share for the directory created in step 1.
- Restart your novell-smb service.
- Open a web browser and navigate to `https://your_server_IP_address/nps/iManager.html`.
- Authenticate as your admin user.
- Scroll down to the File Access (NetStorage) role and select the Storage Location: Create task. The Storage Locations: Create Object screen appears, as shown in Figure 8.46.

![](img/c7771e8540507f2b00c088c7a411b57b_400_0.png)

FIGURE 8.46
Creating a Storage Location object.

- In the **Object Name** field, enter a name for the Storage Location object.
- In the **Display Name** field, enter the name for the Storage Location object that you want users to see in NetStorage.
- In the **Directory Location** field, enter the location of the directory in the Linux file system.

This step trips up a lot of folks the first time they configure a Storage Location object (at least, it tripped me up the first time I tried to create a Storage Location object). The field name makes it sound like you can enter a simple directory path, but nothing is further from the truth.

Instead of a path such as /tmp, you have to enter a URL in this field. If you're pointing to a directory on a Linux server, the format for the URL is as follows:

`cifs://server IP address/Samba_share`

For example, if your share name is tmp (such as the one we created earlier in this chapter) and your server's IP address is 192.168.1.36, you would enter the following:

`cifs://192.168.1.36/tmp`

> **TIP**
> If you happen to be pointing to a NetWare server, you enter the URL as `ncp://server IP address/volume name/path`.

- In the **Context** field, enter the context where the Storage Location object will reside in the eDirectory tree.
- Click **Create**.
- When prompted that the object was created, click **OK**.

After you have created all your Storage Location objects, you next need to create *Storage Location Lists*, which are used to associate Storage Location objects with eDirectory user, group, or container objects. Users associated through such lists will see the storage locations in the list displayed when they authenticate to NetStorage.

To create a Storage Location List, complete the following steps:

- In iManager, select the **Storage Location: Create/Modify List** task under **File Access (NetStorage)**. The screen shown in Figure 8.47 is displayed.

![](img/c7771e8540507f2b00c088c7a411b57b_401_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_401_1.png)

- In the **Object** field, browse to and select a user, group, or container object you want to associate with the Storage Location object.
  - If you select a user object, only that user will have access to the storage location. If you select a group object, all users who are members of the group will have access. If you select a container, all users who reside within the container will have access.
- Click **OK**. The screen in Figure 8.48 appears.
- In the **Storage Location Objects** field, browse to and select the Storage Location object(s) you want to associate with the list. You can select multiple objects.
