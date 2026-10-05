# # OffSec

PS C:C:\Users\offsec\Desktop> .\bypass.ps1
.\bypass.ps1 : File C:\Users\offsec\Desktop\bypass.ps1 cannot be loaded because
running scripts is disabled on this
system. For more information, see about_Execution_Policies at
https://go.microsoft.com/fwlink/?linkID=135178.

```
At line:1
+ .bypass.ps1
+ -----------------------
+ CategoryInfo         : SecurityError: (:) ) PSExecutionException
+ FullyQualifiedError : UnauthorizedAccess
Listing 245 - Attempting to run the script and encountering the Execution Policies Error
```

Unfortunately, when you attempt to run our malicious script, we are presented with an error that
references the Execution Policies of our system, which appear to prevent your script from running.

A quick review of the Microsoft documentation on PowerShell execution (linked in the
error message), shows that these policies are set on a per-user rather than per-system basis.

> Keep in mind that much like anything in Windows, the PowerShell Execution
Policy settings can be dictated by one or more Active Directory GPOs.582 In those
cases, it may be necessary to search for additional bypass vectors.

Let's view and change the policy for our current user. Please note that in this instance,
we have chosen to change the policy globally rather than a per-script basis, which can be
achieved by using the -ExecutionPolicy flag for each script when it is run.

First, we are getting to retrieve the current execution policy by the Get-ExecutionPolicy -Scope
CurrentUser command and then it to Unrestricted via the Set-ExecutionPolicy-ExecutionPolicy
Unrestricted -ScopeCurrentUser.

```
PS C:C:\Users\offsec\Desktop> Get-ExecutionPolicy -Scope CurrentUser
Undefined
```

```
PS C:C:\Users\offsec\Desktop> Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope
CurrentUser
```

Execution Policy Change
The execution policy helps protect you from scripts that you do not trust. Changing
to the security risks described in the about_Execution_Policies help Module at
https://go.microsoft.com/fwlink/?linkID=135170. Do you want to change the execution
olicy?

```
[Y] Yes to All [N] No Lo to All [S] Suspend [?] Help (default is
""): A
```

```
PS C:C:\Users\offsec\Desktop> Get-ExecutionPolicy -Scope CurrentUser
Unrestricted
```

Listing 246 - Changing the ExecutionPolicy for your current user