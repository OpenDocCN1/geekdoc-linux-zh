# 160

# compress, uncompress, zcat

# Description

# compress

The compress command tries to reduce the size of the named files by using adaptive Ziv coding. Except when the output is to the standard output, each file is replaced by one with the extension .z, while keeping the same ownership modes, change times, and modification times.

If appending a .z to the file name would make the name exceed 14 bytes, the command fails. If no files are specified, the standard input is compressed to the standard output.

The amount of compression depends on the size of the input, the number of bits per code, and the distribution of common substrings. Typically, such source code or English is reduced by 50-60 percent. Compression is generally much better than that achieved by Huffman coding (as used in pack(-)) and takes less time to compute. The bits parameter specified during compression is encoded within the compressed file, along with a magic number to ensure that neither decompression of random data nor recompression of compressed data is followed afterwards.

> Note — Although compressed files are compatible between machines with large memory, use -b 12 for file transfer to architectures with a small process data state (64 kilobytes or less).

compress should be more flexible about the existence of the .z suffix.

# uncompress

The uncompress command restores files to their original state after they have been compressed by the compress command. If you specify no files, the standard input is uncompressed to the standard output.

This command supports the uncompressing of any files produced by compress. Files produced by compress on other systems, uncompress supports 9 to 16-bit compression (see -b).

# zcat

The zcat command writes to standard output the uncompressed form of files that have been compressed with compress. It is the equivalent of uncompress -c. Input files are not affected.

# Options

+   -b bits The upper limit (in bits) for common substring codes. Bits must be between 9 and 16 (16 is the default). Lowering the number of bits results in less compressed files.

+   -c Write to the standard output; change no files and create no .z files. The behavior of zcat is identical to that of uncompress -c.