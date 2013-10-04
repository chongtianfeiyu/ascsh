ActionScript Compiler 2.0 Shell
===============================

`ascsh` and `ascshd`* are wrappers for the new ActionScript Compiler 2.0,
modelled to be roughly equivalent to the older Flex Compiler's `fcsh` and `fcshd`.
They improve AS3/AIR/SWF/SWC project compilation performance by maintaining a
persistent JVM compiler process.

Setup
-----

Clone (or download) the repo and run `./install.sh` (Linux/Mac) or `install.bat` (Windows).  Install will alert
you that you must have the `$AIR_HOME` environment variable set.  If so, it will compile and install `ascsh` and
`acsshd` into the AIR SDK bin and lib directories.

`uninstall.sh` and `uninstall.bat` remove `ascsh` and `ascshd`

Usage
-----

`ascsh `is a shell (like `fcsh`) that it a shell and requires text input to kick off a new
build.  Simply enter your compile command at the prompt:

````
> $AIR_HOME/bin/ascsh
ascsh v0.2 by Jeff Ward, simbulus.com
(ascsh)
mxmlc main.as -o Main.as
  ... 10 second build
(ascsh)
mxmlc main.as -o Main.as
  ... 2 second build
(ascsh)
````

`ascshd` is a convenience wrapper around `ascsh` currently written in Ruby.  It
starts a background server thread to maintain the `ascsh` process, and sends
commands to it for builds.  This way, your build can simply call `ascshd` again
and again from your build system (no fussy shell), and it just gets faster over time:

````
> $AIR_HOME/bin/ascsdh mxmlc main.as -o Main.as
  ... 10 second build
> $AIR_HOME/bin/ascsdh mxmlc main.as -o Main.as
  ... 2 second build
````

Stop the server process by calling `ascshd kill`

* Note that **ascshd may not work under Windows**.  It's currently a Ruby script
that uses processes, sockets, and process I/O to operate, and it seems to
hang on Windows.  I'd like to hear others' feedback - feel free to contribute a
Windows-compatible `ascshd` (in any language you like - perl, python, Java, etc.)
The ruby script should be fairly straight-forward to replicate.

History
-------

version 0.2 - working ascsh, ascshd in Ruby (Windows support iffy)
version 0.1 - proof of concept
