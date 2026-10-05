# OffSec

Penetration Testing with Kali Linux

Figure 195: Disabling Windows Defender Automated Sample Submission

Having such a targeted scenario allows us to test AV evasion vectors without worrying about our sample being submitted for further analysis.

Since automatic sample submission allows Windows Defender to get our sample analyzed by its machine learning engines, we should only enable it once we are confident our bypasses will be effective and only if our target sample submission enabled.

> Since both Windows Defender cloud protection and automatic sample submission require internet connectivity, we should first verify that this is reflected in our target environment: some company policies mandate limited internet access to some production servers and as a consequence, some advanced AV features are inhibited.

Another rule of thumb should be when developing AV bypasses is to always prefer custom code. As we have learned at the beginning of this Module, AV signatures are extrapolated from the malware sample and thus, the more novel and diversified our code is, the fewer chances we have to incur any existing detection.

# 12.3.2 Evading AV with Thread Injection

Now that we have a general understanding of the detection techniques used in antivirus and the relative bypass methods, we can turn our focus to a practical example.

Finding a universal solution to bypass all antivirus products is difficult and time consuming, if not impossible. Considering time limitations during a typical penetration test, it is far more efficient to target the specific antivirus product deployed in the target network.

For the purposes of this Module, we will interact with Avira Free Security version 1.1.68.29553 on our Windows 11 client. Once we connect via RDP with the provided credentials, we'll notice that Avira is already installed and can be launched from the Desktop shortcut. Once started, we can navigate to the Security panel from the left menu and click on Protection Options: