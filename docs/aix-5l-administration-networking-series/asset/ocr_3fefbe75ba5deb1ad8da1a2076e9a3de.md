![](bbox=[0.13, 0.1, 0.9, 0.52])

# **Figure 29-4. ESS Specialist Add Volumes (1 of 2)**

host I want the storage attached to. Using this method allows me to detach the storage from one host and attach it to another without losing every host definition on the LUNs in the process. This is just a placeholder, so make the dummy host names descriptive of what the storage is used for. An example is a VG and host name combination.

After we select the host, the next step is to highlight the storage arrays that you want to use. This is where your excellent storage planning will be seen by everyone. To select multiple arrays, just hold down the CTRL key and click each array you want to select. I have selected every A loop array in the ESS, as shown in Figure 29-4.

When you click **Next**, you move to the **Add Volumes (2 of 2)** panel, as shown in Figure 29-5. Now you need to make some actual configuration decisions.

In our planning, you decided on a LUN size for this group of storage. For my demonstration, I like to use a 64GB LUN size. I want to add 32 LUNs, each having a LUN size of 64GB, but there is still one more major decision to make. Do you want to add the LUNs sequentially, or does spreading the LUNs across all of the arrays make more sense? This decision varies, depending on what you are doing. For this example, I want to spread the partitions across all of the arrays. At the bottom of the panel, you