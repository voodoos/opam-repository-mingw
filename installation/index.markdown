---
layout: default
title: Installation
---

There are two ways to setup this opam repository:

## Graphical Installer

You can try the graphical installer:

* [32-bit](https://dl.dropboxusercontent.com/s/2y1hkzl7l8kedcn/OCaml32.exe)
  (updated 20. Feb 2016)
* [64-bit](https://dl.dropboxusercontent.com/s/d41lodwfm3cku7n/OCaml64.exe)
  (updated 20. Feb 2016)

The installer will first create a customized cygwin environment and
then set up opam and OCaml inside this environment. The setup should
be easy and fast this way. However, the installer won't allow you to
set custom options: proxy configuration, select the initial OCaml
version to install, etc. The 32-bit version will install a 32-bit
version of cygwin and then download a 32-bit version of OCaml; the
64-bit version will download 64-bit versions of both toolchains.

## Manual Installation

* Download links:
  * [32-bit](https://dl.dropboxusercontent.com/s/eo4igttab8ipyle/opam32.tar.xz)
    (updated 20. Feb 2016)
  * [64-bit](https://dl.dropboxusercontent.com/s/b2q2vjau7if1c1b/opam64.tar.xz)
    (updated 20. Feb 2016)

* Install [cygwin](https://cygwin.com/) and install the following
  additional packages through cywin's setup utility: rsync, patch,
  diffutils, curl, make, unzip, git, m4, perl - and of course
  mingw64-i686-gcc-core or mingw64-x86_64-gcc-core.

* If your logon name contains whitespace characters (e.g. 'Firstname
  Lastname') or any other character that would require quoting inside
  a unix shell or cmd.exe, follow the instructions
  [there](https://www.cygwin.com/faq.html#faq.setup.name-with-space).
  The name of your home directory should only contain alphanumeric
  ascii letters, no whitespaces (both, the windows version
  `C:\cygwin\home\user` and the posix version `/home/user`).

* Download one of the archives listed above. The archives contain
  native versions of opam, flexdll and aspcud. They are all not linked
  against cygwin1.dll, so you can use them both with either the 32-bit
  or 64-bit version of cygwin. Then proceed inside a cygwin shell:

{% highlight bash %}
tar -xf 'opam32.tar.xz' # or tar -xf 'opam64.tar.xz'
bash opam32/install.sh  # --prefix /usr/foo, the default prefix is /usr/local
opam init mingw 'https://github.com/fdopen/opam-repository-mingw.git' --comp 4.02.3+mingw32c --switch 4.02.3+mingw32c
# or, if you prefer the 64-bit version
opam init mingw 'https://github.com/fdopen/opam-repository-mingw.git' --comp 4.02.3+mingw64c --switch 4.02.3+mingw64c
eval $(opam config env)
{% endhighlight %}

The above commands will download and install precompiled versions of
OCaml. You can also compile it from source: 

{% highlight bash %}
opam init mingw 'https://github.com/fdopen/opam-repository-mingw.git' --comp 4.02.3+mingw32 --switch 4.02.3+mingw32
# or
opam init mingw 'https://github.com/fdopen/opam-repository-mingw.git' --comp 4.02.3+mingw64 --switch 4.02.3+mingw64
{% endhighlight %}

There are also mingw-versions for the obsolete
[4.01.0 version of OCaml available](https://github.com/fdopen/opam-repository-mingw/tree/master/compilers/4.01.0).

## Next Step

Install `depext` and [depext-cygwinports](/depext-cygwin), if you want
to use libraries like [pcre](https://github.com/mmottl/pcre-ocaml) or
[lablgtk](http://lablgtk.forge.ocamlcore.org/).
