# 1. vcpkg

- [1. vcpkg](#1-vcpkg)
  - [1.1. 项目介绍](#11-项目介绍)
    - [1.1.1. 工程目录介绍](#111-工程目录介绍)
    - [1.1.2. 为不同目标自定义vcpkg实例](#112-为不同目标自定义vcpkg实例)
  - [1.2. 支持的平台](#12-支持的平台)
  - [1.3. 常用命令](#13-常用命令)
    - [1.3.1. search](#131-search)
    - [1.3.2. install](#132-install)
    - [1.3.3. export](#133-export)
  - [1.4. IDE集成](#14-ide集成)
    - [1.4.1. Visual studio](#141-visual-studio)
    - [1.4.2. VSCode](#142-vscode)
    - [1.4.3. cmake](#143-cmake)
  - [1.5. 问题集](#15-问题集)
    - [1.5.1. 自定义库如何添加到vcpkg中](#151-自定义库如何添加到vcpkg中)
  - [1.6. 参考资料](#16-参考资料)

## 1.1. 项目介绍

[git](https://github.com/Microsoft/vcpkg)

### 1.1.1. 工程目录介绍

- buildtrees - Contains subfolders of sources from which each library is built.
- docs - documentation and examples.
- downloads - Cached copies of any downloaded tools or sources. vcpkg searches here first when you run the install command.
- installed - Contains the headers and binaries for each installed library. When you integrate with Visual Studio, you're essentially telling it add this folder to its search paths.
- packages - Internal folder for staging between installs.
- ports - Files that describe each library in the catalog, its version, and where to download it. You can add your own ports if needed.
- scripts - Scripts (CMake, PowerShell) used by vcpkg.
- toolsrc - C++ source code for vcpkg and related components.
- triplets - Contains the settings for each supported target platform (for example, x86-windows or x64-uwp).

- buildtrees -包含用于构建每个库的源子文件夹。
- docs -文档和示例。
- downloads-任何下载的工具或源的缓存副本。运行安装命令时，vcpkg首先在此处搜索。
- installed-包含每个已安装库的标头和二进制文件。与Visual Studio集成时，实际上是在告诉它将此文件夹添加到其搜索路径。
- packages -内部文件夹，用于安装之间的暂存。
- ports-描述目录中每个库，其版本以及下载位置的文件。您可以根据需要添加自己的端口。
- scripts -vcpkg使用的脚本（CMake，PowerShell）。
- toolsrc -vcpkg和相关组件的C ++源代码。
- triplets -包含每个受支持的目标平台的设置（例如x86-windows或x64-uwp）。

### 1.1.2. 为不同目标自定义vcpkg实例

## 1.2. 支持的平台

`.\vcpkg.exe help triplet`

&emsp;&emsp;注意：这里的arm架构特指类似于surface这种运行在arm处理器上的Win10平台，而并非我们传统意义上的Linux或android的ARM平台。

```powershell
Available architecture triplets
VCPKG built-in triplets:
  arm-uwp
  arm64-windows
  x64-linux
  x64-osx
  x64-uwp
  x64-windows-static
  x64-windows
  x86-windows

VCPKG community triplets:
  arm-ios
  arm-linux
  arm-mingw-dynamic
  arm-mingw-static
  arm-windows
  arm64-ios
  arm64-linux
  arm64-mingw-dynamic
  arm64-mingw-static
  arm64-osx
  arm64-uwp
  arm64-windows-static
  s390x-linux
  wasm32-emscripten
  x64-ios
  x64-mingw-dynamic
  x64-mingw-static
  x64-openbsd
  x64-osx-dynamic
  x64-windows-static-md
  x86-ios
  x86-mingw-dynamic
  x86-mingw-static
  x86-uwp
  x86-windows-static-md
  x86-windows-static
  x86-windows-v120
```

## 1.3. 常用命令

### 1.3.1. search

`vcpkg search ffmpeg`

```powershell
ffmpeg               4.3.1#9          a library to decode, encode, transcode, mux, demux, stream, filter and play pr...
ffmpeg[avcodec]                       Codec support in ffmpeg
ffmpeg[avdevice]                      Device support in ffmpeg
ffmpeg[avfilter]                      Filter support in ffmpeg
ffmpeg[avformat]                      Format support in ffmpeg
ffmpeg[avisynthplus]                  avisynthplus support in ffmpeg
ffmpeg[avresample]                    Libav audio resampling library support in ffmpeg
ffmpeg[bzip2]                         bzip2 support in ffmpeg
ffmpeg[fdk-aac]                       AAC de/encoding via libfdk-aac support in ffmpeg
ffmpeg[ffmpeg]                        build the ffmpeg.exe application
ffmpeg[ffplay]                        ffplay application support in ffmpeg
ffmpeg[ffprobe]                       ffprobe application support in ffmpeg
ffmpeg[gpl]                           allow GPL licensed libraries
ffmpeg[iconv]                         iconv support in ffmpeg
ffmpeg[lzma]                          lzma support in ffmpeg
ffmpeg[mp3lame]                       MP3 encoding via libmp3lame support in ffmpeg
ffmpeg[nonfree]                       allow nonfree and unredistributable libraries
ffmpeg[nvcodec]                       Hardware accelerated codecs
ffmpeg[opencl]                        OpenCL processing support in ffmpeg
ffmpeg[openssl]                       openssl support in ffmpeg
ffmpeg[opus]                          Opus de/encoding via libopus support in ffmpeg
ffmpeg[postproc]                      Postproc support in ffmpeg
ffmpeg[sdl2]                          sdl2 support in ffmpeg
ffmpeg[snappy]                        Snappy compression, needed for hap encoding support in ffmpeg
ffmpeg[soxr]                          libsoxr resampling support in ffmpeg
ffmpeg[speex]                         Speex de/encoding via libspeex support in ffmpeg
ffmpeg[swresample]                    Swresample support in ffmpeg
ffmpeg[swscale]                       Swscale support in ffmpeg
ffmpeg[theora]                        Theora encoding via libtheora support in ffmpeg
ffmpeg[version3]                      upgrade (L)GPL to version 3
ffmpeg[vorbis]                        Vorbis en/decoding via libvorbis support in ffmpeg
ffmpeg[vpx]                           VP8 and VP9 de/encoding via libvpx support in ffmpeg
ffmpeg[wavpack]                       wavpack encoding via libwavpack support in ffmpeg
ffmpeg[x264]                          H.264 encoding via x264 support in ffmpeg
ffmpeg[x265]                          HEVC encoding via x265 support in ffmpeg
ffmpeg[zlib]                          zlib support in ffmpeg
ffnvcodec            10.0.26.0        FFmpeg version of Nvidia Codec SDK headers.
opencv[ffmpeg]                        ffmpeg support for opencv
opencv2[ffmpeg]                       ffmpeg support for opencv
opencv3[ffmpeg]                       ffmpeg support for opencv
opencv4[ffmpeg]                       ffmpeg support for opencv
openimageio[ffmpeg]                   Enable ffmpeg support for openimageio
```

### 1.3.2. install

`vcpkg install ffmpeg[gpl]:x86-windows-static`

search 出来的 `[]`

### 1.3.3. export

## 1.4. IDE集成

### 1.4.1. Visual studio

### 1.4.2. VSCode

### 1.4.3. cmake

## 1.5. 问题集

### 1.5.1. 自定义库如何添加到vcpkg中

## 1.6. 参考资料

1. [官网](https://docs.microsoft.com/en-us/cpp/build/vcpkg?view=msvc-160)
2. [vc第三方库辅助管理工具vcpkg的安装使用](https://cloud.tencent.com/developer/article/1443852)