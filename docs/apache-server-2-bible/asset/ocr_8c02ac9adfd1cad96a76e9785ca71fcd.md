# **Listing 18-2** (*Continued*)

```
#
my $data = shift;
my $secret = 'ID10t' ;  # Change this key if you like.

# We need the following line to tell Perl that
# we want to use the Digest::MD5 module.
use Digest::MD5;

# Create a new MD5 object
my $ctx = Digest::MD5->new;

# Add data
$ctx->add($data);

# Add secret key
$ctx->add($secret);

# Create a Base64 digest
my $digest = $ctx->b64digest;

# Return the digest
return $digest;
}

sub alert{
#
# Purpose: Display an alert dialog box
#          using Java Script.
#

# Get the message that we need to display
my $msg = shift;

# Create a java script that uses the alert()
# dialog box function to display a message
# and then return the browser to previous screen.
print <<JAVASCRIPT;

<script language="JavaScript">
alert("$msg");
history.back();
</script>

JAVASCRIPT
}

```