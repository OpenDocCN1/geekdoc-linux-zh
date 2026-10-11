# EXAMPLE 13.3 (CONTINUED)

```
```
  ARNING_BITS      =>  *main::ARNING_BITS
  re::             =>  *main::re::
  CORE::           =>  *main::CORE::
  DynaLoader::     =>  *main::DynaLoader::
  mro::            =>  *main::mro::
  stdout           =>  *main::stdout
                   =>  *main::
  stdin            =>  *main::stdin
  ARGV             =>  *main::ARGV
  INC              =>  *main::INC
  name             =>  *main::name
  ENV              =>  *main::ENV
  Regexp::         =>  *main::Regexp::
  UNIVERSAL::      =>  *main::UNIVERSAL::
  family           =>  *main::family
  _.perlio.c       =>  *main::_.perlio.c
  E_TRIX_MAXBUF    =>  *main::E_TRIX_MAXBUF
  main::           =>  *main::main::
  Carp::           =>  *main::Carp::
  _.perlmain.c     =>  *main::_.perlmain.c
  Perlio::        =>  *main::Perlio::
  0                =>  *main::0
  _.universal.c    =>  *main::_.universal.c
  BEGIN            =>  *main::BEGIN
                   =>  *main::
  @                =>  *main::@
  feature::        =>  *main::feature::
  STDOUT           =>  *main::STDOUT
  IO::             =>  *main::IO::
  val              =>  *main::val
                   =>  *main::
                   =>  *main::
  Exporter::       =>  *main::Exporter::
  STDERR           =>  *main::STDERR
  Internals::      =>  *main::Internals::
  $G               =>  *main::$G
  STDIN            =>  *main::STDIN
  warnings::       =>  *main::warnings::
```
```

# EXPLANATION

The lexical state variable is declared. It is not on the global symbol table. To see an example how state variables are used, see Chapter 11, “How do Subroutines Function?”

The lexical my variable is declared and is not on the symbol table.

Global our variables are declared. They are on the symbol table and available to other packages. They will not be flagged as global variables when the strict pragma is turned on.