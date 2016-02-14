---
layout: default
title: depext cygwin
---


[depext-cygwinports](https://github.com/fdopen/depext-cygwinports) is
a wrapper around `cygcheck` and cygwin's
[setup-x86.exe](https://cygwin.com/setup-x86.exe) \(or
[setup-x86_64.exe](https://cygwin.com/setup-x86_64.exe) \).

The installation of external libraries (like pcre, gtk2, or gmp) is
very convenient this way.  <br />

## Preparation

* Add `/usr/i686-w64-mingw32/sys-root/mingw/bin` or
  `/usr/x86_64-w64-mingw32/sys-root/mingw/bin` to your $PATH (in front
  of `/usr/bin`, not after it!)

* Install `depext-cygwinports` with:

{% highlight bash %}
opam install depext depext-cygwinports
{% endhighlight %}
<br />

## Usage

Now you can use `opam depext` as usual. The following command for
example will install
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
