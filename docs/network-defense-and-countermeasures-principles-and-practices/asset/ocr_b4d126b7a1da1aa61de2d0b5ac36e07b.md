+   - ShiftRows: A transposition step where each row of the state is shifted cyclically a certain number of steps. In this step the first row is left unchanged. Every byte in the second row is shifted one byte to the left (with the far left wrapping around). Every byte of the third row is shifted two to the left, and every byte of the fourth row is shifted to the left (again with wrapping around).

+   - MixColumns: A mixing operation that operates on the columns of the state, combining the 4 bytes in each column. In the MixColumns step, each column of the state is multiplied with a fixed polynomial.

With the aforementioned steps in mind, this is how steps are executed in the Rijndael cipher. 128-bit keys, there are 10 rounds. For 192-bit keys, there are 12 rounds. For 256-bit keys, there are 14 rounds.

+   - Key Expansion: The first step is that the round keys are derived from the cipher key using Rijndael's key schedule. The key schedule is how a key is generated for each round, based on the cryptographic key that was exchanged between the sender and receiver.

+   - Initial Round: This initial round will only execute the AddRoundKey step. This is simply XORing with the round key. This initial round is executed once, then the subsequent rounds will be executed.

+   - Rounds: This phase of the algorithm executes several steps, in the following order:

+   - SubBytes

+   - ShiftRows

+   - MixColumns

+   - AddRoundKey

+   - Final Round: This round has everything the rounds phase, except no MixColumns.

+   - SubBytes

+   - ShiftRows

+   - AddRoundKey

In the AddRoundKey step, the sub-key is XORed with the state. For each round, a sub-key is derived from the main key using Rijndael's key schedule; each sub-key is the same size as the state.

# IDEA

International Data Encryption Algorithm (IDEA) is another block cipher. This particular algorithm works with 64-bit blocks of data at a time and a 128-bit key. The procedure is fairly complicated and uses sub-keys generated from the key to carry out a series of modular arithmetic and XOR operations on segments of the 64-bit plaintext block. The encryption scheme uses a total of 52 16-bit sub-keys. These are generated from the 128-bit key with the following procedure:

+   - 128-bit key is split into eight 16-bit keys, which are the first eight sub-keys.