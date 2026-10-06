# Special Instructions 16

# CHAPTER CONTENTS

+   16.1 Intel® Advanced Encryption Standard New Instructions (AES-NI) ..................... 275
16.1.1 Further Reading ................................................................................................ 276
16.2 PCLMUL-Packed-Carry-Less-Multiplication................................................................. 276
16.2.1 Further Reading ................................................................................................... 277
16.3 CRC32 ................................................................................................................ 277
16.3.1 Further Reading ................................................................................................... 277
16.4 SSE4.2 String Functions ............................................................................ 277
16.4.1 Further Reading ................................................................................................ 278

The x87 floating point instructions were added to the x86 instruction set in order to alleviate a few specialized problems. Over the years, the Intel® Architecture has collected quite a few specialized instructions that are designed to simplify the lives of developers and improve performance. One of the associated challenges is that as the number of instructions increases, it can be hard for someone not familiar with the architecture to find helpful instructions. The author thought it fitting to close the book by highlighting some of these lesser known instructions. Additional information can be found in the whitepapers listed at the end of each section and within the Intel® Software Developer Manual and Optimization Reference.

# 16.1 INTEL® ADVANCED ENCRYPTION STANDARD NEW INSTRUCTIONS (AES-NI)

Typically, one of the largest challenges to the wide adoption of security measures is performance. Despite the wide users places on security, their behavior is strongly influenced by what they perceive to improve their performance, and what they perceive to impede their performance. As a result, providing high performance encryption and decryption is a prerequisite for enabling ubiquitous encryption.

275