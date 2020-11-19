[![Build Status](https://travis-ci.org/raku-community-modules/perl6-LN.svg)](https://travis-ci.org/raku-community-modules/perl6-LN)

# NAME

LN - Get `$*ARGFILES` with line numbers via `$*LN`


# SYNOPSIS

```bash
perl  -wlnE   'say "$.:$_"; close ARGV if eof' foo bar # Perl
raku -MLN -ne 'say "$*LN:$_"'                  foo bar # Raku
```

```bash
$ echo -e "a\nb\nc" > foo
$ echo -e "d\ne"    > bar

$ raku -MLN -ne 'say "$*LN:$_"' foo bar
1:a
2:b
3:c
1:d
2:e

$ raku -ne 'use LN "no-reset"; say "$*LN:$_"' foo bar
1:a
2:b
3:c
4:d
5:e
```

# DESCRIPTION

Mixes in
[`IO::CatHandle::AutoLines`](https://github.com/raku-community-modules/perl6-IO-CatHandle-AutoLines) into
[`$*ARGFILES`](https://docs.perl6.org/language/variables#index-entry-%24%2AARGFILES)
which provides `.ln` method containing current line number of the current handle
(or total line number if `'no-reset'` option was passed to `use`). For ease
of access to that method `$*LN` dynamic variable containing its value is
available.

It's been known to fail with versions like Raku 2020.01. Use 2020.02
at least for this.

# EXPORTED TERMS

# `$*LN`

Contains same value as [`$*ARGFILES.ln`](https://github.com/raku-community-modules/perl6-IO-CatHandle-AutoLines#synopsis)
which is a method exported by
[`IO::CatHandle::AutoLines`](https://github.com/raku-community-modules/perl6-IO-CatHandle-AutoLines)
that gives the current line number of the handle.

By default, the line number will get reset on each new file in `$*ARGFILES`.
If you wish it to *not* reset, pass `"no-reset"` positional argument to the
`use` line:

```raku
use LN 'no-reset';
```

# EXPORTED TYPES

## role `IO::CatHandle::AutoLines`

Exports [`IO::CatHandle::AutoLines`](https://github.com/raku-community-modules/perl6-IO-CatHandle-AutoLines) role, for you to use, if needed.

-----

#### REPOSITORY

Fork this module on GitHub:
https://github.com/raku-community-modules/LN

#### BUGS

To report bugs or request features, please use
https://github.com/raku-community-modules/LN/issues

#### AUTHOR

Zoffix Znet (http://perl6.party/)

Currently maintained by the Raku community.

#### LICENSE

You can use and distribute this module under the terms of the
The Artistic License 2.0. See the `LICENSE` file included in this
distribution for complete details.

The `META6.json` file of this distribution may be distributed and modified
without restrictions or attribution.
