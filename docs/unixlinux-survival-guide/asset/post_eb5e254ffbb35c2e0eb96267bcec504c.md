
environments “grew” in a more organic manner and were not scaled to fit the needs. Somewhere in the past, the decision was made to install the backup service on a machine that seemed to have room for that task. If this machine dies, it doesn’t just take the data, or whatever it used to do besides running the backup, with it, but the backup system is gone as well. You have no way to start a recovery session. As simple as the last statement sounds, many IT-related decisions remain pending because of daily stress and overworked administrators, with the inherent promise to “look into that, as soon as time permits.”

If you are confronted with a situation like the one described, you should try to find a solution as soon as possible. A system capable of running a backup service for a couple of clients (a client in that respect is every machine, workstation, or server having data that needs to be backed up) in a satisfactory way needs to fulfill only four requirements:

- 1. There should be a reliable backup device attached to it.
- 2. The system needs a certain amount of memory and hard disk space.
- 3. The used operating system should be stable and secure.
- 4. The system should have more than one network interface.

The backup system should not run additional services. These services would suffer when the system is busy running a recovery session. Configurations using a customized runlevel (see Chapter 5 for more on init states and runlevels) to run the backup software are not usable during normal operation hours without shutting down running services. The quote “you only need the backup software during the night” works as long as you do not have to recover a crashed system during daytime.

The operating system to run the backup software on should be as stable and secure as possible. Because backups are usually performed via the network, the OS should be able to deal with more than one network interface and make use of the presence of more than one network interface.

There is one exception to the rule. If you are using clustered systems—this means more than one system is clustered to the others and is not visible to the outside world as an individual system, but as a single system providing services to the network, the so-called virtual system—then running the backup server on it should not be a problem. You just have to make sure to be aware of the impact on the running services and that you have enough capacity to start the backup software during normal operation hours as well.

## 4.2.8 Check the Backups!

Test periodically whether it is possible to read in old backups. If the read/write head of a tape drive starts moving, it will be a gradual process, and it will take a long time before a noticeable change occurs. If the unit fails to read in an older tape, you should take precautions immediately. Compensating for a misaligned read/write head requires either great skill or money. If you desperately need to get back an older backup written with a misaligned head, brace yourself for the bill to be paid. It can be done, but the companies capable of doing it charge accordingly. If you have to try to misalign the head of a replacement unit just to get to the contents of the tape, the warranty of this device will be voided.

Make it a habit to restore backups older than a month or even older to an empty directory on a periodic basis. If you encounter any errors, the unit should be replaced. If you followed the author’s advice and bought an external unit, test it as well. The capability to restore important information is at stake here.

## 4.3 SUMMARY

This chapter discussed strategies regarding backup and provided information that needs to be taken into account while creating a strategy for doing daily, weekly, and monthly backups. It talked about the necessity of storing copies of the backups off-site. It continued with tips and a script to create backups of files vital to the operation of the system. Some other tips included the creation of a duplicate boot disk and the necessary assessment of the existing backup hardware and infrastructure.
