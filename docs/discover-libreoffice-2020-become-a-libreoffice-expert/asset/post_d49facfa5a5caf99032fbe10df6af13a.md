
# GET PRODUCTIVE

## LibreOffice Typography

![](img/e39350c3a7c0d527d71b0e4097a0ba66_67_0.png)

Figure 5: Hyphenation controls improve the look of your document.

Writing Aids. Note that neither of these manual tools functions unless a word falls into the hyphenation range for that paragraph style.

The Hyphenation tool is so useful that LibreOffice users should get in the habit of using it immediately after spell checking on every document.

However, the Hyphenation tool is especially useful when you choose to have justified lines, where the characters fill all the space between the left and right margin. Left uncorrected, justified lines can leave unsightly irregular spacing. You can usually rid your documents of the irregular spacing so long as you are willing to take the time. The only problem you are likely to have is a short final line in a paragraph, and you can adjust its appearance by setting the paragraph style to Alignment | Justified | Last line Left.

### AUTOMATING ADVANCED FEATURES

Starting with the 5.3 release, LibreOffice uses the HarfBuzz font-rendering engine. HarfBuzz simplifies the use of features like small capitals and ligatures by using them automatically at appropriate times if the font supports them. No manual formatting, or even the modification of a style, is needed. For example, instead of using two separate “i”s, LibreOffice will use the special ligature “fi” if it is available, automatically adding professional typographical symbols. You can tell if a feature is available in a font because it appears in Insert | Special Character.

![](img/e39350c3a7c0d527d71b0e4097a0ba66_67_1.png)

Figure 6: Using the Hyphenation tool just before publishing improves your documents, especially those with justified paragraphs.

![](img/e39350c3a7c0d527d71b0e4097a0ba66_67_2.png)

Figure 7: With recent releases of LibreOffice, you can force the automatic use of advanced features by adding code snippets in any field for entering a font family. Here, Liberation Sans is set to use old-style figures and small capitals.

You can force an advanced feature’s use or turn it off from within any field to specify a font by typing a code tag written in lowercase characters directly after the font name, without any space in-between (Figure 7). For instance, :smcp or :smcp=on will both automatically turn lowercase letters into small capitals. If you want to turn off the use of small capitals, add :smcp=off. Multiple snippets can be added one after the other, so that :liga:onum:cpss forces the use of standard ligatures, old-style figures, and kerning for upper case letters.

In some cases, only the long form can be used, because you need to specify a variable. For example, :frac=1 forces the use of smaller-sized fractions with a diagonal separator, while :frac=2 forces the use of smaller-sized fractions with a horizontal separator. A complete list of available tags, including those for writing systems that do not use Latin characters, is available online [1]. Some of the most useful features are listed in Table 1.

**Table 1: Selected Codes for Advanced Features**

| Code | Function |
| :--- | :--- |
| :smcp | Converts uppercase letters to small capitals. |
| :liga | Applies standard ligatures. |
| :pnum | Converts old-style figures to proportional figures. |
| :onum | Converts all figures to old-style figures. |
| :frac=1 | Converts fractions to smaller-sized fractions with a diagonal line. |
| :frac=2 | Converts fractions to small-sized fractions with a horizontal line. |
| :kern | Kerns characters. |

With these codes, advanced typographical features can be set up once and saved in a template, allowing your documents to have the formatting of a professional publisher.

### THE COMPLETION OF A REVOLUTION

For almost 20 years, LibreOffice and its predecessors have produced good enough copy resulting in many technical publishers using LibreOffice files for book printing. Still, a few finishing details remained imperfect.

However, in the last few years, LibreOffice has added those finishing details. I can personally attest to the fact that LibreOffice can successfully replace FrameMaker for technical manuals and brochures. The result is a free layout tool as good as anything available for professional use.

**INFO**

- 1. List of available tags: https://en.wikipedia.org/wiki/List_of_typographic_features#OpenType_typographic_features

# Public Money
# Public Code

![](img/e39350c3a7c0d527d71b0e4097a0ba66_68_0.png)

Modernising Public Infrastructure with Free Software

# GET PRODUCTIVE

# Digital Signatures

## Using Digital Signatures

## Secure Documents

![](img/e39350c3a7c0d527d71b0e4097a0ba66_69_0.png)

> By adding a digital signature, you can boost your document's security. *By Bruce Byfield*

A digital signature verifies a document’s trustworthiness. It guarantees that the sender is who they claim to be, and that the document has not been edited since it was signed. Ordinary file sharing may not require one, but if privacy is important – particularly in business or when financial matters are discussed – then a digital signature is one of the main ways to safeguard a file’s contents.

Originally, a digital signature was created by a third-party certificate manager, which offered a certificate guaranteeing the document’s integrity. LibreOffice continues to refer to digital signatures as, but, somewhat confusingly, uses the same term to refer to a GNU Privacy Guard (GPG) key that serves the same purpose. GPG [1] is a cross-platform method of encryption that can be installed on Linux, macOS, or Windows. Although a third-party service refers to certificates and GPG refers to keys, both operate in a similar manner. Both consist of a private certificate or key and a public one that the recipient must be sent in order to read the sent files. As the originator, you can use the certificate or key to read your own encrypted files.

Creating either the certificate or the key is the time-consuming part of using a digital signature. Once you have created one, it is simply a case of associating the digital signature with the file, which is a matter of minutes in any of LibreOffice’s main modules.

## SETTING UP A CERTIFICATE

A few years ago, using a certificate authority was expensive. Practically speaking, certificate authorities were beyond the average home user’s means. However, today, many free certificate authorities exist. These free certificate authorities sometimes lack all the features of traditional certificate authorities, and the certificates they issue are sometimes valid for a limited time. For example, certificates from the Linux Foundation’s Let’s Encrypt [2] are only good for 90 days unless deliberately renewed. However, in many cases, these free certificates are good enough for the average user.

Describing the procedure for all major certificate authorities would be too lengthy to go into here. However, these steps for Let’s Encrypt (Figure 1) should be similar enough to those for other certificate authorities for you to adjust as needed:

- 1. Sign in and follow the steps to generate a certificate. You will be asked to name the certificate, specify the encryption type, identify the web server with which to associate the certificate, provide details about your location, and select whether you want to renew the certificate automatically or let it expire.
- 2. Add the certificate's URL in your web browser's preferences and set up and make it available for files.
- 3. Apply the certificate to a file via *File* | *Digital Signature* | *Digital Signatures* ..., and then restart Writer.

You will need the passphrase for the key (Figure 2). From the same dialog window, you can view or remove a certificate, as well as sign a document with it.

## USING GPG

GPG is a cross-platform encryption tool that is available under a variety of similar names. Using it for a digital certificate has the advantage of being free, requiring no registration, and expiring when you choose. In addition, because GPG keys are a self-contained system, they do not need to be registered on a web server to be used – although you do need to send your public encryption key separately to those who will receive your files.

To generate keys with GPG, run the command:

```
gpg --full-generate-key
```

GPG takes you through five steps to create a key: adding your name and email, creating a passphrase, choosing the algorithm, setting the key size, and assigning an expiration date. If you are unsure about some of the possible choices, you can simply accept the defaults. These don't always offer the highest level of encryption, but they should be adequate in most cases. If you want the highest possible security, you can always research the choices as you encounter them (Figure 3).

As a last step, you should create a revocation certificate so that you can make the new key invalid if it is ever compromised by running the command:

```
gpg --armor --output revoke.asc \
--gen-revoke PUBLIC-KEY-ID
```

Once the key is created, you can send out the public key to the intended recipients of your digitally signed files with

```
gpg --output YOURNAME.gpg \
--export KEY-EMAIL
```

or as a protected plain text file with the format:

```
gpg --armor --output YOURNAME.gpg \
--export KEY-EMAIL
```

From within LibreOffice, the key can be selected from *Files* | *Digital Signature* | *Digital Signature* ..., by navigating to the directory where it is located.

Recipients of the file who have your public key can verify it is from you with:

```
gpg --fingerprint KEY-EMAIL
```

![](img/e39350c3a7c0d527d71b0e4097a0ba66_70_0.png)

![](img/e39350c3a7c0d527d71b0e4097a0ba66_70_1.png)

```
bb@nanday:$ gpg --full-generate-key
   gpg (GnuPG) 2.1.18; Copyright (C) 2017 Free Software Foundation, Inc.
   This is free software: you are free to change and redistribute it.
   There is NO WARRANTY, to the extent permitted by law.

   Please select what kind of key you want:
    (1) RSA and RSA (default)
    (2) DSA and Elgamal
    (3) DSA (sign only)
    (4) RSA (sign only)
   Your selection?
```

Figure 3: GPG keys are a modern alternative to using a certificate.
