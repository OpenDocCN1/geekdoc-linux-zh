# COMMAND OPTIONS

+   **-in** *filena*
+   This specifies the input filena to read data from or standard input if this option is not specified.

+   **-out** *filena*
+   specifies the output filena to write to or standard output by default.

+   **-inkey** *file*
+   the input key file, by default it should be a private key.

+   **-keyform** *PEM\|DER*
+   the key format *PEM*, *DER* or *ENGINE*.

+   **-passin** *arg*
+   the input key password source. For more information about the format of *arg* see the *PASS PHRASE ARGUMENTS* section in (1).

+   **-peerkey** *file*
+   the peer key file, used by key derivation (*agreet*) operations.

+   **-peerform** *PEM\|DER*
+   the peer key format *PEM*, *DER* or *ENGINE*.

+   **-engine** *id*
+   specifying an engine (by its unique *id* string) will cause *pkeyutl* to attempt to obtain a functional reference to the specified engine, thus initialising it if needed. The engine will then be set as the default for all available algorithms.

+   **-pubin**
+   the input file is a public key.

+   **-certin**
+   the input is a certificate containing a public key.

+   **-rev**
+   reverse the order of the input buffer. This is useful for so libraries (such as CryptoAPI) which represent the buffer in little endian format.

+   **-sign**
+   sign the input data and output the signed result. This requires a private key.

+   **-verify**
+   verify the input data against the signature file and indicate if the verification succceeded or failed.

+   **-verifyrecover**
+   verify the input data and output the recovered data.

+   **-encrypt**
+   encrypt the input data using a public key.

+   **-decrypt**
+   decrypt the input data using a private key.

+   **-derive**
+   derive a shared secret using the peer key.

+   **-hexdump**
+   hex dump the output data.