# ## EXIT CODES

+   * 0
+   the operation was completely successfully.
+   * 1
+   an error occurred parsing the command options.
+   * 2
+   one of the input files could not be read.
+   * 3
+   an error occurred creating the PKCS#7 file or when reading the MIME ssage.
+   * 4
+   an error occurred decrypting or verifying the ssage.
+   * 5
+   the ssage was verified correctly but an error occurred writing out the signers certificates.