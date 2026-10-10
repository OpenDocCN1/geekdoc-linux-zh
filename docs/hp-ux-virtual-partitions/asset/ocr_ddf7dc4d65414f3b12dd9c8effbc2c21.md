Performing this interactive backup of *cable1* could not be simpler with SAM. Let’s now see if we can backup *cable2* to the remote tape drive on *cable1*. Keep in mind that as far as SAM is concerned, these are two completely different systems, even though vPar *cable1* and *cable2* are running on the same computer. This means that the backup of *cable2* to the tape drive on *cable1* is remote.

We can initiate the backup of *cable2* in two different ways. The first would be to invoke SAM on *cable2* and specify all of the appropriate information. The second is to run SAM remotely. We’ll chose the latter approach. We first specify from *cable1* the name of the remote system on which we want to run SAM, as shown in Figure 11-6:

![](bbox=[0.16, 0.38, 0.82, 0.54])

Figure 11-6 Add vPar *cable2* as a Remote System on Which to Run SAM

After we specify the hostname of *vchdcn4* and make a note that this is vPar *cable2*, we press OK and SAM configures this as a remote host.

We can now run select the remote host and run SAM on it as shown in Figure 11-7: