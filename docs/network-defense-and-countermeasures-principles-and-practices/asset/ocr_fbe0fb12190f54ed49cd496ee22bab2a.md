# CHAPTER 6 Encryption Fundamentals

To decrypt you take the ciphertext, and raise it to the $d$ power modulo $n$:

$P = c^d \pmod n$

If this seems a bit complex to you, you must realize that many people work in network security without being familiar with the actual algorithm for RSA (or any other cryptography for that matter). You can also get a better understanding of RSA by walking through the algorithm utilizing small integers.

Normally RSA is done with large integers. To make the math easy to follow, this example uses small integers (Note: This example is from Wikipedia):

+   1. Choose two distinct prime numbers, such as $p = 61$ and $q = 53$.

+   2. Compute $n = pq$ giving $n = 61 \times 53 = 3233$.

+   3. Compute the totient of the product $\Phi(n) = (p-1)(q-1)$ giving $\Phi(3233) = (61-1)(53-1) = 3120$.

+   4. Choose any number $1 < e < 3120$ that is co-prime to 3120. Choosing a prime number for we leaves us to check that $e$ is not a divisor of 3120. Let $e = 17$.

+   5. Compute $d$, as shown before that $de \pmod m \equiv 1$; yielding $d = 2753$.

+   6. The **public key** is $(n = 3233, e = 17)$. For a plaintext message $m$, the encryption function is $m^{17}$ (mod 3233).

+   7. The **private key** is $(n = 3233, d = 2753)$. For an encrypted ciphertext $c$, the decryption function is $c^{2753}$ (mod 3233).

RSA is based on prime numbers. You might think, "Couldn't someone take the public key and use factoring to derive the private key?" Well, hypothetically, yes. However, it turns out that factoring large numbers into their prime factors is pretty difficult. No efficient algorithm exists for doing it. By "large numbers," we mean RSA can use 1024, 2048, 4096-bit and larger keys. Those make for some huge numbers. Or, if anyone ever invents an efficient algorithm that factor a large number into its prime factors, RSA would be dead.

RSA has become a popular encryption method. It is considered quite secure and is used in situations where a high level of security is needed.

# Diffie-Hellman

Now that you have seen RSA, consider a few asymmetric algorithms. Perhaps the well known is Diffie-Hellman, which was the first described asymmetric algorithm.

This cryptographic protocol allows two parties to establish a shared key over an insecure channel. In other words, Diffie-Hellman is often used to allow parties to exchange a symmetric key through some insecure medium, such as the Internet. It was developed by Whitfield Diffie and Martin Hellman in