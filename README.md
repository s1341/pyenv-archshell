pyenv-archshell
===============

An extension to the `pyenv shell` command, allowing LD_LIBRARY_PATH to be set
when necessary.

This plugin adds the `pyenv archshell` command, which is a wrapper around the
standard `pyenv shell` command.

At the moment, this plugin only has an effect on linux.

If a version is specified, `archshell` will try to determine if the python
binaries in that version are compiled for the same architecture as the host. If
not, `LD_LIBRARY_PATH` will be set.

For example, even on a 64-bit host some 32-bit applications try to dynamically
link against python. If only a 64-bit python is available the loader will fail
and the process will not function correctly.

Current versions of pyenv (with PR yyuu/pyenv/#168), should easily be able to
install a 32-bit python on a 64-bit host.

It's not enough to have a 32-bit python available. We must tell the 32-bit
applications where to find the correct version of the library. By default, it
will search the standard library paths and will pick up the 64-bit shared
object.

We can help the process find the correct version by setting LD_LIBRARY_PATH.

The `archshell` command automates the process of switching to a specific pyenv
version and setup the LD_LIBRARY_PATH as needed.

## Usage

```
pyenv archshell 2.7.5_32bit

./my_32bit_app
```
