+   5.2.4. --root <path>: Use <path> As an Alternate Root . . . . . . . . . . . . . . . . 74

+   5.2.5. -rcfile <rcfile>: Use <rcfile> As an Alternate rpmrc File . . . 75

+   5.2.6. --dbpath <path>: Use <path> to Find an RPM Database . . 75

# 5.3. A Few Handy Queries . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 75

+   5.3.1. Finding Config Files Based on a Program Name . . . . . . . . . . . . . 75

+   5.3.2. Learning More About an Uninstalled Package . . . . . . . . . . . . . . 76

+   5.3.3. Finding Documentation for a Specific Package . . . . . . . . . . . . . . 76

+   5.3.4. Finding Similar Packages . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 77

+   5.3.5. Finding Recently Installed Packages, Part I . . . . . . . . . . . . . . . . . 77

+   5.3.6. Finding Recently Installed Packages, Part II . . . . . . . . . . . . . . . . 77

+   5.3.7. Finding the Largest Installed Packages . . . . . . . . . . . . . . . . . . . . . . 78

# 6 Using RPM to Verify Installed Packages . . . . . . . . . . . . . . . . . . . . . . . . 79

+   6.1. rpm -v: What Does It Do? . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 80

+   6.1.1. What Does It Verify? . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 81

+   6.2. When Verification Fails: rpm -v Output . . . . . . . . . . . . . . . . . . . . . 83

+   6.2.1. Other Verification Failure Messages . . . . . . . . . . . . . . . . . . . . . . 84

+   6.3. Selecting What to Verify and How . . . . . . . . . . . . . . . . . . . . . . . . . . 85

+   6.3.1. The Package Label: Verify an Installed Package Against the RPM Database . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 85

+   6.3.2. -a: Verify All Installed Packages Against the RPM Database . 85

+   6.3.3. -f <file>: Verify the Package Owning <file> Against the RPM Database . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 86

+   6.3.4. -p <file>: Verify Against a Specific Package File . . . . . . . . . . . . . 86

+   6.3.5. -g <group>: Verify Packages Belonging to <group> . . . . . . . . . . 87

+   6.3.6. --nodesp: Do Not Check Dependencies Before Erasing Package . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 87

+   6.3.7. -noscripts: Do Not Execute Verification Script . . . . . . . . . . . . . 88

+   6.3.8. --nofiles: Do Not Verify File Attributes . . . . . . . . . . . . . . . . . . . 88

+   6.3.9. -v: Display Additional Information . . . . . . . . . . . . . . . . . . . . . . . . . 89

+   6.3.10. -vv: Display Debugging Information . . . . . . . . . . . . . . . . . . . . . 89

+   6.3.11. --dbpath <path>: Use <path> to Find an RPM Database . . . . . 90

+   6.3.12. --root <path>: Set Alternate Root to <path> . . . . . . . . . . . . . . . 90

+   6.3.13. -rcfile <rcfile>: Set Alternate rpmrc File to <rcfile> . . . . . . . 90

+   6.4. We’ve Lied to You . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 90

+   6.4.1. RPM Controls What Gets Verified . . . . . . . . . . . . . . . . . . . . . . . . 90

+   6.4.2. The Package Builder Can Also Control What Gets Verified . . . 91

# 7 Using RPM to Verify Package Files . . . . . . . . . . . . . . . . . . . . . . . . . . . . 93

+   7.1. rpm -K: What Does It Do? . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 94

+   7.1.1. Pretty Good Privacy: RPM’s Assistant . . . . . . . . . . . . . . . . . . . 94

+   7.2. Configuring PGP for U . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95

+   7.3. Using rpm -K . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95

+   7.3.1. -v: Display Additional Information . . . . . . . . . . . . . . . . . . . . . . . . . 96

+   7.3.2. When the Package Is Not Signed . . . . . . . . . . . . . . . . . . . . . . . . . . 97

+   7.3.3. When You Are Missing the Correct Public Key . . . . . . . . . . . . . . 97

+   7.3.4. When a Package Just Doesn’t Verify . . . . . . . . . . . . . . . . . . . . . . . . . 98

+   7.3.5. -nopgp: Do Not Verify Any PGP Signatures . . . . . . . . . . . . . . . . . . . 99