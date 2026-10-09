

sub get_free_edges { my $self = shift; return $self->{_free_edges}; }
sub make_portals_from_holes { my $self = shift; print(STDERR "Making portals from holes:"); $self->find_free_edges(); $self->merge_free_edges_into_portals(); }
sub add_nonlooped_portal { my $self = shift; my $portal_index = shift; my $portal = shift; $self->{_nonlooped_portals}{$portal_index} = $portal; }
sub get_nonlooped_portal { my $self = shift; my $portal_index = shift; return $self->{_nonlooped_portals}->{$portal_index}; }
sub get_all_nonlooped_portals { my $self = shift; return $self->{_nonlooped_portals}; }
sub add_nonlinked_portal { my $self = shift; my $portal_index = shift; my $portal = shift; $self->{_nonlinked_portals}{$portal_index} = $portal; }
sub get_all_nonlinked_portals { my $self = shift; return $self->{_nonlinked_portals}; }
sub get_nonlinked_portal { my $self = shift; my $portal_index = shift; return $self->{_nonlinked_portals}->{$portal_index}; }

################### PRIVATE ###################

sub find_free_edges {
    my $self = shift;
    my $saSector = shift; # Inferring missing argument based on context
    my $saFacet_key;
    my $saFacet;
    my $aoOtherFacet_key;
    my $aoOtherFacet;
    my @edge_list;

    print STDERR "Scanning for free edges. Sector ", $saSector->name(), "\n";
    for $saFacet_key ( keys %{ $saSector->get_all_facets() } ) {
        $saFacet = $saSector->get_facet($saFacet_key);
        print STDERR " facet ", $saFacet_key, " ";
        @edge_list = $saFacet->get_edge_list();
        for ( my $i=0; $i < @edge_list; $i++ ) {
            my $edge_taken = undef;
            for $aoOtherFacet_key ( keys %{ $saSector->get_all_facets() } ) {
                if ($aoOtherFacet_key != $saFacet_key) { # for all OTHER facets
                    $aoOtherFacet = $saSector->get_facet($aoOtherFacet_key);
                    if ($aoOtherFacet->contains_e_edge($edge_list[$i][0], $edge_list[$i][1])) {
                        $edge_taken = 1;
                    }
                }
            }
            if ( !$edge_taken ) {
                print STDERR " FREE EDGE ", $edge_list[$i][0], ",", $edge_list[$i][1], "\n";
                push @{$self->get_free_edges()}, $edge_list[$i] ;
            }
        }
    }

    print STDERR "\n Summary of found free edges:\n";
    for ( my $i=0; $i < @{$self->get_free_edges()}; $i++ ) {
        print STDERR " ";
        print STDERR $self->get_free_edges()[$i][0], " ";
        print STDERR $self->get_free_edges()[$i][1], "\n";
    }
}

sub _merge_free_edges_into_portals {
    my $self = shift;
    my @portal;

    # note that we must link the edges from pt1 to pt0 instead of pt0 to pt1
    # because we must reverse the orientation of the edges to make the portal
    # normal point the same direction as the neighboring facets' normals.

    my $portal_num = 0;
    my $unlooped_portal_num = 0;
    while ( ($#{$self->get_free_edges()} >= 0) ) {

        my $error = undef;
        print STDERR " Creating new portal:\n";
        $portal = Portal->new($self);
        $self->add_portal(sprintf("%d", $portal_num), $portal);

        my $e_idx = 0;
        my $idx1 = @{$self->get_free_edges()}[$e_idx][1];
        my $idx0 = @{$self->get_free_edges()}[$e_idx][0];

        # add current vertex to vertex list
        $portal->add_vertex_index( $idx1 );
        splice ( @{$self->get_free_edges()}, $e_idx, 1 ); # remove current edge
        print STDERR "\t\t\t\tStarting vertex $idx1.";

        my $first_idx = $idx1;

        while ( ( $idx0 != $first_idx ) && !$error ) {
            # keep going through vertex pairs until you hit the starting vertex again

            # find daisy-chained edge
            my $i;
            my $done = undef;

            for ( $i=0; $i <= $#{$self->get_free_edges()} && !$done; $i++ ) {
                my $candidate_idx1 = @{$self->get_free_edges()}[$i][1];
                my $candidate_idx0 = @{$self->get_free_edges()}[$i][0];

                if ( $candidate_idx1 == $idx0 ) {
                    $idx1 = $candidate_idx1;
                    $idx0 = $candidate_idx0;

                    # add current vertex to vertex list
                    $portal->add_vertex_index( $idx1 );
                    print STDERR "\t\t\t\t\tDaisy-chaining vertex $idx1.";

                    $e_idx = $i;
                    # remove current edge
                    splice ( @{$self->get_free_edges()}, $e_idx, 1 );
                    $done = 1;
                }
                # the videoscape format appears to arbitrarily reverse
                # the order of vertices in two-vector *faces* (probably since
                # no normal vector orientation can be computed based on two
                # vertices), so we have to also check for a matching edge in
                # the other direction, i.e. edge 0-1 and 1-2 daisy chains to 1-3,
                # but so does 0-1 and 3-1 (since 3-1 is the same as 1-3)
                elsif ( $candidate_idx0 == $idx0 ) {
                    $idx1 = $candidate_idx0;
                    $idx0 = $candidate_idx1;

                    # add current vertex to vertex list
                    $portal->add_vertex_index( $idx1 );
                    print STDERR "\t\t\t\t\t\t\tDaisy-chaining vertex $idx1.";

                    $e_idx = $i;
                    # Remove current edge
                    splice ( @{$self->get_free_edges()}, $e_idx, 1 );
                    $done = 1;
                }
            }

            if ( !$done ) {
                print STDERR "Ugh oh, free edges couldn't be joined into a loop; skipping...";
                $self->delete_portal($portal);
                $self->add_nonlooped_portal(sprintf("%d", $unlooped_portal_num++), $portal);
                $done = 1;
                $error = 1;
            }
        }
        if (! $error) {
            print STDERR " Portal complete.\n";
            $portal_num++;
        }
    }
    return 1; # so the require or use succeeds
}

## Actor.pm

模块 `Actor.pm` 代表一个插件对象，或称为演员（actor）。在本章稍后部分，我们将学习如何在 Blender 中指定演员。

成员变量 `_name` 是一个用于唯一标识该演员的字符串。

成员变量 `_parent` 是此演员最初所在的扇区（sector）对象；成员变量 `_parent_name` 是该扇区对象的名称。

成员变量 `_orientation` 是一个包含对象旋转矩阵九个元素的字符串。一种更灵活的方法是将旋转矩阵存储为数组，其中每个元素都可单独访问，但在这种情况下，我们实际上并不使用旋转矩阵；我们只是从网格中读取它，并将其重写到世界文件中。这就是为什么方向（orientation）被存储为一个简单的字符串。

成员变量 `_position` 是一个包含对象位置坐标的字符串。与方向（orientation）一样，使用字符串存储格式是因为我们不进行任何位置操作。

成员变量 `_is_camera` 反映当前正在考虑的插件对象是否是场景中的主摄像机。根据第 5 章中的世界文件格式，摄像机通过世界文件中的 CAMERA 行指定，而其他插件对象则通过 ACTOR 行指定；因此，我们需要区分这两者。

成员变量 `_meshfile` 是包含此插件对象几何信息的 Videoscape 文件的名称。正如我们之前提到的以及稍后更详细看到的，我们在 Blender 中使用简单的立方体作为插件对象的占位符；实际的插件几何形状由这个单独的网格文件定义。

成员变量 `_uvfile` 是包含网格纹理坐标的文件名称。

成员变量 `_texturefile` 是包含网格纹理图像的文件名称。

成员变量 `_pluginfile` 是控制此插件对象行为的动态库文件的名称。

### 列表 6-6：Actor.pm

```perl
package Actor;
use strict;
use Portals::Facet;
use Portals::Portal;
use Portals::Vertex;

#########################
## the object constructor ##
#####################################################
sub new {
  my $proto = shift;
  my $class = ref($proto) || $proto;
  my $self = {};
  $self->{_name} = undef;
  $self->{_parent} = undef;
  $self->{_parent_name} = undef;
  $self->{_orientation} = undef;
  $self->{_position} = undef;
  $self->{_is_camera} = undef;
  $self->{_meshfile} = undef;
  $self->{_uvfile} = undef;
  $self->{_texturefile} = undef;
  $self->{_pluginfile} = undef;

  bless ($self, $class);
  return $self;
}
#####################################################
## methods to access per-object data ##
## With args, they set the value. Without ##
## any, they only retrieve it/them. ##
#####################################################

sub name {
  my $self = shift;
  if (@_) {$self->{_name} = shift}
  return $self->{_name};
}

sub parent_name {
  my $self = shift;
  if (@_) {$self->{_parent_name} = shift}
  return $self->{_parent_name};
}

sub parent {
  my $self = shift;
  if (@_) {$self->{_parent} = shift}
  return $self->{_parent};
}

sub is_camera {
  my $self = shift;
  if (@_) {$self->{_is_camera} = shift}
  return $self->{_is_camera};
}

sub meshfile {
  my $self = shift;
  if (@_) {$self->{_meshfile} = shift}
```

