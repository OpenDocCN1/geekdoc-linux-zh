The potential for easier management on an enterprise level. To identify and con- figure your system with the proper settings to disallow anonymous connections and enumerations, refer to the recommendations in Table 4.6. The recommend- mations in the table are separated by the name precursor, configuration object, and the corresponding recommended value.

The “Allow SID/Name translation” object allows an anonymous user to query the system with systems IDs (SIDs), and in the case that a corre- spending user, that name is returned. The “Do not allow anonymous enumeration of SAM accounts and shares” disallow unauthenticated users from determining what users and shares are on the XP system. With the same respect, the object that allows shares to be accessed anonymously should be empty unless there is a specific requirement of your system. The “Named Pipes that can be accessed anonymously” is referring to XP initiated communication sessions for internal processes, in which you specify that anonymous users may have access. Lastly, the “Let everyone permits to anonymous users” is somewhat unique is the most dangerous object because it has the potential to allow unauthorized users to inherit the configured Everyone group permissions.

# Table 4.6 Network Access Configurations for Anonymous Connections

| Name Precursor | Configuration Object Name | Value |
| --- | --- | --- |
| Network access | Allow anonymous SID/Name translation | Disabled |
| Network access | Do not allow anonymous enumeration of SAM accounts | Enabled |
| Network access | Do not allow anonymous enumeration of SAM accounts and shares | Enabled |
| Network access | Let Everyone permissions apply to anonymous users | Disabled |
| Network access | Named Pipes that can be accessed anonymously | NONE |
| Network access | Shares that can be accessed anonymously | NONE |

Figure 4.10 details what your security options should look like after you have implemented these selections.