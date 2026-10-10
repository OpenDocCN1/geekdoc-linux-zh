
```perl
    print $aVertex->y(), "\n";
    print $aVertex->z(), "\n";
    }

# facets
my $Facet_key;
my $Facet;
for $facet_key ( keys %{$aSector->get_all_facets()}) {
    $aFacet = $aSector->get_facet($facet_key);

    if($aFacet->get_is_invisible()) { next }

    if ((length($aFacet->get_tex_id()) == 0)
    || ( ! exists $self->get_world()->get_all_textures->
        {$aFacet->get_tex_id()}))
    # could be falsely linked to a nonexistent texture id
    {
        print "GEOMPOLY ";
        print $aFacet->get_vertex_index_count(), "\n";
        for(my $i=0; $i<$aFacet->get_vertex_index_count(); $i++) {
            print " ", $aFacet->get_vertex_index($i);
        }
        print "\n";
    }
    else {
        my $aTex = $self->get_world()->get_texture
        (sprintf("%s",$aFacet->get_tex_id()));

        print "GEOMPOLY_TEX\n"; # ,"$aTex->get_tex_id(), "";
        print $aFacet->get_vertex_index_count(), "\n";
        for(my $i=0; $i<$aFacet->get_vertex_index_count(); $i++) {
            print " ", $aFacet->get_vertex_index($i);
        }
        # texture image number
        # print " ", $tex_name_to_num{$aTex->get_tex_id()};
        print " ", $self->get_world()->get_texture_imagenum
        ($aTex->get_image()), "\n";
        # texture orientation
        printf(" %f %f %f ",
        $aTex->get_origin()->x(),
        $aTex->get_origin()->y(),
        $aTex->get_origin()->z());
        printf(" %f %f %f ",
        $aTex->get_u_vec()->x(),
        $aTex->get_u_vec()->y(),
        $aTex->get_u_vec()->z());
        printf(" %f %f %f ",
        $aTex->get_v_vec()->x(),
        $aTex->get_v_vec()->y(),
        $aTex->get_v_vec()->z());
        print "\n";
    }
}
```

## 第6章：Blender 与世界编辑

### 传送门

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

# 该 sector 内的 actors
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

#### errGen.pm

模块`errGen.pm`是一个生成器类，旨在识别`World`（世界）对象中的错误，并打印诊断信息作为输出。

成员变量`world`存储世界对象，该对象必须已经由解析器对象填充完毕。

方法`generate`（生成）会在内存中的世界结构中搜索错误，打印诊断信息作为输出，并创建一系列`Videoscape`文件以可视化显示错误的位置。错误检查会查看每个`sector`（扇区）中未成环（non-looped）且未链接（non-linked）的传送门列表，打印文本消息以指示该`sector`存在此类传送门，并创建一个包含展示此类无效传送门边界的边的`Videoscape`文件。输出文件为`nonlinked.obj`和`nonlooped.obj`；星号表示可能会创建多个按顺序编号的`Videoscape`文件，每个拥有无效传送门的`sector`对应一个文件。通过将`Videoscape`文件加载到`Blender`中，您可以看到任何无效传送门的空间位置。通过将关卡网格（level meshes）存储在一个图层或场景中，将无效传送门存储在另一个图层或场景中，您可以轻松地在两者之间切换，以确切看到哪些`sector`网格导致了无效传送门。

##### 列表 6-10：errGen.pm

```perl
package errGen;
use strict;
use Portals::World;
use FileHandle;

my $debug = 0;
my $debug_str = "DEBUG----------------.";
my $portal_flag = hex '0x800000';

#####################################
## 对象构造函数 ##
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
# 访问每个对象数据的方法 ##
## #
# 带参数时，它们设置值。不带 ##
# 参数时，它们仅检索值。 #
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

    # 错误报告

    unlink <nonlinked.obj*>;
    unlink <nonlooped.obj*>;

    for my $aSector_key ( keys %{$self->get_world()->get_all_sectors()} ) {
      my $portal_key;
      my $aPortal;

      $aSector = $self->get_world()->get_sector($aSector_key);

      if ( keys %{$aSector->get_all_nonlooped_portals()} ) {
        print STDERR "Sector ", $aSector_key, " has nonlooped portals.\n";

        # 顶点

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

        # 顶点

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

#### 控制脚本

就像面向对象系统中的常见情况一样，我们有许多组件（类），每个组件都代表问题领域中一个有用且连贯的数据抽象。（不要陷入认为一个类只擅长做一件事的陷阱，因为类是数据抽象，而不是功能单元。）为了将整个系统整合起来，我们有一个控制脚本，它创建适当的对象并使其运行起来。对于我们的传送门化系统，这个脚本是`vid2port.pl`。

##### vid2port.pl
