![](bbox=[0.04, 0.12, 0.1, 0.2])

# What permissions do I need to change the operations master?

✂ Permissions may vary depending on your network configuration, but generally, you need to be a member of the Enterprise Admins group. For most Active Directory operations, your user account should be a member of this group so that you can have proper permissions to handle Enterprise tasks and issues, such as transferring the operations master role.

# Is there more than one operations master role?

✂ Yes. By using the transfer option, you are transferring the operations master that handles domain naming, which is called the *domain-naming master*. Other operations master roles exist, depending on your Enterprise configuration, including Schema Master, Relative ID Master, PDC Emulator, and Infrastructure Master. These master roles are automatically configured by the Active Directory. For example, if you upgrade a PDC from Windows NT 4.0 in a mixed environment, that server will automatically be a PDC Emulator.

![](bbox=[0.03, 0.49, 0.49, 0.8])

![](bbox=[0.5, 0.49, 0.93, 0.8])

+   **3** Choose **Action**\> **Operations Master**.

+   **4** Click **Change** to transfer the operations master role to the other domain controller you have connected to.

+   **5** Click **Close**.