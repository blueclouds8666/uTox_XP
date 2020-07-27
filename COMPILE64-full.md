# Compiling μTox and toxcore from source

Without dying in the try™ Edition

Disclaimer: this process or software comes with no warranty. <br />
Note: This guide can be followed and done with the **Windows XP SP3** operating system.
<br />
<br />

## Building a 64 bit binary

### Software required

We will mainly use two developer utilities called **MinGW** and **CMake GUI**. Files needed are:

- [CMake GUI installer](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/cmake-3.2.3-win32-x86.exe)
- [MinGW Portable](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW-portable.7z)
- [MinGW component - GCC Compiler x64](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20x64/mingw-w64-x86_64-7.1.0-release-win32-seh-rt_v5-rev2.7z)
- [MinGW component - GCC-ar x64](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20x64/mingw-w64-x86_64-7.1.0-hotfix-for-gcc-ar.7z)
- [MinGW component - package configurator x64](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20x64/mingw-w64-x86_64-pkg-config-0.29-1-any.pkg.tar.xz)
- [MinGW component - Yasm](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20shared/mingw-w64-i686-yasm-1.3.0-2-any.pkg.tar.xz)
- [MinGW component - Autoconf](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20shared/autoconf2.5-2.68-1-mingw32-bin.tar.xz)
- [MinGW component - Autoconf wrapper](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20shared/autoconf-10-1-mingw32-bin.tar.xz)
- [MinGW component - Automake](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20shared/automake1.11-1.11.1-1-mingw32-bin.tar.xz)
- [MinGW component - Automake wrapper](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20shared/automake-4-1-mingw32-bin.tar.xz)
- [MinGW component - Libtool](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20shared/libtool-2.4-1-mingw32-bin.tar.xz)
- [MSYS component - coreutils](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20msys/coreutils-5.97-MSYS-1.0.11-snapshot.tar.xz)
- [MSYS component - libcrypt](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20msys/libcrypt-1.1_1-3-msys-1.0.13-dll-0.tar.xz)
- [MSYS component - m4 macro processor](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20msys/m4-1.4.16-2-msys-1.0.17-bin.tar.xz)
- [MSYS component - Perl](https://github.com/blueclouds8666/uTox_XP/raw/files/utilities/MinGW%20Packages%20msys/perl-5.8.8-1-msys-1.0.17-bin.tar.xz)

1. Install CMake GUI with default values from *cmake-3.2.3-win32-x86.exe*.
2. Extract *MinGW-portable.7z* on the C:\ root folder. A new folder C:\MinGW will appear.
3. Now you will need to install the MinGW components above mentioned. <br />
  3.1. To install them, open each compressed file and extract **the content of the mingw32 / mingw64** folder to C:\MinGW. For those components that don't have that folder, just extract its root content to C:\MinGW.
4. Then, let's install the MSYS components, also mentioned on the previous list. <br />
  4.1. Extract the content of these compressed files to C:\MinGW\msys\1.0
5. Dev software is now installed. Now navigate to C:\MinGW\msys\1.0 and make a new folder called *project*.
6. Make another folder inside *project* called *prefix*.
<br />

### Compile *VPX*

c-toxcore depends on this library, so we need to compile it. Download it here:

- [VPX source code v1.3.0](https://codeload.github.com/webmproject/libvpx/zip/v1.3.0)

--> Extract it on C:\MinGW\msys\1.0\project\
--> Open the the MinGW's msys terminal, located on C:\MinGW\msys\1.0\msys.bat <br />
--> Execute the following commands to configure and proceed with the compilation:

```sh
cd /project/libvpx-1.3.0
CROSS=x86_64-w64-mingw32- ./configure --target=x86_64-win64-gcc --prefix=/project/prefix --disable-examples --disable-unit-tests --disable-shared --enable-static
make
make install
```
<br />

### Compile *Opus*

c-toxcore depends on this library, so we need to compile it. Download it here:

- [Opus source code v1.1](https://ftp.osuosl.org/pub/xiph/releases/opus/opus-1.1.tar.gz)

--> Extract it on C:\MinGW\msys\1.0\project\
--> Open the the MinGW's msys terminal, located on C:\MinGW\msys\1.0\msys.bat <br />
--> Execute the following commands to configure and proceed with the compilation:

```sh
cd /project/opus-1.1
./configure --host=x86_64-w64-mingw32 --prefix=/project/prefix --disable-extra-programs --disable-doc --disable-shared --enable-static
make
make install
```
<br />

### Compile *libsodium*

c-toxcore depends on this library, so we need to compile it. Download it here:

- [Libsodium source code v1.0.3](https://github.com/jedisct1/libsodium/archive/1.0.3.zip)

--> Extract it on C:\MinGW\msys\1.0\project\
--> Open the the MinGW's msys terminal, located on C:\MinGW\msys\1.0\msys.bat <br />
--> Execute the following commands to configure and proceed with the compilation:

```sh
cd /project/libsodium-1.0.3
./autogen.sh
./configure --host=x86_64-w64-mingw32 --prefix=/project/prefix --disable-shared --enable-static
make
make install
```
<br />

### Compile *c-toxcore*

Now that we have all required libraries, let's compile it. Download it here:

- [c-toxcore source code v0.1.11](https://github.com/TokTok/c-toxcore/archive/v0.1.11.zip)

--> Extract it on C:\MinGW\msys\1.0\project\
--> Open the the MinGW's msys terminal, located on C:\MinGW\msys\1.0\msys.bat <br />
--> Execute the following commands to configure and proceed with the compilation:

```sh
cd /project/c-toxcore-0.1.11
./autogen.sh
./configure --host=x86_64-w64-mingw32 --prefix=/project/prefix --disable-ntox --disable-tests --disable-testing --with-dependency-search=/project/prefix --disable-shared --enable-staticmake
make
make install
```
<br />

### Mixing all the libraries

We are still missing some libraries, damn. We have to download them precompiled from here:

- [OpenAl precompiled library x64](https://github.com/blueclouds8666/uTox_XP/raw/files/libraries-precompiled/windows-x64/libfilteraudio_build_windows_x86-64.zip)
- [audio_filter precompiled library x64](https://github.com/blueclouds8666/uTox_XP/raw/files/libraries-precompiled/windows-x64/libfilteraudio_build_windows_x86-64.zip)

--> just extract both compressed files over C:\MinGW\msys\1.0\project\prefix
<br />
<br />

### Preparing μTox source files

Now we will need the μTox source files, plus the third-party libraries. Those are:

- [uTox source code](https://github.com/blueclouds8666/uTox_XP/archive/oldtoxcore.zip)
- [uTox third party lib - stb](https://github.com/blueclouds8666/uTox_XP/raw/files/third-party%20libraries/stb-9d9f75eb682dd98b34de08bb5c489c6c561c9fa6.zip)
- [uTox third party lib - minIni](https://github.com/blueclouds8666/uTox_XP/raw/files/third-party%20libraries/minIni-77908366d4c0a758e33c4c6f39a29eba836ae7dd.zip)
- [uTox third party lib - QR Code generator](https://github.com/blueclouds8666/uTox_XP/raw/files/third-party%20libraries/QR-Code-generator-7e18dfe885f1cf2924078542927496c35d575ce7.zip)

7. Extract the μTox source code on C:\MinGW\msys\1.0\project
8. Rename the resulting folder to "uTox"
9. Copy the content of  \project\prefix  over  \project\uTox\libs\windows.
10. Browse to \project\uTox\third-party and extract there the three third-party libs.
<br />

### Final steps

11. Open CMake GUI. It can be found at Start menu > All programs > CMake.
12. Fill these gaps as following:

> - *Where is the source code:* C:/MinGW/msys/1.0/project/uTox
> - *Where to build the binaries:* C:/MinGW/msys/1.0/project/uTox/build

13. Click on generate. A new window will pop up, set the values as:

> - *Generator for this project:* MinGW Makefiles
> - *From the list below:* Specify native compilers

14. After clicking next, you will only need to define the C compiler path, which is: C:/MinGW/bin/x86_64-w64-mingw32-gcc.exe
15. Hit finish. If no errors show up, it means you did everything right, congratulations!
16. You can now compile the binary by running \project\uTox\build\buildWindows.bat. After the compiler finishes, you should get a binary EXE file on the same folder. Now it's time to enjoy μTox!
17. Several compiler options can be tweaked from the CMake panel. Make sure to click on Generate after you change them.
<br />
<br />