# You are being watched

Prevent apps and services from keeping tabs on you.

Many tasks that were once performed exclusively on PCs have now branched out to phones. They can double up as media players, recorders, gaming devices, GPS navigation devices and more. To enjoy all these conveniences you need apps. Unfortunately, apps are the weakest link between your private data and the world. Many access your personal data to 'enhance their experience.' But you must trust that apps will only use this data in a desirable way. Unfortunately, not every app clearly states how they use your it and you have no way of knowing if you're safe.

Then there are the free web services. Web companies like Google, Twitter, Facebook and others provide you with a free service in return for information about you. This information is then used to target ads. Some consider this fair trade but privacy campaigners are becoming increasingly concerned.

A critical component of your Android smartphone is the permissions system. When you install an app, it notifies you of what it would like to gain access to. You can then install the app, or not. Unfortunately, this system puts a lot of responsibility on the users to know whether these access requests are appropriate. According to research reports (source: http://bit.ly/1bRbsV) many apps request excessive permissions.

There are multiple ways of visualising app permissions. BitDefender's free Clueless app helps you identify what an app is doing, and what it should be doing. Once installed Clueless will scan your apps and categorise them as High Risk, Moderate Risk, and Low Risk. You can then browse each list and click on an app to find out the feature it can access. You should uninstall any High Risk apps as they might be pinching your passwords or reading emails.

Then there's Malwarebytes' Anti-Malware mobile app which also includes a Privacy Manager. It scans apps and divides them into categories based on the phone feature they have access to, such as Access Calendar and Access Storage. The app will come in handy when, for example, you wish to view all the apps that can read personal information such as your contact list and your web history.

> “Sharing images reveals a lot of information thanks to the EXIF data attached…”

is that once you disable a particular feature, say, access to contacts, XPrivacy will shield the real data and instead feed a list of bogus contacts to any app that requests them.

In addition to preventing the apps from leaking info, you should also minimise the personal data you put out there, even when sharing something as innocuous as images. John McAfee, who was evading authorities, was ousted in Guatemala thanks to a photo.

Sharing images taken from your smartphone reveal a lot of information about you thanks to the EXIF data attached to them, so if you take an image with a GPS-enabled camera or a smartphone, it can reveal your location, the time it was taken as well as the unique ID of the device.

To strip EXIF information from pictures before sharing them you can use the Instant EXIF Remover app. The app doesn't have an interface. Once installed it'll be available as an option in the 'Share' action. When selected, the app will intercept any images you wish to share and delete all EXIF data, before passing them on to the email client or any other sharing app. Also, before you upload files to a cloud sharing service like Dropbox or Google Drive, it's a good idea to encrypt them. You can do this easily on a Linux box with EncFS.

# Control permissions

Once you've identified a privacy-intruding app you can remove it. Google recently let slip a privacy functionality in Android 4.3 that users could unlock with the Aps Ops Launcher tool. With this feature you could selectively turn off privacy-related permissions. For example, you could install the Shazam music recognition app but turn off its ability to track your location. However, Google removed the feature in the following update, much to the chagrin of the EFF. When asked, Google said the feature was experimental and was released by accident.

If you have a rooted Android device you can still get the feature as a module for the Xposed framework. Users of rooted devices can also use the XPrivacy module for Xposed. With XPrivacy you can control specific permissions for all installed apps. The best bit

![](bbox=[0.07, 0.68, 0.32, 0.95])

EncFS is available in the repositories of popular distros like Fedora and Ubuntu. The tool requires you to create two directories – one that houses your unencrypted content and the other with the encrypted version. The way the tool works is that you interact with the files in the unencrypted folders and they are encrypted on-the-fly in the encrypted folder. To use EncFS with a cloud sharing service like Dropbox, just make sure you keep the encrypted folder inside the Dropbox folder. This will automatically sync any changes to the encrypted folder to Dropbox! After installing EncFS, create the two folders with EncFS ~/ Dropbox/encrypted ~/Private. The tool will ask you questions and create the folders. Any files in the Private directory will now be synced.

# Three degrees of separation

You don't need to be talking to a terror suspect to get the NSA interested in your personal communications. The agency is allowed to travel 'three hops' from its target. So they can monitor the communication of people who talk to people who talk to people who talk to you. This three degrees of separation allows NSA to virtually monitor everyone.

Mastering the learning curve of XPrivacy will go a long way in protecting your privacy.

![](bbox=[0.82, 0.12, 0.95, 0.27])