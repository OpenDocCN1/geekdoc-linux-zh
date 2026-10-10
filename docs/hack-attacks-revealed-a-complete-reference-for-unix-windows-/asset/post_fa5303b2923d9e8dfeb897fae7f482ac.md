
## xcrack.pl

```perl
getwordlist();				# getting all words into array
getpasslist();				# getting login and password
print ("\n\tFinished - ", $wordlist, " - Against - ", $passlist);
#------------------------------------------------------------
sub getpasslist{
open (PWD, $passlist) or die (" No Good Name for password File ",
$passlist, "\n");
while (<PWD>)
{
	($fname, $encrypted, $uid, $gid, $cos, $home, $shell) = split (
/:/);
	if ($encrypted eq "**")		# Check if the account is Locked
	{
		print "Account :", $fname, "		-------
	Disabled\n";
		next;		# Skip to next read
	}
	if ($encrypted eq "x")		# Check if the account is Locked
	{
		print "Account :", $fname, "		-------
	Disabled\n";
		next;		# Skip to next read
	}
	if ($encrypted eq "")		# Check if the account has No Password
	{
		print "Account :", $fname, "		-------
	No Password\n";
		next;		# Skip to next read
	}

enccompare();				# Call on next Sub
	}
} close (PWD);	# closes the password file
}
#------------------------------------------------------------
sub getwordlist{
open (WRD, $wordlist) or die (" No Good Name for wordfile ", $wordlist,
"\n");
while (<WRD>)
{
	@tmp_array = split;			# Getting the entire contents of
	# our
	push @word_array, [@tmp_array]; # word file and stuffing it
	# in here
	}
close (WRD);	# closes the wordlist
}
#------------------------------------------------------------
sub enccompare{
for $password ( @word_array)
{
	$encword = crypt (@$password[0], $encrypted); # encrypt our
	# word
	# with the same salt
if ($encword eq $encrypted)                          # as the encrypted
	# password
		{
print "Account :" , $fname, "\t-----\t"aPassword:" ,
@$Password[0], "\n";
			last;		# Print the account name and password if broken
			# then break loop
		}
	}
###############################################################
sub usage { print "usage = perl xcrack.pl PASSWORDFILE WORDFILE\n";
	}
# End xcrack.pl	# simple usage if no #ARGV's
```

To run xcrack, use the following command:
`perl xcrack.pl PASSWORDFILE WORDFILE`

The latest Perl engine is available at www.Perl.com. This program must be executed with a word file or dictionary list (one is available on the CD bundled with this book). To create a password file with custom input, execute crypt.pl, as shown here:

## crypt.pl

```perl
# Usage "Perl crypt.pl username password uid gid cos home

# start crypt.pl
if ($#ARGV < 1) {
		usage();
		exit;
	}
	
$file = "password";				# just supplying variable with filename
$username = $ARGV[0];			# carries name
$password = $ARGV[1];			# carries unencrypted password
$uid = $ARGV[2];			# uid
$gid = $ARGV[3];			# gid
$cos = $ARGV[4];			# cos
$home = $ARGV[5];				# home dir
$shell = $ARGV[6];			# shell used
$encrypted = crypt ($password, "PH");		# encrypt's the password
open (PWD, ">>$file") or die ("Can't open Password File\n");	#opens file in append mode
		#writes the data and splits them up using :
print PWD $username, ":", $encrypted, ":", $uid,
":", $gid, ":", $cos, ":", $home, ":", $shell, "\n";
close (PWD);				#closes the file
print "Added ok";

sub usage{
print "\nUsage perl crypt.pl username password uid gid cos home she
ll\n";
}
# End crypt.pl
```

The last module in this Perl series is used for creating wordlists using random characters, shown here:

```perl
if ($#ARGV < 1) {
usage();		#If there are no arguments then print the usage
exit;
}

$word = $ARGV[0];
$many = $ARGV[1];\ srand(time);
			# an array of the random characters we want to produce
			# remove any you know are not in the password

@c=split( / */,
"ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789");

open (CONF, ">>$word") or die ("\nFile Error With Output File\n");
# we will repeat the following lines $many times i will be splitting
# down the @c array with caps in 1, symbols in 1, lowercase in 1 and
# numbers in 1.

for($i=0; $i <$many; $i +=1)
		{
print CONF	$c[int(rand(62))], $c[int(rand(62))], $c[int(rand(62
))]),
				$c[int(rand(62))], $c[int(rand(62))], $c[int(rand(62))]
				,
				$c[int(rand(62))], $c[int(rand(62))];
print CONF "\n";
		}

sub usage
		{
		print "\nusage = perl wordlist.pl OUTPUTFILE NumberOfWord
s \n";
		}

# In the next version I want to be able to give templates as an input
# and build all the combinations in between i.e. the password starts
# with "John" and there are 8 characters and none are numbers or
# uppercase so we can input  "john"1111 ..

# Below will produce words like bababa99 this was done and can be
# rearranged a bit as you need before the next version ........

# @c=split(/ */", "bcdefghjklmnpqrstvwxyz");
# @v=split(/ */", "aeiou");

# {
# print CONF $c[int(rand(21))], $v[int(rand(5))],
#       $c[int(rand(21))], $v[int(rand(5))],
#       $c[int(rand(21))], $v[int(rand(5))],
#       int(rand(10)), int(rand(10));
# print CONF "\n";
# }
```

## Password Cracking

Password cracking in Windows is commonly achieved using the revision of UnSecure (see Figure 8.7), a program hackers use to exploit flaws with current networking and Internet security. This program is able to manipulate possible password combinations to pinpoint the user’s password. Currently,

![](img/ba85bb40c695c02adae8cbd6666f2e0c_397_0.png)

### Figure 8.7 The UnSecure password cracker.

UnSecure can break into most Windows 9x, Windows NT, Mac, UNIX, and other OS servers, with or without a firewall. The software was designed to be used over an existing network connection, but it is able to work with a dial-up connection as well. On a Pentium 233, UnSecure will go through a 98,000 word dictionary in under five minutes when attacking locally.

UnSecure uses two password-cracking methods: a dictionary attack and a brute-force attack. The dictionary attack compares against a file containing all of the words and combinations you choose, separated by spaces, carriage returns, linefeeds, and so on. The brute-force attack allows you to try all possible password combinations using the characters you specify (a-z, A-Z, 0-9, and special).

![](img/ba85bb40c695c02adae8cbd6666f2e0c_398_0.png)

Password shadowing is a security measure whereby the encrypted password field of /etc/passwd is replaced with a special token; then the encrypted password is stored in a separate file. To defeat password shadowing, hackers write programs that use successive calls to getpwent() to forcefully obtain the password file.

## Remote Control

With the exponential growth of the Internet and advanced collaboration, there are many programs in worldwide distribution that can make the most threatening virus seem harmless. These programs are designed to allow a remote attacker the ability to control your network server or personal computer covertly. Armed with such daemons, attackers can collect passwords, access accounts (including email), modify documents, share hard drive volumes, record keystrokes, capture screen shots, and even listen to conversations on the computer's microphone.

Knowing this, it is imperative to consider the implications of hackers in control of your computer: They can place orders with your online accounts, read your personal email, send mail spam or bombs to others with your system, and even remotely view your screen. Some extremely dangerous flavors of these programs have the capability to wipe entire disk drives and even damage monitors. Reportedly, some victims are working on their system at the same time their computers are being remotely controlled for use in some crime. Assaults such as this make it very difficult for victims to prove their innocence, particularly if the hackers erase the evidence of their presence after committing the crime (with log bashing and techniques along those lines discussed earlier).

These programs are called remote-control daemons, and they are currently distributed in many ways: disguised as jokes, games, pictures, screen savers, holiday greetings, and useful utilities, to name a few. The three most widespread remote-control programs are Netbus, Back Orifice, and SubSeven, but there are many more. Chapter 4 has a complete listing of the most common mutations.

So far, antivirus/Trojan packages cannot possibly keep up with the different compilations of remote controllers. And, perhaps more alarming, is that it takes very little hacking expertise to distribute and operate these programs. Most of them include clients that provide detailed menus with GUIs. Recently, for example, hackers have been spreading a mutation of the popular remote-control daemon BackDoor-G, called BACK-AGN, as an attachment to email spam. In action, the malicious code typically has a spoofed, or illegitimate, return address; thus, the attachment may carry virtually any false identity. When a user clicks on it, the program executes, installs itself, and creates a gaping hole into the system. This is a Windows 9x Internet backdoor Trojan that gives virtually unlimited access to the system over the Internet.

More alarming still is that there are many flavors of programs like BackDoor-G floating around whose operation is almost undetectable by the user, though the files it installs in the Windows and Windows/System folders can be easily located on infected systems. With these two mutations, the first installed file, named BackDoor-G.ldr, is located in the Windows folder, and acts as a loader for the main Trojan server. The second, which is the kernel Trojan module itself, is named BackDoor-G.srv; it is also located in the Windows folder. This portion of the program receives and executes commands from the Internet. It contains a dynamic link library (DLL) file named WATCHING.DLL OR LM_DRK_33.DLL that the program copies into the Windows\System folder. The Trojan server then monitors the Internet for connections from the client software, identified as BackDoor-G.dll.
