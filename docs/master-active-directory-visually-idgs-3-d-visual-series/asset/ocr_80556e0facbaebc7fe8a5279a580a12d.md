# TIPS

# How are Extensions used?

Some snap-ins contain extensions to other snap-ins. You can think of extensions as “links.” Some snap-ins have configuration that requires the snap-in to open another snap-in. For example, in Active Directory Users and Computers, you can configure Group Policy for a domain. In order to configure Group Policy, the Group Policy snap-in has to be opened. The Users and Computers snap-in contains a link to the Group Policy snap-in so it can be automatically launched when you want to configure Group Policy. The extensions allow different, yet related, snap-ins to function together so you do not have to manually open related snap-ins.

# When I remove a snap-in, is the snap-in deleted?

No. When you remove a snap-in from the Standalone tab, you are simply telling the MMC not to load a previously selected snap-in. This action simply removes the snap-in from you list so it is not loaded.

![](bbox=[0.03, 0.52, 0.48, 0.84])

# REMOVING A SNAP-IN

+   1. Select the Standalone tab, then select the snap-in you want to Remove.

+   2. Click the Remove button.
+   3. Click OK when you are done.

![](bbox=[0.5, 0.52, 0.97, 0.84])

The snap-in now appears in the console.