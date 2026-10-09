Videoscape files, since one Videoscape file represents one sector. The next code block of interest then begins at the line marked "link portals together." At this point in the code, we have already read in and parsed all facet definitions for all sectors, and have stored these in memory. So, we call `make_portals_from_holes` for each sector, then call `link_portals` for the world to link all portals amongst all sectors. At this point, the sector objects in memory now contain both the geometry polygons and the portals, which are linked to their connected sectors. The data is ready to be written to disk by one of the generator classes, which we cover next.

```
Listing 6-8: VidscParser.pm
```perl
package VidscParser;

# defines variable $Bin, which is dir from which script was invoked
use FindBin;
use lib "$FindBin::Bin";

use strict;
use Portals::World;
use Portals::Actor;
use FileHandle;

my $debug = 0;
my $debug_str = "DEBUG---------";
my $portal_flag = hex '0x800000';
my $lid_extraction_program = "$FindBin::Bin/../vidinfo/vidinfo";
my $attrib_filename_format_str = "attrib%d.dat";
my $attrib_dir = "";

##########################################
## The object constructor ##
##########################################
sub new {
    my $proto = shift;
    my $class = ref($proto) || $proto;
    my $self = {};
    $self->{_world} = World->new();
    bless ($self, $class);
    return $self;
}

##########################################
## methods to access per-object data ##
##
## With args, they set the value. Without ##
## any, they only retrieve it/them. ##
##########################################
sub get_world {
    my $self = shift;
    return $self->{_world};
}

sub parse {
    my $self = shift;
```
```