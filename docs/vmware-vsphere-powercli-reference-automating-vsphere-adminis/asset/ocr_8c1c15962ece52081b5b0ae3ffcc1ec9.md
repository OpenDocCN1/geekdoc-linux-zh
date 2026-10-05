# NO, YOU DON'T HAVE TO TYPE ALL CODE

Several of the scripts we show are quite long, at least for a PowerShell script. Of course, you will not have to type them in. You will be able to download all the scripts from book's web page at www.wiley.com/go/vmwarevspherecli2e.

When you use a script as opposed to a module? Well, the two types of files are very similar. They both contain PowerShell code, they both contain code that has been written to be reused, and they can be used from the command line or from the PowerShell ISE. The difference between them is the intended usage. A PowerShell script (ps1) is intended to be executed like a cmdlet or from the command line. Conversely, a PowerShell module (ending with psm1) is meant to be included, or referenced, from a script or from the command line.

# Executing a Script

The reason you're reading this book is that you want to take advantage of CLI and its ability to automate your infrastructure. As you begin to explore the world of CLI and PowerShell, you will encounter many snippets and scripts that you can take advantage of. However, you need to ensure that your environment is configured and ready to execute scripts before using them in production. This means you must ensure that the PowerShell execution policy is configured correctly to allow your scripts to execute.

The default execution policy is set to Restricted. This mode will allow the execution of individual commands, for example from the CLI, but will not script execution. To begin using CLI modify the policy to use something restrictive but still secure. The best option is to use the RemoteSigned value, which will enable executing scripts that you have created, but not those that have been downloaded from the Internet.

> TIP If you copy and paste code from a web page into your PowerShell window, the code will execute normally. Likewise, if you copy that text into a file and save it with the correct extension, it will execute as expected. This restriction applies to files that were downloaded from the Internet, meaning you have clicked a link and chosen to save the file locally. The RemoteSigned policy prevents a script from an untrusted source from executing malicious content on your desktop or server, and it's important to keep this security mechanism in place.