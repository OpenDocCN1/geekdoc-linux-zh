
### 示例 13.8（续）

```
7  our $CarpLevel = 0;       our $MaxArgLen = 64;  # How much of each argument to print. 0 = all.

8  our $MaxArgNums = 8;      # How many arguments to print. 0 = all.

9

10

11 our require Exporter;

12 our $ISA = ('Exporter');

13 our @EXPORT = qw(confess croak carp);

14 our @EXPORT_OK = qw(cluck verbose longmess shortmess);

15 our @EXPORT_FAIL = qw(verbose);   # hook to enable verbose mode
```

```
# The members of %Internal are packages that are internal to perl.

# Carp will not report errors from within those packages if it

can. The members of %CarpInternal are internal to Perl's warning

system. Carp will not report errors from within these packages

# either, and will not report calls to *() these packages for carp and

# croak. They replace $CarpLevel, which is deprecated. The

# $max(EvalLen|Arg|Len|Nums)) variables are used to specify how the eval

# text and function arguments should be formatted when printed.

our %CarpInternal;

our %Internal;

# disable these by default, so they can live w/o require Carp

<continues here>

# if the caller specifies verbose usage ("perl -MCarp=verbose script.pl")

# then the following method will be called by the Exporter which knows

# to do this thanks to @EXPORT_FAIL, above. $_[1] will contain the word

# 'verbose'.

sub export_fail { shift; $Verbose = shift if $_[0] eq 'verbose'; @_ }

sub _cgc {

    no strict 'refs';

    return ${"CORE::GLOBAL::caller"} if defined

           ${"CORE::GLOBAL::caller"};

    return;

}

sub longmess {

    # Icky backward compatibility wrapper. :-(

    #

    # The story is that the original implementation hard-coded the

    # number of call levels to go back, so calls to longmess were off

    # by one. Other code began calling longmess and expecting this

    # behaviour, so the replacement has to emulate that behaviour.

    my $cgc = _cgc();

    my $call_pack = $cgc ? $cgc->(1) : caller();

    if ( %Internal{$call_pack} or %CarpInternal{$call_pack})  {

        return longmess_heavy(@_);

    }

    else {

        local $CarpLevel = $CarpLevel + 1;

        return longmess_heavy(@_);

    }

}

our @CARP_NOT;

sub shortmess {

    my $cgc = _cgc();

    # Icky backward compatibility wrapper. :-{

    local @CARP_NOT = $cgc ? $cgc->() : caller();

    shortmess_heavy(@_);

}

    sub croak   { die  shortmess @_  }

    sub confess { die  longmess  @_  }

    sub carp    { warn shortmess @_  }

    sub click   { warn  longmess @_  }

< Continues here >
```
