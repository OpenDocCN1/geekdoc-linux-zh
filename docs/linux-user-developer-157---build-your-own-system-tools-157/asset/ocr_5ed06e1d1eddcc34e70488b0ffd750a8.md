![](bbox=[0.0, 0.15, 0.94, 0.55])

# 08 Sign in as an IAM user

In order to sign in with your user IAM credentials, you first need to navigate to the URL that you created in Step 6, and then enter your username from step 1 and your password from Step 3.

Once your ability to sign in has been confirmed, it is time to secure access to your (and every other users') account using multi-factor authentication.

# 09 Set up MFA authentication

Login credentials that consist of a username and a password can no longer be considered secure, not without MFA (multi-factor authentication). Brute-force attacks are rampant and frequently successful because encryption standards remain inadequate (or more accurately put: woefully outdated for the massive computational capabilities of the cloud). In order to combat the inadequacy of conventional login procedures, Amazon introduced multi-factor authentication (MFA) with the help of a token generator.

A token generator is a device – a mobile app or another piece of software – that is designed to provide an additional layer of security with the help of a one-time-use string of characters, the so-called token. A token can confirm the authorisation of its user to access AWS resources, but it requires prior registration with Amazon.

In order to register an MFA device, head over to the users section of the IAM service in the AWS Management Console, scroll down to the section Security Credentials>Sign-in Credentials and click on Manage MFA Device.

> " Login credentials that consist of a username and a password can no longer be considered secure "

# 10 Troubleshooting MFA

Should you be unable to sign in even though your MFA device appears to be working, the token generator may be out of sync with the AWS token verification system. All you need to do to restore access is synchronise them.

Should your MFA device stop working entirely for any reason (such as, most notably, wear and tear), you would not be able to sign in to the AWS Management Console of whatever account it was associated with. The device must be deactivated immediately and replaced as soon as possible. Obviously, you will also need to change your password just to be on the safe side – how to go about doing this is a whole different question. It depends whether the MFA was associated with the root account or with an IAM user.

If you’re experiencing problems related to an MFA device associated with an AWS root account, ask Amazon for help by submitting the form on this webpage: https://aws. amazon.com/forms/aws-mfa-support. You will need to provide a phone number and details regarding the issue.

IAM users should seek help from their AWS administrators (that’s probably you). Especially for mobile AWS administrators, an MFA token generator is highly advisable.