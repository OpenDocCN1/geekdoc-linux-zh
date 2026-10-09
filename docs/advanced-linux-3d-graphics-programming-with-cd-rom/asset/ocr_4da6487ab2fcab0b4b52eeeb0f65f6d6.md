```
"$portal->add_vertex_index( $idx1 );
splice ( @{$selff->get_free_edges()}, $e_idx, 1 ); # remove current edge
print STDERR "\t\t\t\tStarting vertex $idx1.";",

my $first_idx = $idx1;

while ( ( $idx0 != $first_idx ) && !$error ) {
# keep going through vertex pairs until you hit the starting vertex again

# find daisy-chained edge

my $i;
my $done = undef;

for ( $i=0; $i<=$#{$selff->get_free_edges()} ) & & ($done; $i++) {
my $candidate_idx0 = $@{$selff->get_free_edges()[$i][1]}[1];
my $candidate_idx0 = ${@{$selff->get_free_edges()[$i][1]}[0];

if ( $candidate_idx1 == $idx0 ) {
$idx1 = $candidate_idx1;
$idx0 = $candidate_idx0;

# add current vertex to vertex list
$portal->add_vertex_index( $idx1 );
print STDERR "\t\t\t\t\tDaisy-chaining vertex $idx1.";

$e_idx = $i;
# remove current edge
splice ( @{$selff->get_free_edges()}, $e_idx, 1 );
$done = 1;
}

# the videoscape format appears to arbitrarily reverse
# the order of vertices in two-vector *faces* (probably since
# no normal vector orientation can be computed based on two
# vertices), so we have to also check for a matching edge in
# the other direction, i.e. edge 0-1 and 1-2 daisy chains to 1-3,
# but so does 0-1 and 3-1 (since 3-1 is the same as 1-3)
}
elif ( $candidate_idx0 == $idx0 ) {
$idx1 = $candidate_idx0;
$idx0 = $candidate_idx1;

# add current vertex to vertex list
$portal->add_vertex_index( $idx1 );
print STDERR "\t\t\t\t\t\t\tDaisy-chaining vertex $idx1.";

$e_idx = $i;
# Remove current edge
splice ( @{$selff->get_free_edges()}, $e_idx, 1 );
$done = 1;

}

}

if ( !$done ) {
print STDERR
"Ugh oh, free edges couldn't be joined into a loop; skipping...";
$self->delete_portal($portal);
$self->add_nonlooped_portal(sprintf("%d",$unlooped_portal_num++),
$portal);

$done = 1;
$error = 1;
```