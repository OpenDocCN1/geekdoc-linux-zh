# OffSec

Penetration Testing with Kali Linux

The directories in the PATH environment variable match paths used in the CreateFile calls recorded by Process Monitor.

So far, we know that the service binary tries to locate a file called myDLL.dll, but fails to do so. To abuse this, we can write to a DLL file with a name to a path used by the DLL search order. The first call attempts to locate the DLL in the Documents folder of steve. Because it's a home directory of steve, we have permissions to write to this folder and can place a malicious DLL then restart the service to load it.

Before we create a DLL, let's briefly review how a DLL works and how it may lead us to code execution. Each DLL can have an optional entry point function named DllMain, which is executed when processes or threads attach the DLL. This function generally contains cases DLL_PROCESS_ATTACH, DLL_THREAD_ATTACH, DLL_THREAD_DETACH, DLL_PROCESS_DETACH. These cases handle situations when the DLL is loaded or unloaded by a process or thread. They are generally used to perform initialization tasks for the DLL or tasks relating to the existing DLL. If a DLL doesn't have a DllMain entry point, it only provides resources.

The following lists you a code example from Microsoft, outlining a basic DLL in C++. The DLL contains the entry point function DllMain and the previously mentioned cases in a switch statement. Depending on the value of ul_reason_for_call one of these cases gets executed. As of now, all cases use a break statement.

```
BOOL APENTRY DllMain(
HMODULE hModule, // Handle to DLL module
DWORD ul_reason_for_call, // Reason for calling function
LPVOID lpReserved) // Reserved
{
    switch (ul_reason_for_call )
    {
        case DLL_PROCESS_ATTACH: // A process is loading the DLL.
            break;
        case DLL_THREAD_ATTACH: // A process is creating a new thread.
            break;
        case DLL_THREAD_DETACH: // A thread exits normally.
            break;
        case DLL_PROCESS_DETACH: // A process unloads the DLL.
            break;
    }
    return TRUE;
}
```

Listing 432 - Code example of a basic DLL in C++

The provided comments from Microsoft state that DLL_PROCESS_ATTACH is used when a process is loading the DLL. Since the target service binary in our example tries to load the DLL, this is the case we need to add our code to.

Let's use the code from the previous section to build the C++ DLL code. Adding the include statement as well as the system call code, we need to use an include statement for

803 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/troubleshooting/windows-client/deployment/dynamic-link-library#the-dll-entry-point
804 (Wikipedia, 2022), https://en.wikipedia.org/wiki/C%20%28B

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

512