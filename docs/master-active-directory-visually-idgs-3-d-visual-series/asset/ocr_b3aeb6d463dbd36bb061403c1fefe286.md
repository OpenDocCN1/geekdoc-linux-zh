![](bbox=[0.03, 0.13, 0.09, 0.2])

# Can I still use Windows NT Workstation or Windows 9x client computers in the domain after a change to native mode?

✔ Yes. The change to native mode affects only domain controllers. After you make the change, only Windows 2000 domain controllers can be used. However, client computers are not affected by the change to native mode, and you can still use a mix of Windows 2000, Windows NT, or Windows 9x client computers.

# Can’t I still use a Windows NT BDC after the change to native mode?

✔ No. Native mode allows only Windows 2000 servers. You cannot use Windows NT servers in the domain, regardless of the role they once played in a Windows NT network. Keep in mind that native mode erases any functionality with downlevel NT servers, so if your environment still uses NT servers, you should not change to native mode until they have all been upgraded.



VI

![](bbox=[0.0, 0.49, 0.46, 0.82])

![](bbox=[0.49, 0.49, 0.96, 0.82])

+   4 Click Yes to continue with the mode change.

+   The General tab now displays the Domain Operation Mode as native mode.

+   5 Click OK to close the Properties sheet.