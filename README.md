# `framework-arduinoteensy-cxx20`
A fork of the PlatformIO ArduinoTeensy framework compatible with GCC 10 & C++20.

# Usage

## Prerequisites

In order to build with this framework, you'll need to clone a few repos.

### Clone framework and dependencies

First, clone this repository:

```sh
git clone https://github.com/thevisus/framework-arduinoteensy-cxx20.git
```

This framework is compatible with the GNU ARM Embedded Toolchain v10.2.1. A
corresponding [PlatformIO
toolchain](https://github.com/thevisus/toolchain-gcc-arm-embedded) is therefore
necessary:

```sh
git clone https://github.com/thevisus/toolchain-gcc-arm-embedded.git
```

Finally, a PlatformIO "platform" is needed to drive the build:

```sh
git clone https://github.com/thevisus/teensy-gcc10.git
```

Each of these needs to be installed locally via PlatformIO. The `pio` command or
similar management software should be able to do this. The simplest method, on
Linux/macOS is to symlink the projects into the PlatformIO user directory:

```sh
ln -s /path/to/framework-arduinoteensy-cxx20 $HOME/.platformio/packages
ln -s /path/to/toolchain-gcc-arm-embedded $HOME/.platformio/packages
ln -s /path/to/teensy-gcc10 $HOME/.platformio/platforms
```

You may check the full platform's availability using `pio`:

```sh
pio platform show teensy-gcc10
```

## Configuring a project

In your project's `platform.ini`, adjust your environment settings similar to
the following:

```ini
[platformio]
default_envs = teensy41

[env:teensy41]
platform = teensy-gcc10
platform_packages = toolchain-gcc-arm-embedded
board = teensy41
framework = arduino
```

## Building a project

If everything is setup correctly, you may build your project per usual.

```sh
# compile
pio run
# upload
pio run --target upload
```

### Example Makefile

Driving the pio process via `make` can be accomplished with a simple Makefile.
(NB: this version assumes `make` will be invoked from within `vim`; if that's
not the case, remove the `-c vim` portions.)

```Makefile
all:
	pio -c vim run

upload:
	pio -c vim run --target upload

clean:
	pio -c vim run --target clean

program:
	pio -c vim run --target program

uploadfs:
	pio -c vim run --target uploadfs

update:
	pio -c vim update
```

# Upstream
The code in `cores` is up-to-date as of late 2020 from the original
https://github.com/PaulStoffregen/cores repo, combined with the libraries and
tools found in PlatformIO's original framework-arduinoteensy. It's a bit of a
mish-mash, but is fairly up-to-date and functional (tested and run in live
systems for several months now).

However, due to the amalgamation of repos and a variety of other reasons, the
`cores` code will only be minimally updated for critical fixes, if at all.
Instead, a leaner version of the 4.1 core, intended to be built with the
[dds](https://github.com/vector-of-bool/dds) toolchain is actively maintained at
my personal Gitea: https://git.thevis.us/visus/teensy-core-4.1

# License
```
Teensyduino Core Library
http://www.pjrc.com/teensy/
Copyright (c) 2017 PJRC.COM, LLC.

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

1. The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

2. If the Software is incorporated into a build system that allows
selection among a list of target devices, hen similar target
devices manufactured by PJRC.COM must be included in the list of
target devices and selectable in the same manner.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS
BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN
ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

