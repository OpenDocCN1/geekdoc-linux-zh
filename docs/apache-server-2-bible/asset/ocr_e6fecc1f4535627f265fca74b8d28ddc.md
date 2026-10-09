If this happens frequently, you can use a CGI script to automatically redirect users to your home page or to an internal search engine interface. Simply modify the *DirectoryIndex* directive to be:

```
`DirectoryIndex index.html index.htm /cgi-bin/index.pl`
```

Now add a CGI script such as the one shown in Listing 18-1 in the *ScriptAlias*- specified directory.

# Listing 18-1: **index.pl**

```
#!/usr/bin/perl  # # Purpose: this script is used to redirect # users who enter a URL that points to # directories without index.html page. # use CGI qw(:standard);  # Set the automatically redirect URL my $AUTO_REDIRECT_URL = '/';  # Get the current URL path my $curDir = $ENV{REQUEST_URI};  # If the current URL path is not home page ( / ) then # redirect user to home page if ($curDir ne '/'){ print redirect($AUTO_REDIRECT_URL); # If the home page is also missing the index page, # we can't redirect back to home page (to avoid # recursive redirection), so display an error message. } else { print header; print "HOME PAGE NOT FOUND!"; }  exit 0;
```

This script runs after Apache fails to find the directory index files (*index.html* or *index.htm*). The script simply redirects a user whose URL points to a directory with no index file to the Web site’s home page.