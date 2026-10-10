+   - Algorithm for creating the certificate (default is SHA-1)
+   - How long the certificate will remain valid (default is two years)
+   - Certificate root (default is your organizational certificate)

# Creating Trusted Root Certificates

Trusted root certificates provide the certificates from other organizations that your server will trust automatically. You can use iManager to add trusted root certificates to your eDirectory tree in the specified container by clicking the Create Trusted Root link and entering the following information:

+   - **Name**—The eDirectory object to be assigned to this trusted certificate
+   - **Container**—The name of the eDirectory trusted root container to store the trusted certificate object
+   - **Certificate file**—The path of the certificate file you have received from the CA

# Creating User Certificates

For users to make use of a Public Key Infrastructure application, such as an e-mail system, they need key-pair certificates assigned to their user accounts. In the following activity, you use iManager to create user certificates in eDirectory.

![](bbox=[0.04, 0.41, 0.08, 0.45])

# Activity 11-6: Creating User Certificates

Time Required: 15 minutes

Objective: Use iManager to access and manage user certificates with the Novell Certificate Services.

Requirements: A Windows XP or SUSE Linux 10 computer

Description: Eric is planning to set up an e-mail system that uses PKI to encrypt user e-mail transactions and wants you to create certificates for users in the IT Department. In this activity, you use iManager to create certificates for all users in your IT OU.

+   1. If necessary, log on to your local computer, start your Web browser, start iManager, and log in with your administrative user name and password.
+   2. Click to expand the **Novell Certificate Server** heading and then click the **Create User Certificate** link to display the Create User Certificate Wizard.
+   3. Click the **Object Selector** button next to the Create a new certificate for the following users text box, navigate to your **IT OU**, and then click to add IT users to the Selected Objects list box.
+   4. Click **OK**, and then click **Next** to display the Certificate Details window.
+   5. Enter **Email service** in the Certificate nickname text box, verify that the Standard creation method is selected, and then click **Next** to display the summary window. Record the signing CA, signature algorithm, and expiration date:
+   6. Click **Finish** to create the user certificates and display the Results window.
+   7. Click **Close** to return to the iManager main window, and exit iManager. Leave your system running for the next activity.

# Encryption Protocols

A number of encryption protocols can be used to secure data and passwords transmitted across networks. Most protocols can be configured to use symmetric or asymmetric cryptography, depending on security and performance needs. When exchanging keys isn't necessary, symmetric protocols require less processing overhead, so they are often used to encrypt data transmitted on private networks, and keys for each user can be stored in a directory service on the server.