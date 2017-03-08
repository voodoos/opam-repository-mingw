---
layout: default
title: depext cygwin
---


[depext-cygwinports](https://github.com/fdopen/depext-cygwinports)
provides all functions that are necessary in order to
support [opam-depext](https://github.com/ocaml/opam-depext) under
cygwin. The installation of external libraries (like pcre, gtk2, or
gmp) is very convenient this way.

`depext-cygwinports` will also install a wrapper for `pkg-config`
inside `$(opam config var bin)`. `pkg-config` is available as either
`i686-w64-mingw32-pkg-config` or `x86_64-w64-mingw32-pkg-config` under
cygwin and most build instructions will just look for `pkg-config`.

<br />

## Preparation

* Add `/usr/i686-w64-mingw32/sys-root/mingw/bin` or
  `/usr/x86_64-w64-mingw32/sys-root/mingw/bin` to your $PATH (in front
  of `/usr/bin`, not after it!). The cygwin maintainer use this
  convention to avoid name clashes. There is for example one
  `curl-config` script at `/usr/bin` (for cygwin's version of libcurl
  that is linked against `cygwin1.dll`), one in
  `/usr/x86_64-w64-mingw32/sys-root/mingw/bin` (64-bit native windows)
  and one in `/usr/i686-w64-mingw32/sys-root/mingw/bin`. The dlls at
  `/usr/x86_64-w64-mingw32/sys-root/mingw/bin` and
  `/usr/i686-w64-mingw32/sys-root/mingw/bin` usually also have
  identical names. Therefore you have to configure your PATH manually.
  (As an alternative you can use `eval $(ocaml-env cygwin)` instead of
  `eval $(opam config env)`,
  see [ocaml-env](/opam-repository-mingw/ocaml-env))

* Install `depext-cygwinports` with:

{% highlight bash %}
opam install depext depext-cygwinports
{% endhighlight %}
<br />

## Usage

Now you can use `opam depext` in the same way as under linux. 
The following command for example will install
[OCaml-Top](https://www.typerex.org/ocaml-top.html) including all
dependencies (gtk2, gtksourceview, etc.):

{% highlight bash %}
opam depext -i ocaml-top
{% endhighlight %}
<br />

## Caveats

* `depext-cygwinports` won't work in multiuser contexts - you need
  write access to your root directory of cygwin. If you use the
  graphical installer and start it as normal user, the installer will
  configure it correct for you. If you want to install additonal
  cygwin packages later or update your installation, start cygwin's
  setup with `cygwin-install gui` (`cygwin-install` is the wrapper
  installed by `depext-cygwinports`, it will call cygwin's setup with
  the right parameters for you). <br /> And by the way, you can create
  multiple, independent cygwin installations without any
  problems. Every user could create its own version, it would just
  waste disk space.
* `depext-cygwinports` is a misnomer at the moment. Yaakov Selkowitz
  recently moved all relevant packages from his
  [repository \('cygwinports'\)](http://cygwinports.org/) to the
  [main repository](http://permalink.gmane.org/gmane.os.cygwin/157342). The
  latest release of `depext-cygwinports` therefore does not longer
  install any packages from cygwinports. But this might change again
  in the future.
