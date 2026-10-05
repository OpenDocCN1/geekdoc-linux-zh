Close the Invoke-LocalPSScriptReturnCode workflow and then Save And Close the workflow.

You are now ready to use the New-ADUser workflow. Run it and set the parameters as follows (Figure 21.42):

firstName: Buffy (First Name of the new user)

surname: Summers (Surname of the new user)

ou: Ou=Users,OU=HQ,DC=sunnydale,DC=local (DN of the OU for the user)

keepTogether: No

adUsername: Sunnydale\scott (AD account with AD rights to create the new user)

adPassword: ***** (password for that username)

# FIGURE 21.42 Starting the New-ADUser workflow

![](bbox=[0.283, 0.442, 0.881, 0.827])