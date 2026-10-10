# ## Cryptography Digital Signature

Have you ever signed a document physically? Do you know the importance and implication of your action? I am sure you understand if it is a matter of life and death. Well, a digital signature is like your handwritten signatures or typed messages, which is a binding signatory to that message or document. It is a technique, which binds an entity/person to digital data or information. Both the receiver and any third party can independently verify this binding.

In the physical world, when we sign documents, it is a sign of assurance that such a message is from the sender, and there shouldn't be any repudiation of the original message. In the case of a digital signature, the signer only knows the secret key.

The model of the digital signature system is based on public-key cryptography, and the diagram below shows the entire process involved.

![](bbox=[0.21, 0.47, 0.79, 0.68])

The following is an explanation of what goes on in the entire process:

+   * Each individual implementing the digital signature has his or her own pair of the public or private key

+   * Normally, the keys used for the encryption and decryption process is different from that use in the signing and verification process. The signature key is the private key whereas the verification key is the public key