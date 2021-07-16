# Examples

## CMake

[cmake.yml](cmake.yml) shows how to install the relevant toolchain package for each msystem choice.
See [the MSYS2 documentation](https://www.msys2.org/docs/environments/) for explanations on the different msystem
options available.

When building for mingw with CMake, one has to take care to install the mingw version, not msys version, of CMake, i.e.
the one prefixed with `mingw-w64-*`.

Compared to the GitHub Actions CMake examples/templates (see [actions/starter-workflows: ci/cmake.yml](https://github.com/actions/starter-workflows/blob/main/ci/cmake.yml)),
there's a few changes:

* Don't use the `${{github.workspace}}` for specifying an absolute path; it's
  spelled out with backslashes, which don't work as intended when interpreted
  by the bash shell. Instead use relative paths (the run commands start out
  with `${{github.workspace}}` as the current working directory anyway).

* When building with CMake on Windows for mingw targets, one has to set a
  a choice of generator with `-G`; the default is NMake, which looks for
  the installed MSVC compilers instead. You can choose between `Ninja`
  (install `${{matrix.prefix}}-ninja`; the build uses the command `ninja`),
  `MinGW Makefiles` (install `${{matrix.prefix}}-make`, the build uses
  `mingw32-make`) or `MSYS Makefiles` (install `make`, and the build uses
  the plain `make` command).

## PKGBUILD

[pkgbuild.yml](pkgbuild.yml) shows how to build and test a package using a PKGBUILD recipe.
