9 Save the file. You are now ready to create the makefiles for both the encode and decode programs.

10 Enter the following code in the editor, and save it in the file `encode_make`:

```
encode: encode.o encode_file.o
gcc encode.o encode_file.o -o encode

encode.o: encode.c
gcc -c encode.c

encode_file.o: encode_file.c
gcc -c encode_file.c
```

11 Create a file named `decode_make`, and enter this code:

```
decode: decode.o decode_file.o
gcc decode.o decode_file.o -o decode

decode.o: decode.c
gcc -c decode.c

decode_file.o: decode_file.c
gcc -c decode_file.c
```

12 Save the file. You are ready to build the programs.

13 Type `make -f encode_make` and press Enter.

14 Type `make -f decode_make` and press Enter. Your screen should resemble Figure 10-14.

![](bbox=[0.2, 0.59, 0.76, 0.91])

Figure 10-14: Output of make commands