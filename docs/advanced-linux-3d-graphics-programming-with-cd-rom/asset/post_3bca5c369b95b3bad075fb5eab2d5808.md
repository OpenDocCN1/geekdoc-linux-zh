
## Chapter 6: Blender and World Editing

# portals

```perl
my $portal;
my $portal;

for my $portal_key ( keys %{$sector->get_all_portals()}) {
  $portal = $sector->get_portal($portal_key);
  print "PORTALPOLY ";
  print $portal->get_vertex_index_count()+1;
  for(my $i=0; $i<$portal->get_vertex_index_count(); $i++) {
    print " ", $portal->get_vertex_index($i);
  }
  print " ", $portal->get_target_selector()->name();
  print "\n";
}

# actors within this sector
my $actor_key;
for my $actor_key ( keys %{$sector->get_all_actors()}) {
  my $actor;
  $actor = $sector->get_actor($actor_key);
  if ($actor->is_camera()) {
    print "CAMERA ", $actor->name(), " ";
    print "no_plugin\n";
    print $actor->position(), " ";
    print $actor->orientation(), " ";
  } else {
    print "ACTOR ", $actor->name(), " ",
    print $actor->pluginfile(), " ",
    print $actor->position(), " ",
    print $actor->orientation(), " ",
    print $actor->meshfile(), " ",
    print $actor->texturefile(), " ",
    print $actor->uvfile(), " \n";
  }
  print "\n";
}
```

## errGen.pm

Module *errGen.pm* is a generator class that attempts to identify errors in a *World* object and prints diagnostics as output.

Member variable *world* stores the world object, which must have already been filled by a parser object.

Method *generate* searches for errors in the world structure in memory, prints diagnostics as output, and creates a series of Videoscape files which visually display the location of the errors. The error checking looks at the non-looped and non-linked portal lists of each sector, prints a text message indicating the existence of such portals for the sector, and creates a Videoscape file containing edges illustrating the boundaries of such invalid portals. The output files are in *nonlinked.obj* and *nonlooped.obj*; the asterisk indicates that several sequentially numbered Videoscape files may be created, one for each sector with invalid portals. By loading these Videoscape files into Blender, you can see the spatial location of any invalid portals. By storing the level meshes in one layer or scene and the invalid portals in another layer or scene, you can easily switch back and forth between the two to see exactly which sector meshes cause the invalid portals.

### Listing 6-10: errGen.pm

```perl
package errGen;
use strict;
use Portals::World;
use FileHandle;

my $debug = 0;
my $debug_str = "DEBUG----------------.";
my $portal_flag = hex '0x800000';

#####################################
## the object constructor ##
####################################
sub new {
    my $proto = shift;
    my $class = ref($proto) || $proto;
    my $self = {};
    $self->>{_world} = undef;
    bless ($self, $class);
    return $self;
}

#############################################
# methods to access per-object data ##
## #
# With args., they set the value. Without ##
# any, they only retrieve it/them. #
###############################################

sub get_world {
    my $self = shift;

    return $self->>{_world};
}

sub set_world {
    my $self = shift;
    my $w = shift;

    $self->>{_world}=$w;
}

sub generate {
    my $self = shift;

    my $aSector_key;
    my $aSector;

    my $unlinked_num;
    my $unlooped_num;

    # error report

    unlink <nonlinked.obj*>;
    unlink <nonlooped.obj*>;

    for my $aSector_key ( keys %{$self->get_world()->get_all_sectors()} ) {
      my $portal_key;
      my $aPortal;

      $aSector = $self->get_world()->get_sector($aSector_key);

      if ( keys %{$aSector->get_all_nonlooped_portals()} ) {
        print STDERR "Sector ", $aSector_key, " has nonlooped portals.\n";

        # vertices

        my $fname;

        if ($unlooped_num) {
          $fname = sprintf("%d_nonlooped.obj%d", $aSector_key, $unlooped_num++);
        } else {
          $fname = sprintf("%d_nonlooped.obj", $aSector_key);
          $unlooped_num = 1;
        }

        my $fh = FileHandle->new();
        $fh->open($fname, "w") or die "Couldn't open $fname: $!\n";
        print $fh "3DLI\n";

        my $num_vertices = 0;
        for my $v ( keys %{$aSector->get_all_vertices()} ) { $num_vertices++; }
        print $fh "$num_vertices\n";
        my $vertex_key;
        my $aVertex;
        for my $vertex_key ( sort keys %{$aSector->get_all_vertices()} ) {
          $aVertex = $aSector->get_vertex($vertex_key);
          # print "(" . $vertex_key . ")";
          print $fh " ", $aVertex->{x};
          print $fh " ", $aVertex->{z}; # reverse y and z to conv. lhs->rhs
          print $fh " ", $aVertex->{y};
          print $fh "\n";
        }

        for my $portal_key ( keys %{$aSector->get_all_nonlooped_portals()} ) {
          $aPortal = $aSector->get_nonlooped_portal($portal_key);

          # since the portal may have more than 4 sides, and since Blender
          # only handles polygons with max 4 sides, we can't write out the
          # portal as a single polygon; instead we write it out edge by edge
          my $edge;
          for my $edge ( $aPortal->get_edge_list() ) {
            print $fh "2 ", $edge->[0], " ", $edge->[1], "\n";
            print $fh " 0xFFFFFF\n";
          }
        }

        $fh->close();
      }

      if ( keys %{$aSector->get_all_nonlinked_portals()} ) {
        print STDERR "Sector ", $aSector_key, " has nonlinked portals.\n";

        # vertices

        my $fname;

        if ($unlinked_num) {
          $fname = sprintf("%d_nonlinked.obj%d", $aSector_key, $unlinked_num++);
        } else {
          $fname = sprintf("%d_nonlinked.obj", $aSector_key);
          $unlinked_num = 1;
        }

        my $fh = FileHandle->new();
        $fh->open($fname, "w") or die "Couldn't open $fname: $!\n";
        print $fh "3DLI\n";

        my $num_vertices = 0;
        for my $v ( keys %{$aSector->get_all_vertices()} ) { $num_vertices++; }
        print $fh "$num_vertices\n";
        my $vertex_key;
        my $aVertex;
        for my $vertex_key ( sort keys %{$aSector->get_all_vertices()} ) {
          $aVertex = $aSector->get_vertex($vertex_key);
          # print "(" , $vertex_key , ")";
          print $fh " " , $aVertex->{x}, " ";
          print $fh " " , $aVertex->{z}, " "; # reverse y and z to conv. lhs->rhs
          print $fh " " , $aVertex->{y}, "\n";
        }

        for my $portal_key ( keys %{$aSector->get_all_nonlinked_portals()} ) {
          $aPortal = $aSector->get_nonlinked_portal($portal_key);

          # since the portal may have more than 4 sides, and since Blender
          # only handles polygons with max 4 sides, we can't write out the
          # portal as a single polygon; instead we write it out edge by edge
          my $edge;
          for my $edge ( $aPortal->get_edge_list() ) {
            print $fh "2 " , $edge->[0], " " , $edge->[1] , "\n";
            print $fh " 0xffffff\n";
          }
        }

        $fh->close();
      }
    }
}
```

## Controlling Scripts

As is often the case with object-oriented systems, we have a number of components (classes), each of which represents a useful, coherent data abstraction in the problem domain. (Don't fall into the trap of thinking that a class does one thing well, because a class is a data abstraction, not a functional unit.) To bring the entire system together, we have a controlling script which creates the proper objects and sets them in motion. For our portalization system, this script is `vid2port.pl`.

### vid2port.pl

Controlling script `vid2port.pl` executes the portalization system by creating and invoking methods on the appropriate structural objects.

Invoke `vid2port.pl` with a command of the form:

```bash
perl $L3D/source/utils/portalize/vid2port.pl name.obj* > world.dat
```

Replace `name.obj` with the name prefix of the Videoscape file to which you exported your meshes. Include the asterisk on the command line; this causes the shell to pass all Videoscape files with matching names as parameters to the Perl script. As output, this creates file `world.dat`; diagnostic messages are also printed to the standard error stream during the portalization process.

The script begins by creating an instance of a Videoscape parser object. It then calls `parse` on the parser object, passing a list of all the Videoscape filenames as a parameter. The parser object creates in memory a world object corresponding to the Videoscape files. Next, `vid2port.pl` creates an error generator object, assigns the world object to the generator, and calls `generate`. This creates the `nonlooped.obj*` and `nonlinked.obj*` Videoscape files to help find invalid portals. Finally, `vid2port.pl` creates an `l3d` generator object, assigns the world object to this generator, and calls `generate`. This prints the final portal world file to the standard output stream, which we redirected on the command line into file `world.dat`.

### Listing 6-11: vid2port.pl

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

## Embedding Location, Orientation, Texture, Actor, and Other Information into Meshes

We now understand the basics of the portalization system: parsing Videoscape, scanning for holes, generating portals, linking portals, and creating the final world file as output. Now it's time to see how we can use the system to specify information on plug-in objects and textures. Doing so requires some fundamental enhancements to the system.

Notice that the entire portalization system so far has functioned without knowing which exported Videoscape file corresponded to which mesh in Blender. Up until now, this was
