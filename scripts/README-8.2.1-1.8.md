# xPack GNU ARM Embedded GCC

This is the **xPack** version of the 
[GNU Arm Embedded Toolchain](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm).

For details, see 
[The xPack GNU ARM Embedded GCC](https://xpack.github.io/arm-none-eabi-gcc/) pages.

## Easy install

The **xPack ARM Embedded GCC** toolchain is also available as a 
binary [xPack](https://www.npmjs.com/package/@xpack-dev-tools/arm-none-eabi-gcc) 
and can be conveniently installed with [xpm](https://www.npmjs.com/package/xpm):

```console
$ xpm install --global @xpack-dev-tools/arm-none-eabi-gcc
```

For more details on how to install the toolchain, please see 
[How to install the ARM toolchain?](http://gnu-mcu-eclipse.github.io/toolchain/arm/install/) page.

## Compliance

This release closely follows the official ARM distribution, as described 
in the original ARM release text files:

- `distro-info/arm-readme.txt`
- `distro-info/arm-release.txt`

## Changes

Compared to the ARM distribution, the build procedure is more or less the 
same and there should be no functional differences, except the following 
bug fixes:

- [Issue:[#4](https://github.com/gnu-mcu-eclipse/arm-none-eabi-gcc-build/issues/4)]
  the Windows paths with spaces bug apparently was caused by an old version of 
  and with the new version (5.0.4) the 
  [89249](https://gcc.gnu.org/bugzilla/show_bug.cgi?id=89249) 
  `gcc.c` patch is no longer needed;
- [Issue:[#3](https://github.com/gnu-mcu-eclipse/arm-none-eabi-gcc-build/issues/3)]
  due to a problem in the GCC configure script and the specifics of the static
  build, LTO was not effective on Windows, and the initial workaround proved 
  not effective either; in the new build environment the configure script is
  enables LTO and it is functional on windows too;
- [Issue:[#1](https://github.com/gnu-mcu-eclipse/arm-none-eabi-gcc-build/issues/1)]
  the `liblto_plugin` copied/linked to the `lib/bdf-plugins` for `ar`
  to find it and be able to process archives with LTO objects
- a patch was applied to binutils to fix the 32-bit objcopy bug 
  [24065](https://sourceware.org/bugzilla/show_bug.cgi?id=24065)
- a patch was applied to gcc to fix the Windows LTO with -g bug
  [89183](https://gcc.gnu.org/bugzilla/show_bug.cgi?id=89183)

GDB was built with the latest Git commit bda678b9 from 2019-05-09, 
corresponding to GDB 8.3.50, to fix
the bugs affecting C++ LTO projects
[24145](https://sourceware.org/bugzilla/show_bug.cgi?id=24145)

## Compatibility

The binaries were built using 
[xPack Build Box (XBB)](https://github.com/xpack/xpack-build-box), a set 
of build environments based on slightly older distributions, that should be 
compatible with most recent systems.

- GNU/Linux: all binaries were built with GCC 7.4, running in a CentOS 6 
  Docker container
- Windows: all binaries were built with mingw-w64 GCC 7.4, running in a 
  CentOS 6 Docker container 
- macOS: most binaries were built with GCC 7.4, running in a separate  
  folder on macOS 10.10.5; GDB cannot be compiled with GCC, so Apple 
  clang was used.

Partial support for Python3 was added to GDB for GNU/Linux and macOS; 
not yet available on Windows ([24469](https://sourceware.org/bugzilla/show_bug.cgi?id=24469)).

## Build

The scripts used to build this distribution are in:

- `distro-info/scripts`

For the prerequisites and more details on the build procedure, please see the 
[How to build?](https://github.com/xpack-dev-tools/arm-none-eabi-gcc-xpack/blob/xpack/README-BUILD.md) page. 

## Documentation

The original PDF documentation is available in the `share/doc` folder.

## More info

For more info and support, please see the xPack project site:

  http://xpack.github.io/arm-none-eabi-gcc/

Thank you for using open source software,

Liviu Ionescu

