# 4.1 Initial installation of z/VM, compared to z/OS

This section is intended for z/OS system programmers, who have little or no experience with z/VM. This section should help you understand the basics of installing a z/VM system.



Existing z/OS and z/VM sites usually perform their installation or upgrade tasks from an existing running system.

z/VM sites typically use an existing virtual machine to install a new z/VM system from a z/VM DDR (tape delivery) or DVD delivery. As of January 2008, the z/VM base operating system and base options became available for Internet delivery orders placed using ShopzSeries, in countries where it is available. See the following Web address for more information:

```
http://www.vm.ibm.com/buy/edelivery/
```

z/OS sites do the installations from an existing z/OS image using one of the available installation methods offered by IBM, currently ServerPac, CBPDO, or SystemPac®.



IBM offers only one delivery type to install z/VM, although an option for type of media (DVD or tape) is available.



As mentioned, the available installation methods offered by IBM for z/OS are currently ServerPac, CBPDO, or SystemPac. This section describes each.



The z/OS installation method named ServerPac is a "software delivery package consisting of products and service for which IBM has performed the SMP/E installation steps and some of the post-SMP/E installation steps" (according to z/OS V1R9.0 Planning for Installation, GA22-7504-17). The package is an integrated set of products that have passed initial testing. This method involves the use of the CustomPac Installation Dialog, which allows the customer to customize aspects such as naming data sets and volumes, and placing data sets within the set of disks built during installation. Customers are given the choice of