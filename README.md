# Composers Desktop Project

The [Composers Desktop Project](http://www.composersdesktop.com/) (CDP) is a software platform produced since the late 1980s by the eponymous organisation.
It is a suite of offline processes (also called CDP programs) for transforming audio files. This repository is simply a copy I made from the original source code provided
at [unstablesound.net/cdp.html](http://www.unstablesound.net/cdp.html), because I think having a navigable version of it is useful.
I am not the author of this code. The source code is released under the GNU Lesser General Public License (LGPL) v2.1.

__Note:__ CDP is actually on GitHub now, so I might delete this "fork" and ask to pull my changes: https://github.com/ComposersDesktop/CDP7

The following changes have been made to the source code archive linked to above:

- remove `.DS_Store` OS X desktop files
- remove `~` swap files
- replace `libaaio/libaaio-0.3.1.tar.bz2` with the extracted library directory `libaaio-0.3.1`
- add `-fPIC` C-compiler flag to libraries (`dev/cdp2k`, `dev/sfsys`, `dev/externals/portsf`)
- do not include prebuilt `.a` files
- fix problem with multiple macro definition of `min` and `max` (collision with STL) in `dev/externals/reverb/tdelaymain.cpp`

## Building on Linux

Dave Phillips has written a useful text about building the project on Linux: https://www.renoise.com/blog/linux-cdp-tool-guide

Since `libaaio` is already extracted here, the preparatory steps reduce to:

```bash
cd libaaio-0.3.1
./configure --prefix=/usr/local
make
sudo make install
```

Then to build CDP itself:

```bash
cd ../dev/
./makeprograms.sh
```

### Linker problems

__Note:__ While I could build the project without modifications under Debian Jessie with gcc 4.9.2, I had issues on Debian Stretch with gcc 6.3.0.
This is with `amd64` architecture. The errors are like this:

    /usr/bin/ld: ../portaudio/lib/.libs/libportaudio.a(pa_front.o): relocation R_X86_64_32 against `.rodata.str1.8' can not be used when making a shared object; recompile with -fPIC

This goes for the three librarys `libcdp2k`, `libsfsys`, and the included portaudio.

In order to make the build work, I added `-fPIC` to the `Makefile.linux` files of the three libraries. I don't know if this has implications for compiling on other platforms.
If adding the flag breaks something for you, you might want to remove this flag again. Note that `veryclean.sh` does not delete the libraries. You have to clean them
manually, like `cd dev/cdp2k; make veryclean -f Makefile.linux`.

I am still having problems compling the following programs, due to portaudio library problem (missing `-fPIC` still):

- listaudevs
- paplay
- pvplay
- recsf
