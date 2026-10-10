+   * **HID protocol** a protocol concerning two units: the device, which is the entity that directly interacts with the user; and the host that communicates with the device and receives input data from the device on actions performed by the user
+   * **Master Session Key (MSK)** a cryptographic key used to generate working session keys for the encrypted exchange of information between two devices
+   * **Pairing** the process by which two Bluetooth-enabled devices agree to communicate with each other and establish a connection
+   * **Piconet** a short-range, ad hoc network linking a group of Bluetooth-enabled devices

# Introduction to Bluetooth Hacking

**Bluetooth** is a short-range wireless communication technology intended to replace the cables connecting portable or fixed devices while maintaining high levels of security. It allows mobile phones, computers, and other devices to exchange information using a short-range wireless connection. The process by which two Bluetooth-enabled devices agree to communicate with each other and establish a connection is known as *pairing*.

The following are some common uses of Bluetooth:

+   * Transferring data between mobile devices and PCs
+   * Connecting a printer, keyboard, or mouse to a PC without cables
+   * Sending photos and ringtones from one device to another

Bluetooth technology has achieved global acceptance. Any Bluetooth-enabled device, almost anywhere in the world, can connect to other nearby Bluetooth-enabled devices and communicate via short-range, ad hoc networks known as *piconets*.

Security within Bluetooth itself covers three main areas:

+   1. Authentication
+   2. Authorization
+   3. Encryption

This chapter focuses on Bluetooth and the security issues involved with it. It discusses the different types of attacks hackers make against Bluetooth-enabled devices, as well as tools that make Bluetooth more secure.

# Bluetooth Security Issues

The following are some of the major security issues related to Bluetooth:

+   * Bluetooth allows the use of short PINs to generate encryption keys and links. Because it is relatively easy to discover short PINs, their use can compromise the security of the Bluetooth connection.
+   * The length of the encryption key is negotiable. A stronger initialization key generation process is required to increase Bluetooth security.
+   * Unit keys are reusable, and once used they become public. A unit key is a link key that one device generates and uses as a link key with any other device. Unit keys can be safely used only under full-trust environments because every paired device can copy any other device holding the same unit key.
+   * The master key of paired devices is shared. Using a superior broadcast keying method can increase Bluetooth security.
+   * An attacker can gain unauthorized access to two other users if that attacker has communicated with either of the other two users before. This is mainly because the link key that has resulted from shared information is disclosed.
+   * In Bluetooth communications, only the device is authenticated, not individual users. This means anyone can use the device as long as it is authenticated. For improved security, application-level security and user authentication could be employed.
+   * End-to-end security is not performed. Only the individual links are encrypted and authenticated, making it possible to decrypt the data at intermediate points.
+   * Security services are limited in Bluetooth. Auditing, nonrepudiation, and other types of services do not exist.