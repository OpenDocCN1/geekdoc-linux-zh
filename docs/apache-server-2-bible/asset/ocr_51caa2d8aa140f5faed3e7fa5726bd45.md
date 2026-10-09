![](bbox=[0.125, 0.117, 0.189, 0.179])

> Most people forget to use `https` and use `http` when testing their SSL server and panic when they don't see an SSL connection (usually displayed by a small lock icon in the status bar of most popular Web browsers).

# # Getting a Certificate

Before you can use Apache with SSL (via mod\_ssl or Apache-SSL), you must create appropriate server certificate. You can get a server certificate from a commercial certificate authority or you can create your own certificate authority and then create certificates for your own servers and clients. The latter method is typically used for a large organization that wants to manage certificates between campuses internally.

# ## Getting a server certificate from a commercial CA

To get a signed certificate from a commercial CA, you must meet its requirements. There are two types of requirements:

+   You (the requester) must prove that you are the entity you claim to be.
+   
+   You must submit a Certificate Signing Request (CSR) in electronic form.

The first requirement is usually met by following the CA's guidelines for verifying individuals or organizations, so you must consult with your chosen CA to learn how to proceed. Typically, if you are planning on getting your Web server certified, be prepared to submit copies of legal documents, such as business registration or incorporation papers. Alternatively, you can create a CSR using OpenSSL.

The very first step in creating a CSR is to create a private key for your server. Then you need to create a certificate signing request that needs to be sent to a commercial certificate authority. After you have been approved by a commercial certificate authority you can install the certificate on your server and use SSL with Apache. I discuss these steps in detail in the following sections.

# ## Generating a private key

To generate an encrypted private key for a Web server host called `www.domain.com` run:

```
openssl genrsa -des3 -out www.domain.com.key 1024 -rand /dev/random
```

When you run this command, you are asked to enter a pass phrase (that is, a password) to encrypt the private key with it. Because the private key is encrypted using the `des3` cipher, you are asked to enter the pass phrase every time your server is started. If this is undesirable, you can create a nonencrypted version of the