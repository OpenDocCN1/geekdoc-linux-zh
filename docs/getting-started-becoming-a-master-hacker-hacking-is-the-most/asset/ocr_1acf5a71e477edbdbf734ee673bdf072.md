As you can see in this screenshot, there are two types of msfvenom formats, (1) Executable Formats and Transform Formats. The Executable Formats will create an executable file of some type such as a Windows .exe or a Linux .elf. Executable Formats are the type we will focus on here. These create an executable file that--when opened--will trigger a payload. Transform formats create a payload into a different format such as C or Java. Transform Formats are used in creating your own exploit (we'll cover these in my upcoming book focusing just on Metasploit, “Metasploit Basics for Hackers”).

To view the list of encoders for obscuring the nature of the payload, we can enter; `169 | P a g e`

```
```
root@kali:~: # msfvenom -l encoders
Framework Encoders [ -e<encoder -<value> ]
----------------------------------------------------

Name                          Rank            Description
-----                         ----            ---------------------------------------------------------
cmd/brace                     low             Bash Brace Expansion Command Encoder
cmd/echo                      good            Echo Command Encoder
cmd/generic_sh                manual          Generic Shell Variable Substitution Command Encoder
cmd/sh$                       low             Bourne (sh/sh$) Substitution Command Encoder
cmd/perl                      normal          Perl Command Encoder
cmd/powershell_base64         excellent       PowerShell Base64 Command Encoder
cmd/print p_mp_magic          manual          print( ) via Pmp magic_quotes_utility Command Encoder
generic/c16r                  manual          The C16R Encoder
generic/none                  normal          The 'none' Encoder
mipsbe/xor_xori              manual          Byte XORi Encoder
mipsbe/longxor               normal          XOR Encoder
mipsle/byte_xorx             normal          Byte XORi Encoder
mipsle/longxor               normal          XOR Encoder
php/base64                   great            PHP Base64 Encoder
ppc/longxor                  normal           PPC LongXOR Encoder
ppc/longxor_tag              normal           PPC LongXOR Encoder
ruby/base64                  great           Ruby Base64 Encoder
sparc/longxor_tag            normal           SPARC ENCODE XOR Encoder
x64/xor                      normal           XOR Encoder
x86/xor_dynamic              manual           Dynamic Key XOR Encoder
x64/zutto_dckiru             manual          Zutto Dckiru
x86/add_sub                  manual           Add/Sub Encoder
x86/alpha_mixed              low             Alapha Alphanumeric Mixedcase Encoder
x86/alpha_upper              low             Alapha Alphanumeric Uppercase Encoder
x86/avoid_underscore_tolower manual           Avoid underscore/tolower
x86/avoid_UTF8_tolower       manual           Avoid UTF8_tolower
x86/xor                      manual           BLOXor - A Metamorphic Block Based XOR Encoder
x86/bgp_polyglot             manual           BGP Polyglot
x86/c4le_dword_xor           normal          C4Le Dword XOR Encoder
x86/context_cpuid            manual           CPUCID-based Context keyed Payload Encoder
x86/context_static           manual           statC()D-based Context keyed Payload Encoder
x86/context_time             manual           time( )-based Context keyed Payload Encoder
x86/coundtow                 normal          Single-byte XOR Coundtow Encoder
x86/fifteen_xox              normal          Variable-length Fifteen/nr Dword XOR Encoder
x86/jmp_call_additive        normal          Jmp/Call XOR Additive Feedback Encoder
x86/nota1ghpa                low             Non-Alpha Encoder
x86/noupper                  low             Non-Upper Encoder
x86/opt_sub                  manual           Sub Encoder (optimized)
x86/service                  manual           Register Service
x86/shika ga_nai             excellent        Polymorphic XOR Additive Feedback Encoder
x86/single_static_bit        manual           Single Static Bit
x86/unicode_mixed            manual          Alapha Alphanumeric Unicode Mixedcase Encoder
x86/unicode_upper            manual          Alapha Alphanumeric Unicode Uppercase Encoder
x86/xor_dynamic              normal           Dynamic Key XOR Encoder
```
```