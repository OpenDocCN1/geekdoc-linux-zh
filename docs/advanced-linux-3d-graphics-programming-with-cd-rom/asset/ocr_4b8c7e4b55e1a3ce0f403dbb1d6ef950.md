```
")

sub get_texture {
  my $self = shift;
  my $tex_id = shift;

  return $self->{_textures}->{$tex_id};
}

sub add_texture {
  my $self = shift;
  my $tex_id = shift;
  my $tex = shift;

  $self->{_textures}->{$tex_id} = $tex;
}

sub get_all_texture_imagenums {
  my $self = shift;

  return $self->{_texture_imagenums};
}

sub get_texture_imagenum {
  my $self = shift;
  my $texi_id = shift;

  return $self->{_texture_imagenums}->{$texi_id};
}

sub set_texture_imagenum {
  my $self = shift;
  my $texi_id = shift;
  my $texi = shift;

  $self->{_texture_imagenums}->{$texi_id} = $texi;
}

sub link_portals {
  my $self = shift;
  my $Sector_key;
  my $Sector;
  my $Portal_key;
  my $Portal;
  my $OtherSector_key;
  my $OtherSector;
  my $OtherPortal_key;
  my $OtherPortal;
  for $Sector_key ( keys % ( $self->get_all_sectors() )) {
    my $unlinked_portal_num = 0;
    $Sector = $self->get_sector($Sector_key);

    print STDERR "Linking portals from Sector $Sector_key:";
    for $Portal_key ( keys % ( $Sector->get_all_portals())) {
      $Portal = $Sector->get_portal($Portal_key);
      if ($Portal->get_target_sector()) {
        print STDERR " Already assigned other side of portal $Portal_key:";
        print STDERR " (Sector ", $Portal->get_target_sector()->name(), ")":";
      } else {
```