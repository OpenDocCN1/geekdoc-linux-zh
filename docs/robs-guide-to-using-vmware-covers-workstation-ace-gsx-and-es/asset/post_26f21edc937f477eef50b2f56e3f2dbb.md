
## 3.4 Using Snapshots

You can take a snapshot when the virtual machine is either in a Powered On or Powered Off state or even when it is suspended. Click the snapshot button or select VM → Snapshot → Save Snapshot.

![](img/25fe75b93b97a021effaba85db112a52_48_0.png)

Figure 3.1: The toolbar provides easy access to the snapshot feature.

From this point forward, everything you do in your virtual machine will not affect the original files. All changes to the hard disk will go into separate files, and what was in RAM at the point of taking the snapshot is saved in a separate file.

To go back to the same point where you took the snapshot, just click the Revert button or select Snapshot → Revert to Snapshot. With the new multiple snapshot feature, you can select to which snapshot you want to revert to if you have more than one.

Note: Be careful about using the snapshot feature in a distributed virtual machine environment. If an application in one machine is communicating with another application in a second virtual machine, then reverting to a snapshot in one of the machines will create an inconsistent data set. This is also true for Active Directory and eDirectory synchronization and replication.

Reverting to the snapshot point will delete everything that happened since taking the snapshot and will start out with the disk from that snapshot point. It will restore the RAM which was in the virtual machine's memory when the snapshot was created.

Note: You will still be using the snapshot, so everything you do will still be saved in separate files. Clicking Revert one more time will delete everything again.

Note: Using the snapshot feature results in an overhead to the normal operations of VMware Workstation. If you do not need snapshots for a particular machine then do not create any snapshots or if they already exist, delete them.

## 3.5 Working with Multiple Snapshots

Starting with VMware Workstation 5, you can work with multiple snapshots. This feature helps you to return to any point in time, when you were using a specific configuration.

Note: Virtual machines which were created with an older version of VMware Workstation (prior to version 5 or with other VMware products) can be used in this version, but the snapshot feature will not be available. Upgrade the virtual machine hardware to use this new feature.

The example I will discuss here takes place in a training situation, where the students can go to any exercise in the training by reverting to the snapshot point for a particular exercise. By using snapshots this way, students can go back to a previous exercise when they have messed up their environment. Also, when there is a need to skip an exercise, the students can start at any given point without the need for going through the other exercises first. This is a great solution for modular training delivery.

Tip: Of course students who perform all the exercises without problems do not have to go to any of the snapshots. They can start out with the starting virtual machine and just work their way through the exercises for the duration of the training. Only when something does go wrong, they will not have to start all over again.

![](img/25fe75b93b97a021effaba85db112a52_49_0.png)

Figure 3.2: The simplest way to use multiple snapshots is the linear approach.

The first possibility to work with snapshots is linear: you start out with your first snapshot and keep creating sequential snapshots.

Figure 3.2 shows an example of this approach. You can go back to any point in time. In this example, it is to start a specific exercise. The description box is useful in helping users identify the status of the virtual machine.

There can be some scenarios, when you not only want to follow a single line of snapshots, but you may also want to branch off at any given point in the line of snapshots. This can be done and will result in a snapshot tree.

![](img/25fe75b93b97a021effaba85db112a52_50_0.png)

In the example where exercises are created for students, you can click the initial snapshot and revert to that snapshot in Snapshot Manager by clicking the Go To button.

This will result in a new line of snapshots that can also be branched off at any given point. Just click the snapshot, revert to it and select Take Snapshot.

Figure 3.3: Click the initial snapshot and revert to it to start a new branch.

![](img/25fe75b93b97a021effaba85db112a52_50_1.png)

Figure 3.4 shows an example of a snapshot branch that was created for the exercises in section 2 of a training course. In this example, there is an extra exercise that the students can perform for which an extra snapshot is created at the Exercise 2.2 snapshot point.

They can go to that snapshot, when they want to perform that specific exercise.

Figure 3.4: A snapshot tree can be branched off at any point.

While working with many snapshots, it is possible to lose track of where you are. To find out what the active snapshot is, you need to go into the Snapshot Manager.

You can rename the virtual machine in the settings to the same name as the snapshot. Since the snapshot feature also keeps track of the configuration changes, the VMware Workstation window will show the name of the machine, which will also be the name of the snapshot.

![](img/25fe75b93b97a021effaba85db112a52_51_0.png)

Figure 3.5: Rename the virtual machine in each snapshot to keep track of where you are.

## 3.6 Deleting a Snapshot

You can delete a snapshot at any given time. From the Snapshot Manager, select the snapshot that you want to remove and click the Delete button. This will start a process of optimizing the snapshot tree and linking the children of the deleted snapshot to their parents.

Tip: If you do not want to save the changes that you made since creating the snapshot, first revert to the previous snapshot and then delete the snapshot.

It is also possible to delete an entire snapshots branch at once. To do this, right click the snapshot and select Delete Snapshot and Children.

## 3.7 Configuring the Snapshot Feature

In some situations you might want to disable one of your disks from the snapshot. You can do that by configuring the disk as an independent disk. To do that, go into the settings of the virtual machine, select the disk that you want to set to independent, and click the Advanced button in the disk configuration panel. Set the checkbox to make the disk an independent disk. You can only do this when there are no snapshots already.

You also have to choose between a persistent disk and a nonpersistent disk. The first mode saves all the changes into the original disk file and the second mode saves all the changes in a separate REDO-file, which will be removed when you turn off your virtual machine.

### Disabling Snapshots

The snapshot feature can be disabled on a per virtual machine basis. This only works when the virtual machine does not have a snapshot. To disable taking snapshots, open the virtual machine settings, select the Options tab, and select the snapshot entry. In the right panel, you will see a checkbox to Disable Snapshots.

![](img/25fe75b93b97a021effaba85db112a52_52_0.png)

Figure 3.6: Snapshot behavior can be configured on a per virtual machine basis.

The default configuration for snapshots is that they will not be affected by powering off or resetting the virtual machine. This behavior can be changed from the virtual machine Settings to any of these options:

- Just power off — Does nothing and leaves the snapshot intact.
- Revert to the snapshot — Always removes the snapshot when powering off and always starts with the same state.
- Take a new snapshot — Takes a new snapshot when the machine powers on, and adds all changes you made to the original file.
- Ask me — Asks you which of the above actions to take.

### Changing snapshot priority

With VMware Workstation, virtual machine snapshots are created and restored as a background process. This is a great feature because you can almost instantaneously continue working with the guest OS while the snapshot process is finishing up. If you try to start a new snapshot process when another one is not finished, you will receive a message about it.

![](img/25fe75b93b97a021effaba85db112a52_53_0.png)

It depends on the usage scenario of the virtual machine whether you want to keep this feature turned on. In a classroom environment for example, students who revert to a snapshot can start working immediately. However, when they do this, the machine might be slow in the beginning. Depending on the audience, it might be better to let them wait until the process is finished as a foreground process.

To change the way that the snapshots are created, select VM → Preferences and enable or disable the checkbox in the Priority tab.

Figure 3.7: Snapshots are created as a background process by default.

## 3.8 Cloning Virtual Machines

This new feature allows you to create a copy of a virtual machine. It is different than using snapshots. With multiple snapshots on a virtual machine only one of the snapshots can be active, whereas you can boot one or more clones that you have created of a virtual machine at the same time.

There are a wide variety of usage examples for virtual machine clones. For an instructor who has to set up a classroom with virtual machines, this wizard helps him to easily create unique machines for each student. With the linked clone setup, explained later, the parent could reside on the network, while the student's clone machine is on his own computer.

Other uses are for software testing where at any point in time, or even at a given snapshot in a snapshot tree, you need to have someone else work on the same environment to perform tests for you. Clone the virtual machine and provide them with that copy to work on.
