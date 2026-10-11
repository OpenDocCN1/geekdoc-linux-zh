# EXAMPLE 14.10 (CONTINUED)

```
```
4 sub shoot{ # Instance method for the director
my $self = shift;
print "$self->{Name} is shooting the movie $self->{Movie}.\n";
}
;

5 #-------------------File: Rifleman.pm
package Rifleman; # Class
sub init{
my $class = shift;
my ($name, $shooting_range) = @_;
my $rifleman={
"Name"=>$name,
"Range"=>$shooting_range,
};
return bless($rifleman, $class);
}

6 sub shoot{ # Instance method for the rifleman
my $self = shift;
print "$self->{Name} went to the $self->{Range} range to shoot
  target s.\n";
}
;

7 #-------------------File: user.plx
use BasketballPlayer
use Director;
use Rifleman;
use feature qw(say);

# Create instances of each class
8 $ballplayer=BasketballPlayer->new("Wilt Chamberlain",
"Boston Globe Trotters", 
"center");
9 $movie_director=Director->new( {"Name"=>"Steve McQueen",
"Movie"=>"12 Years A Slave",
"Type"=>"Historical Drama"}
);
10 $gunman=Rifleman->init("Lucas McCain", "North Fork Range");
11 say "The basketball player is a ", ref $ballplayer;
12 say "The director is a ", ref $movie_director;
13 say "The rifleman is a ", ref $gunman;
14 $ballplayer->shoot(); # polymorphism
15 $movie_director->shoot();
16 $gunman->shoot();
```

(Output)

```
11 The basketball player is a BasketballPlayer
12 The director is a Director
13 The rifleman is a Rifleman
14 Wilt Chamberlain was a center and shot baskets for the Boston Globe Trotters.
15 Steve McQueen is shooting the movie 12 Years A Slave.
16 Lucas McCain went to the North Fork Range range to shoot targets.
```
```