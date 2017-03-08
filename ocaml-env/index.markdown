---
layout: default
title: ocaml-env
---

`opam.exe` is intended to be used from within cygwin.  If you want to
install additional libraries or upgrade existing packages, you should
do it inside a cygwin terminal (mintty/rxvt-unicode,...).

Once everything is installed, you are not longer depended on cygwin.
You can build your project from cmd.exe, powershell, your editor,
etc. However, you have to configure your build environment
properly. Your c compiler/linker (msvc or mingw-w64), cygwin (used
internally by mingw/flexlink), and ocaml/opam all require special
changes to the environment (`PATH`, `OCAMLLIB`,
`CAML_LD_LIBRARY_PATH`, `LIBPATH`, etc.).

`ocaml-env` is a little helper to combine these different steps into
one single call.

## Program Startup

Run a program with the proper environment settings, e.g:

{% highlight dos %}
:: run cmd.exe
ocaml-env exec -- cmd.exe
:: start utop from the 4.03.0-mingw64 switch
ocaml-env exec --switch=4.03.0-mingw64 -- utop.exe
:: run utop inside ConEmu / Notepad
ocaml-env-win --switch=4.04.0-msvc32 -- "C:\\Program Files\\ConEmu\\ConEmu.exe" -run utop.exe
ocaml-env-win -- "C:\\Program Files\\Notepad++\\notepad++.exe"
{% endhighlight %}

Note the difference between 'ocaml-env.exe exec -- ..' and
'ocaml-env-win.exe -- ..'.  Use the former to start console based
applications, the latter to start GUI applications.

## Msvc

`ocaml-env` is also useful, if you want to configure your environment
for the msvc toolchain from within cygwin. E.g if you intend to use
Visual Studio 2015 to compile OCaml:

{% highlight dos %}
eval $(ocaml-env cygwin --ms=vs2015 --no-opam --64)
opam switch 4.04+msvc64
{% endhighlight %}

The `--no-opam` switch is necessary, because `4.04+msvc64` is not yet
installed and we don't want to include opam environment settings from
another switch. `--64` is necessary in order to add the environment
variables for the right architecture. You can omit both once your
compiler is installed:

{% highlight bash %}
opam switch 4.04+msvc64
eval $(ocaml-env cygwin --ms=vs2015)
{% endhighlight %}

If you have only one Microsoft toolchain installed, you could in
theory now also omit `--ms=vs2015`. But I'm not sure, if the
auto-detection of program paths works very well. Open
an [issue](https://github.com/fdopen/opam-repository-mingw/issue), if
you encounter any problem.

## Mingw

If you use [depext-cygwinports](/opam-repository-mingw/depext-cygwin),
`ocaml-env` will add `/usr/i686-w64-mingw32/sys-root/mingw/bin` or
`/usr/x86_64-w64-mingw32/sys-root/mingw/bin` to your PATH, `eval
$(ocaml-env cygwin)` might be preferable to `eval $(opam config
env)`.

## Further Info

See `ocaml-env --help` for further details.
