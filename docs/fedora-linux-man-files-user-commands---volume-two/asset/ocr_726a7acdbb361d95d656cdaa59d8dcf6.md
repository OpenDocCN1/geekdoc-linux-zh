# OPTIONS

**-out *filename***

the output filename. If this argument is not specified then standard output is used.

**-passout *arg***

the output file password source. For more information about the format of **arg** see the PASS PHRASE ARGUMENTS section in (1).

**-aes128|-aes192|-aes256|-camellia128|-camellia192|-camellia256|-des|-des3|-idea**

These options encrypt the private key with specified cipher before outputting it. If none of these options is specified no encryption is used. If encryption is used a pass phrase is prompted for if it is not supplied via the **-passout** argument.

**-F4|-3**

the public exponent to use, either 65537 or 3. The default is 65537.

**-rand *file(s)***

a file or files containing random data used to seed the random number generator, or an EGD socket (see (3)). Multiple files can be specified separated by a OS-dependent character. The separator is `;` for MS-Windows, `,` for OpenVMS, and `:` for all others.

**-engine *id***

specifying an engine (by its unique **id** string) will cause **genrsa** to attempt to obtain a functional reference to the specified engine, thus initialising it if needed. The engine will then be set as the default for all available algorithms.

**numbits**

the size of the private key to generate in bits. This must be the last option specified. The default is 512.