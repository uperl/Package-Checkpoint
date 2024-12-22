# Package::Checkpoint ![linux](https://github.com/uperl/Package-Checkpoint/workflows/linux/badge.svg) ![windows](https://github.com/uperl/Package-Checkpoint/workflows/windows/badge.svg) ![macos](https://github.com/uperl/Package-Checkpoint/workflows/macos/badge.svg) ![msys2-mingw](https://github.com/uperl/Package-Checkpoint/workflows/msys2-mingw/badge.svg)

Checkpoint the scalar, array and hash values in a package for later restoration

# SYNOPSIS

```perl
package Foo::Bar {
  our $foo = 1;
  our @bar = (1,2,3);
  our %baz = ( a => 1 );
}

my $cp = Package::Checkpoint->new('Foo::Bar');

# modify Foo::Bar
$Foo::Bar::foo++;
push @Foo::Bar::bar, 4;
$Foo::Bar::baz{b} = 2;

$cp->restore;
# [$@%]Foo::Bar::{foo,bar,baz} are now back to their original values
```

# DESCRIPTION

This module saves the scalars, array and hash variables inside a package.  It doesn't
save anything else, including anything in any sub-packages.  The intent is if you are
storing app configuration in a package, you can checkpoint the config, make changes,
test those changes, and then restore the old values.  Probably a better pattern would
be to store the configuration in another type of object like a single hash variable,
but sometimes that may not be an option due to the age and complexity of an application.

# CONSTRUCTOR

## new

```perl
my $cp = Package::Checkpoint->new($package);
```

Creates a checkpoint for a package, saving all of the scalar, array and hash values
for later restoration.

# METHODS

## restore

```
$cp->restore;
```

Restores the scalar, array and hash values from the checkpoint.

# CAVEATS

Doesn't checkpoint or even consider a whole host of values that might be of interest,
like subroutines or file handles.

# SEE ALSO

- [Package::Stash](https://metacpan.org/pod/Package::Stash)
- [Package::Checkpoint::Guard](https://metacpan.org/pod/Package::Checkpoint::Guard)

# AUTHOR

Graham Ollis <plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2021-2024 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
