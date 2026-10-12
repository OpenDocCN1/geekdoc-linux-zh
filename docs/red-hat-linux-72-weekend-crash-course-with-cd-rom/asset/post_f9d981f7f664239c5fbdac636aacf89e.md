
enclosing it in a pair of asterisks (*). Below that sentence, aspell lists possible corrections, numbering them sequentially from 1. In this case, the utility lists consensus — the right choice — as the first correction for consensus. The list also includes a few items labelled with a letter that mean specific actions such as ignore the misspelling or accept the misspelled word for the rest of the file.

At the end of the list of choices, aspell displays a question mark (?) prompt. You should press one of the numbers or letters from the list shown in aspell’s output to indicate what you want aspell to do. If you press a number, aspell uses the corresponding word to replace the misspelled one. Select i or I to ignore the misspelling; r to replace just this occurrence; R to replace all instances of this misspelling; a to add the word to your private dictionary; or x to exit aspell.

![](img/5fe8f856723cde0b366f73584b9e64b8_219_0.png)

To read the aspell manual, start the Web browser and select *File:: Open Page* and click the **Choose File** button from the **Open Page** dialog box. Go to the */usr/share/doc* directory and look for a directory name that begins with aspell; the complete name depends on the aspell version number. From the *man_html* subdirectory of that directory open the *1\_Introduction.html* file.

![](img/5fe8f856723cde0b366f73584b9e64b8_219_1.png)

## REVIEW

This session introduced you to office applications for Linux. You tried out a few common office tools — spreadsheets, calendars, calculators, and spelling checkers — that come with Red Hat Linux. You also learned about several commercially available office application suites for Linux — WordPerfect Office 2000 for Linux, Appliware Office, and StarOffice. These commercial applications are not part of Red Hat Linux, but you learned how to find out more about each product in case you need a Linux office suite for your home or business.

## QUIZ YOURSELF

- 1. What is the default file format and file extension of the Gnumeric spreadsheet? (See “Using the Gnumeric Spreadsheet.”)
- 2. How do you add an appointment to the GNOME Calendar? (See “GNOME calendar.”)
- 3. What choice of calculators do you have with Red Hat Linux? (See “Working with Calculators.”)
- 4. What utility do you use to check the spellings in a text file? (See “Utilizing the Spelling Checker.”)
- 5. What are some commercially available office applications for Linux? (See “Exploring Koffice Applications.”)

## SESSION

![](img/5fe8f856723cde0b366f73584b9e64b8_220_0.png)

## Using the Red Hat Network

- **Session Checklist**
  - Registering with the Red Hat Network
  - Running the Software Manager
  - Using the Update Agent

One of the biggest challenges of maintaining your Red Hat Linux system is keeping up with software updates that add new features, fix bugs, and, most importantly, address real and potential security risks. In this session, you’ll learn how to use the Red Hat Network to keep your Red Hat Linux system up-to-date and secure.

### Registering with the Red Hat Network

The Red Hat Network is a system management tool developed and administered by Red Hat for Red Hat Linux systems. Its only service, at this time, is the Software Manager. Software Manager consists of several services, including a software update subscription service, automatic Red Hat Package Manager (RPM) updates, and e-mail notification of bugs and security alerts.

Of course, the Red Hat Network is a fee-based service, not a free one. Red Hat Linux users who purchase versions 6.2 and 7.x are permitted a free subscription to Software Manager for one system. Additional subscriptions for other systems cost $19.95 per month, per system.

> For complete information about subscribing to the Red Hat Network, visit its Web site at [http://www.redhat.com/network/](s0103.jpg).

In order to use the Red Hat Network, you have to create a system profile and then register it with the Red Hat Network. *A system profile* is a database of software and hardware information that Red Hat Network uses to customize the updates and notifications you receive. Then, after a quick trip to the Red Hat Network to activate your Software Manager subscription, you can cage the Update Agent to obtain the latest updates for your system. To create the system profile and register with the Red Hat Network, follow this procedure:

- 1. Using the GNOME desktop, select **Main Menu** > **Programs** > **System** > **Red Hat Network**. This opens the Red Hat Registration screen, shown in Figure 20-1.

![](img/5fe8f856723cde0b366f73584b9e64b8_221_0.png)

*Figure 20-1 The Red Hat Network privacy policy*

- 2. After you read the privacy policy, click the **Next** button.
- 3. Fill out the form shown in Figure 20-2 to register your system, and then click the **Next** button.

> **Note**
>
> When selecting a password for the account you create, *do not use the password of any account you know.* Should your Red Hat Network account information be compromised somehow, using a different password will maintain the security of your system – using the same passwords gives the person with your Red Hat Network password access to your Red Hat Linux system.

- 4. If you wish, provide the additional information requested in the next dialog box. Doing so is optional, though. Click the **Next** button to continue.
- 5. The following dialog box allows you to name the system profile. The default name is your system’s host name. This dialog box also shows the hardware information that will be stored in the profile. Figure 20-3 shows the profile for a sample system. Click the **Next** button to continue.

![](img/5fe8f856723cde0b366f73584b9e64b8_222_0.png)

**Figure 20-2** Fill out the registration form to create an account for yourself.

![](img/5fe8f856723cde0b366f73584b9e64b8_222_1.png)

**Figure 20-3** The hardware profile and profile name are specific to your system.

- 6. After a short pause, the next screen shows a list of the packages installed on your system (see Figure 20-4). You should check the checkbox at the top of the dialog so that the Software Manager can store this information in the profile and use it to update packages installed on your system. Click the Next button to continue.

![](img/5fe8f856723cde0b366f73584b9e64b8_223_0.png)

**Figure 20-4** *The software profile enables the Software Manager to update RPMs.*

- 7. In the following dialog box, click **Next** to send the profile information to Red Hat and to register with the Red Hat Network (see Figure 20-5). You can click the **Cancel** button to cancel the registration.

![](img/5fe8f856723cde0b366f73584b9e64b8_223_1.png)

**Figure 20-5** *Send the system profile to the Red Hat Network to register.*

8. Depending on the speed of your network connection, you may see a progress dialog, as shown in Figure 20-6. When the process completes, you will see the screen shown in Figure 20-7. Click the **Finish** button to complete the registration process.

![](img/5fe8f856723cde0b366f73584b9e64b8_224_0.png)

*Figure 20-6 The progress dialog monitors the registration process.*

![](img/5fe8f856723cde0b366f73584b9e64b8_224_1.png)

*Figure 20-7 Clicking the Finish button completes the registration process.*

### Running the Software Manager

After registering with the Red Hat Network, follow this procedure to subscribe to the Software Manager:

- 1. Open the Red Hat Network home page at http://rhn.redhat.com/. Enter the user name and password you created when you registered with the Red Hat Network (see Step 3 in the previous section). Then click the **Login** button.
- 2. Click the **Entitlements** button under the Your RHN category on the left-hand side of the screen. The Entitlement Manager tells you how many entitlements you have left (see Figure 20-8).

![](img/5fe8f856723cde0b366f73584b9e64b8_225_0.png)

*Figure 20-8 The Red Hat Network Entitlement Manager*

- 3. If you have one or more Entitlements left, place a check mark in the checkbox next to the name of the system that you just registered.
- 4. Click the Update Entitlements button at the bottom of the page. The number of entitlements remaining will decrease, and your system is now ready to use the Red Hat Update Agent and Software Manager.
- 5. After updating your account, click the Log Out button in the upper left-hand corner of the page to log out of the Red Hat Network.

You are now ready to use the Update Agent, as described in the next section, to update your Red Hat Linux system's software packages.
