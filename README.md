# Source Tickrate (Server addon)

A _standalone_ **Source Engine** server addon that enables the `-tickrate` command line parameter.

> **srcdslab fork** of [angelfor3v3r/source-tickrate](https://github.com/angelfor3v3r/source-tickrate)
> by angelfor3v3r. All credit for the addon goes to upstream; this fork only adapts the build and
> release pipeline to the srcdslab conventions (Linux builds that run on glibc 2.31 and later).
> See [CHANGELOG.md](CHANGELOG.md).

Currently tested on:
* Counter-Strike: Source (32-bit & 64-bit)
* Team Fortress 2 (32-bit & 64-bit)

**Note**: This plugin may also work on other source games, but it's untested. If there's a Source game you'd like it to work on, and you've confirmed it doesn't work, then please feel free to open an issue or pull request.

## Usage & Installation

Download the archive for your server's OS and architecture from the [releases](https://github.com/srcdslab/source-tickrate/releases) and extract it into your server's game mod folder (i.e. `cstrike`, `tf`, etc).

Archives are named `source-tickrate-<version>-<os>-<arch>.tar.gz`, where `<version>` is a tag or `latest` (rebuilt on every push to the default branch), `<os>` is `linux` or `windows` and `<arch>` is `x86_64` (64-bit server) or `x86` (32-bit server). Each one contains:
```
addons/tickrate_x86-64.so   (tickrate_x86-32.so, or .dll on Windows)
addons/tickrate_x86-64.vdf  (tickrate_x86-32.vdf)
```
Only install the archive matching your server: the engine tries to load every `.vdf` in `addons`.

The Linux builds are made on Ubuntu 20.04 (glibc 2.31), so they run on any distribution with glibc 2.31 or newer.

You can now pass `-tickrate <Desired Tickrate>` on the command line.
Example for **Counter-Strike: Source**:
```
srcds.exe -console -game cstrike +maxplayers 10 +map de_nuke -tickrate 100
```

Note that you must set ConVars such as `sv_maxupdaterate`, `sv_maxcmdrate`, etc. to accommodate the new tickrate setting.

## Building

If the releases don't fit your needs then you can build the library yourself.\
Building requires **CMake 3.15** (or later) and a **C++17** ready compiler.\
The CI builds Linux releases in an `ubuntu:20.04` container so the library runs on glibc 2.31; building on a newer distribution can raise that requirement.

Here are some examples (assuming a 64-bit OS):

### Windows (MSVC):

```
64-bit:
    cmake -G "Visual Studio 17 2022" -A x64 -B cmake-build-x86_64
    cmake --build cmake-build-x86_64 --config Release
    
32-bit:
    cmake -G "Visual Studio 17 2022" -A Win32 -B cmake-build-x86_32
    cmake --build cmake-build-x86_32 --config Release
```

### Linux (GCC):

```
64-bit: 
    cmake -B cmake-build-x86_64 -DCMAKE_C_COMPILER=gcc -DCMAKE_CXX_COMPILER=g++ -DCMAKE_BUILD_TYPE=Release
    cmake --build cmake-build-x86_64 --config Release
    
32-bit: 
    cmake -B cmake-build-x86_32 -DCMAKE_C_COMPILER=gcc -DCMAKE_CXX_COMPILER=g++ -DCMAKE_BUILD_TYPE=Release -DCMAKE_CXX_FLAGS=-m32 -DCMAKE_C_FLAGS=-m32 -DCMAKE_BUILD_TYPE=Release
    cmake --build cmake-build-x86_32 --config Release
```

## Thanks
[angelfor3v3r/source-tickrate](https://github.com/angelfor3v3r/source-tickrate) (upstream)\
[SafetyHook](https://github.com/cursey/safetyhook)\
[Zydis](https://github.com/zyantific/zydis)\
[expected](https://github.com/TartanLlama/expected)\
[{fmt}](https://github.com/fmtlib/fmt)\
[CPM.cmake](https://github.com/cpm-cmake/CPM.cmake)
