Invoke vid2port.pl with a command of the form
perl $L3D/source/utils/portalize/vid2port.pl name.obj* > world.dat

Replace name.obj with the name prefix of the Videoscape file to which you exported your meshes. Include the asterisk on the command line; this causes the shell to pass all Videoscape files with matching names as parameters to the Perl script. As output, this creates file world.dat; diagnostic messages are also printed to the standard error stream during the portalization process.

The script begins by creating an instance of a Videoscape parser object. It then calls parse on the parser object, passing a list of all the Videoscape filenames as a parameter. The parser object creates in memory a world object corresponding to the Videoscape files. Next, vid2port.pl creates an error generator object, assigns the world object to the generator, and calls generate. This creates the nonlooped.obj* and nonlinked.obj* Videoscape files to help find invalid portals. Finally, vid2port.pl creates an l3d generator object, assigns the world object to this generator, and calls generate. This prints the final portal world file to the standard output stream, which we redirected on the command line into file world.dat.

# Listing 6-11: vid2port.pl

```
```perl
#!/usr/bin/perl
use FindBin;
use lib "${FindBin}::Bin";
use Portals::VisdscParser;
use Portals::l3dGen;
use Portals::errGen;
use strict;

my $parser = VisdscParser->new();
$parser->parse(<ARGV>);

my $g = errGen->new();
$g->set_world($parser->get_world());
$g->generate();

my $g = l3dGen->new();
$g->set_world($parser->get_world());
$g->generate();
```
```

# Embedding Location, Orientation, Texture, Actor, and Other Information into Meshes

We now understand the basics of the portalization system: parsing Videoscape, scanning for holes, generating portals, linking portals, and creating the final world file as output. Now it's time to see how we can use the system to specify information on plug-in objects and textures. Doing so requires some fundamental enhancements to the system.

Notice that the entire portalization system so far has functioned without knowing which exported Videoscape file corresponded to which mesh in Blender. Up until now, this was