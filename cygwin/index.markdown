---
layout: default
title: Cygwin Tips & Tricks
---

Some random hints ...

## Symlinks

Cygwin support two kinds of symlinks: emulated symlinks and native
windows symlinks. The advantage of emulated symlinks is that they will
work on all file systems and with all windows versions. And every user
can create them. Therefore, these kinds of symlinks are created by
default. The disadvantage is that they are only understood by cygwin
based tools, not by native windows programs like the OCaml compiler.
(ocambuild behaves particular strange. ocamlbuild will under certain
conditions create symlinks with `ln`, but can't deal with them later.)

If you have the necessary rights, you can instruct cygwin to always
create native windows symlinks instead by setting a special
environment variable (`CYGWIN=winsymlinks:native`). You can circumvent
some problems this way.


## Bind mounts

Cygwin supports
["bind mounts"](https://cygwin.com/ml/cygwin-developers/2010-08/msg00000.html),
e.g:

{% highlight bash %}
mkdir ~/Downloads
mount -o bind /cygdrive/c/Users/MYUSERNAME/Downloads ~/Downloads
# Your Windows Download folder is now accessible via ~/Downloads :)
ls ~/Downloads
{% endhighlight %}

While this is a nice feature, you should use it very carefully, if at
all. When you use opam/OCaml from within cygwin, you frequently switch
between native Windows programs (the OCaml compiler, ocamlfind,
ocamlbuild) and cygwin tools (shell, git, c compiler). Only the latter
can understand bind mounts.

If you are at `~/Downloads` under cygwin, windows programs behave as if
they were at `C:/Users/MYUSERNAME/Download`; the outputs of `cmd.exe
/c dir ..` and `ls -l ..` will differ. Which location is meant by
`../foo`?


## Environment

Check your environment inside a cygwin terminal (`$ env`). And then
configure your `~/.bashrc` to remove anything from the environment
that you don't really need inside cygwin. Remove especially
unnecessary paths from `$PATH`. If your $PATH list is very long or
contains network paths, this will have a negative performance
impact. And of course, it can cause confusion for you or your scripts,
if there is something in your $PATH which is named like a Unix-tool,
but was installed long time ago by a dubious Windows-related
installer.


## Terminal emulators

There are two kinds of terminal emulators:

1. Cygwin terminals, like mintty or rxvt-unicode.
2. "Native" windows terminals, like
   [ConEmu](https://conemu.github.io/) or
   [ConsoleZ](https://github.com/cbucher/console).

You can configure the latter to start with cygwin's bash (or zsh)
instead of cmd.exe or powershell. Use whatever you like. However, some
tools like `utop` will only work under "real" terminals, not the faked
ones that are shipped by cygwin.

Both kinds of terminal emulators can be greatly enhanced, if you
modify your `.bashrc` or `.zshrc` \(`rxvt-unicode` can be configured
by `~/.Xdefaults` - as under linux\). The default configurations are
very minimalistic.


## Emacs

Again, you have several choices:

* [the native windows version](https://ftp.gnu.org/gnu/emacs/windows/)
* cygwin's emacs inside mintty/rxvt-unicode
* cygwin's emacs with a X11 interface (`emacs-X11` inside cygwin's
  `setup_*.exe` )
* cygwin's emacs with a native windows gui (`emacs-w32`)

The problem with cywin's emacs is, that this version can't deal with
windows paths (`C:\foo\bar`); and the native version can't deal with
cygwin's path conventions (`/home/user/file`,
`/cygdrive/c/foo/bar`). Windows paths are emitted by the OCaml
compiler, cygwin paths by the mingw-w64 compiler :)

Whichever version you choose, you have to teach emacs about foreign
paths, either with
[cygwin-mount.el](https://www.emacswiki.org/emacs/cygwin-mount.el) or
with
[windows-path.el](https://www.emacswiki.org/emacs/windows-path.el). Consult
the EmacsWiki
[for further information](https://www.emacswiki.org/emacs/Cygwin).
