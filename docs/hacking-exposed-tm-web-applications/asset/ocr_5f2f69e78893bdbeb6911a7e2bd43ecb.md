# 358 Hacking Exposed Web Applications

# Unattended IISLockdown Installation

For those who wish to automate the deployment of the IIS Lockdown wizard and UrlScan across multiple servers, IISLockdown can be configured to run in an unattended fashion according to predefined settings specified in a file called islockdown.ini. The [Info] section contains basic configuration information used by the IIS Lockdown wizard. The short file RunLockUnattended comes with the IIS Lockdown installation explains the basics of configuring islockdown.ini files and there is a sample islockdown.ini file available in the distribution (don't delete or overwrite this original, as it contains the syntax for configuring all available!). The key parameter is to Set Unattended=TRUE in the file, and run the IISLockdown tool in the desired directory as the islockdown.ini file using the command line or calling it from script. We've had erratic results using this feature (“No memory”) error messages), so your mileage may vary. It’s probably a better idea to integrate UrlScan into the standard template for servers throughout your organization, which means it will be deployed automatically with any new Web server in your configuration.

> The IISLockdown installer is named islockdown.exe, same as the tool itself—don’t mix them up!

# ADVANCED URLSCAN DEPLOYMENT

Whew—who would have thought the “basic deployment” would be so involved! If you ache for the simplicity of copying files around, and you’re going to get your hands dirty with some of the technical details, read on. Manually installing UrlScan involves the following steps:

+   - Extracting UrlScan.dll
- Configuring UrlScan.ini
- Installing UrlScan.dll as an API filter under IIS

We will discuss each one of these steps below. We will complete our discussion with some brief instructions on how to manually remove UrlScan. In order to perform the steps below, you will require:

+   - The latest UrlScan.exe installer (version 2.5 as of this writing; either Baseline or SRP is fine)
- The IISLockdown installer (iislockdown.exe)

Links to each of these items can be found in the “References and Further Reading” section at the end of this chapter.