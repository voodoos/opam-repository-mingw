---
layout: post
title:  "The repository will be discontinued as of August 2021"
date:   2021-02-26 14:30:00
---

Most packages that are still under active development now use
[dune](https://dune.build/), which, unlike oasis, ocamlbuild and other
solutions, offers good Windows support. A special repository for
Windows users is therefore becoming increasingly superfluous. In
addition, there is now [esy](https://esy.sh/) as an alternative, which
also supports Windows.

To ease the transition, I will create a special branch in the near
future, which will only contain the compiler packages of the old
Windows repository, and can be used in addition to the normal upstream
repository (`opam repo add ...`). However, this branch will not be
maintained.

[depext-cygwinports]({{site.baseurl}}/depext-cygwin/) unfortunately
became increasingly useless, as the main maintainer of the
corresponding packages [stopped his
activities](https://cygwin.com/pipermail/cygwin-apps/2020-March/039877.html)
more than a year ago. Hopefully someone else will develop a suitable
alternative; many packages rely on current third-party libraries like
gmp.
