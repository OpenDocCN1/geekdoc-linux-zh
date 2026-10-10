# ## OPTIONS

**-out filename**
the output filename. If this argument is not specified then standard output is used.

**-outform DER|PEM**
This specifies the output format **DER** or **PEM**.

**-pass arg**
the output file password source. For more information about the format of **arg** see the **PASS PHRASE ARGUMENTS** section in (1).

**-cipher**
This option encrypts the private key with the supplied cipher. Any algorithm name accepted by *EVP_get_cipherbyname()* is acceptable such as **des3**.

**-engine id**
specifying an engine (by its unique **id** string) will cause **genpkey** to attempt to obtain a functional reference to the specified engine, thus initialising it if needed. The engine will then be set as the default for all available algorithms. If used this option should precede all other options.

**-algorithm alg**
public key algorithm to use such as **RSA**, **DSA** or **DH**. If used this option must precede any **-pkeyopt** options. The options **-paramfile** and **-algorithm** are mutually exclusive.

**-pkeyopt opt:value**
set the public key algorithm option **opt** to **value**. The precise set of options supported depends on the public key algorithm used and its implementation. See **KEY GENERATION OPTIONS** below for more details.

**-genparam**
generate a set of parameters instead of a private key. If used this option must precede and **-algorithm**, **-paramfile** or **-pkeyopt** options.

**-paramfile filename**
Some public key algorithms generate a private key based on a set of parameters. They can be supplied using this option. If this option is used the public key algorithm used is determined by the parameters. If used this option must precede and **-pkeyopt** options. The options **-paramfile** and **-algorithm** are mutually exclusive.

**-text**
Print an (unencrypted) text representation of private and public keys and parameters along with the PEM or DER structure.