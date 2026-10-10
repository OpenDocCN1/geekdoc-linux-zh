**11.** Read the information and click **Next** in two windows to display the window shown in Figure 2-6.

![](bbox=[0.05, 0.13, 0.59, 0.36])

**12.** To create the first domain controller in a new Active Directory forest, select **Create a new domain in a new forest** and click **Next**.

**13.** You are prompted to enter the domain name of the Active Directory forest root domain. In this case, key lucernepublishing.com and click **Next**.

**14.** You are prompted to fill in the *domain netBIOS name* for this domain. The domain netBIOS name is limited to 15 characters and is maintained for legacy compatibility with older applications that cannot use DNS for their name resolution. In most cases, this name will simply be the first portion of the *fully qualified domain name (FQDN)*—LUCERNEPUBLISHING in the case of the lucernepublishing.com FQDN or SALES in the case of sales.lucernepublishing.com. However, because LUCERNEPUBLISHING is longer than 15 characters, you must select a shorter name. Enter LP as the domain netBIOS name as shown Figure 2-7 and click **Next**.

![](bbox=[0.05, 0.63, 0.59, 0.86])

**15.** You are prompted to select the forest functional level (FFL) and domain functional level (DFL) of the new domain and the new forest. As discussed in Lesson 1, the FFL and DFL are used to control what operating systems can be installed as domain controllers within a domain or forest. Raising the DFL or FFL will enable