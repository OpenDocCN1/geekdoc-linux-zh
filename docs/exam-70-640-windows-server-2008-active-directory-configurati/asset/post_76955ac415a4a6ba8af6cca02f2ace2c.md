
![](img/a8ee53dbf1310726255b6fbb9f296fb2_199_0.png)

The three subcategories within the Account Policies category of the security settings are **Password Policies**, **Account Lockout Policies**, and **Kerberos Policies**. Figure 8-1 shows the expanded Password Policy category within the security settings of the Default Domain Policy GPO for lucerne publishing.com. Note that the figure shows default settings for this policy. Settings in this category focus on enforcing password length, password history, and so on. Password Policies can be applied to domain and local user accounts.

### Figure 8-1
The Default Domain Password Policy in Windows Server 2008

![](img/a8ee53dbf1310726255b6fbb9f296fb2_199_1.png)

### Define a Domain-Wide Account Policy

1.  **Open** the GPMC. Click **Forest:** *<Forest Name>*, click **Domains**, click *<Domain Name>*, and then click **Group Policy Objects**.
2.  Right-click the Default Domain Policy and click **Edit**. A Group Policy Management Editor window for this policy is displayed.
3.  In the left window pane, expand the Computer Configuration node, expand the Policies node, and expand the Windows Settings folder. Then, expand the Security Settings node. In the Security Settings node, expand Account Policies and select **Password Policy**. This displays the available settings for this category of the GPO, similar to what you saw in Figure 8-1. All settings reflect the implemented defaults when the domain was created.
4.  To modify a setting, double-click the setting in the right window pane to open the Properties dialog box for the setting. Then, make the desired value changes. For example, double-click the **Enforce password history** setting, change the value to 22 and then click **OK** to change the domain-wide password history from 24 remembered passwords to 22.
5.  Click **OK** to close the setting's Properties dialog box.
6.  Close the Group Policy Management Editor window for this policy.

**PAUSE.** You can close the GPMC MMC snap-in or leave it open for the next exercise.

Figure 8-2 illustrates the expanded Account Lockout Policy category within the security settings of the Default Domain Policy GPO for lucerne publishing.com. Account Lockout Policies can be used for domain and local user accounts. An Account Lockout Policy specifies the number of unsuccessful logon attempts that, if made within a contiguous time frame, may constitute a potential security threat from an intruder. An Account Lockout Policy can be set to lock the account in question after a specified number of invalid attempts. Additionally, the policy specifies the duration that the account remains locked.

### Figure 8-2
The Default Domain Account Lockout Policy in Windows Server 2008

![](img/a8ee53dbf1310726255b6fbb9f296fb2_200_0.png)

### Configure a Domain-Wide Account Lockout Policy

1.  **Open** the GPMC. Click **Forest: <Forest Name>**, click **Domains**, click **<Domain Name>**, and then click **Group Policy Objects**.
2.  Right-click the **Default Domain Policy** and click **Edit**. A Group Policy Management Editor window for this policy is displayed.
3.  In the left window pane, expand the **Computer Configuration** node, expand the **Policies** node, and expand the **Windows Settings** folder. Then, expand the **Security Settings** node. In the Security Settings node, expand **Account Policies** and select **Account Lockout Policy**. The available settings for this category of the GPO are displayed.
4.  In the right window pane, double-click the **Account lockout duration** policy setting to view the Properties dialog box.
5.  Select the **Define This Policy Setting** checkbox. Note the default setting of 30 minutes for Account Lockout Duration. If you want to change the account lockout duration, you may do so here.
6.  Click **OK** to accept the specified lockout duration. The Suggested Value Changes dialog box, which indicates other related settings and their defaults, is displayed.
7.  Click **OK** to automatically enable these other settings or click **Cancel** to go back to the Account Lockout Duration Properties dialog box.
8.  Click **OK** to accept the additional setting defaults.
9.  Make any additional changes, as necessary, to the other individual Account Lockout Policy settings.
10. Close the Group Policy Management Editor window for this policy.

**PAUSE.** **Leave** the GPMC open for the following exercise.

You have now configured a domain-wide password policy that will configure consistent password settings across an entire domain.

## Configuring Fine-Grained Password Policies

> Prior to Windows Server 2008, an Active Directory administrator was only able to configure a single Password Policy and Single Lockout Policy for any Active Directory domain. If you were faced with a subset of users whose password policy requirements were different, you were left with the choice of configuring a separate domain or forcing all users within the domain to conform to a single password policy. Beginning in Windows Server 2008, you can configure Fine-Grained Password Policies, which allow you to define multiple password policies within a single domain.

To enable Fine-Grained Password Policies, Windows Server 2008 introduces a new object type called msDS-PasswordSettings, also called a Password Settings Object (PSO). Each PSO has the following mandatory attributes:

- **cn.** The common name for the PSO, such as “ServiceAccountNoLockout.”
- **msDS-PasswordSettingsPrecedence.** In a case where multiple PSOs apply, this attribute of the PSO is used as a tie-breaker to determine which PSO should apply: a PSO with a precedence of 1 will be applied over a PSO with a precedence of 5, a PSO with a precedence of 10 will be applied over a PSO with a precedence of 100, and so on.
- **msDS-PasswordReversibleEncryptionEnabled.** This attribute indicates whether the PSO allows passwords to be stored in Active Directory using reversible encryption. This setting should only be enabled if a particular application requires it, because it presents a significant security risk.
- **msDS-PasswordHistoryLength.** This attribute indicates the number of passwords that Active Directory should retain in memory before allowing someone to reuse a previously used password. Setting this attribute to a value of “2,” for example, would prevent someone from reusing the previous two passwords that they had configured for their user account. This setting corresponds to the Enforce Password History setting in Group Policy.
- **msDS-PasswordComplexityEnabled.** This attribute indicates whether the PSO requires a complex password; that is, a password that uses a mixture of uppercase and lowercase letters, numbers, and symbols. The default password policy in Windows Server 2008 requires the use of complex passwords.
- **msDS-MinimumPasswordLength.** This attribute indicates the minimum length of a password defined by this PSO.
- **msDS-MinimumPasswordAge.** This attribute is a negative number that indicates the number of milliseconds old a password must be before it can be changed. The default value is -864000000000, which equates to one day.
- **msDS-MaximumPasswordLength.** As the name indicates, this attribute identifies the maximum length of a password defined by this PSO.
- **msDS-MaximumPasswordAge.** This attribute is a negative number that indicates in milliseconds when a password will expire. The default value is -3628800000000, or 42 days.
- **msDS-LockoutThreshold.** This attribute indicates the number of bad login attempts permitted before an account is locked out.
- **msDS-LockoutObservationWindow.** This attribute is a negative number that indicates the number of milliseconds that must pass before the counter for failed logon attempts should be reset.
- **msDS-LockoutDuration.** This attribute is a negative number expressed in milliseconds that indicates how long an account will remain locked out. A value of “0” indicates that the account will stay locked out until it is manually unlocked by an administrator.

You can create one or more PSOs within a domain and then configure each PSO to apply to one or more user or group accounts within the domain; these objects are not created using the Group Policy Management Editor, but by manually creating the object using ADSIEdit or LDP/LDIFDE. When a user logs on to the domain, Windows Server 2008 uses the following steps to determine the user’s effective password requirements:

1.  Are one or more PSOs assigned to the individual user account? If so, use the PSO that has the winning precedence. If not, continue to step 2.
2.  Are one or more PSOs assigned to a group that has the user account as a member, either directly or through nested group membership? If so, use the PSO that has the winning precedence. If not, continue to step 3.
3.  If PSOs are not assigned to the user or to any group that has the user as a member, apply the domain-wide password policy and account lockout requirements.
