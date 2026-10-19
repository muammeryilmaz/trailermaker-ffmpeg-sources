# Mydos Cut — FFmpeg corresponding source

This repository provides the source code of the open source native libraries
distributed inside the **Mydos Cut** Android app (package `com.mydoscode.mydoscut`, formerly TrailerMaker), as required by the GNU
Lesser General Public License (LGPL). The app's own code is not part of it.

*Türkçe özet: Mydos Cut Android uygulamasının içinde dağıtılan FFmpeg ve
onunla gelen açık kaynak kütüphanelerin kaynak kodları LGPL gereği burada
yayınlanır. Uygulamanın kendi kodu bu depoda değildir.*

## What the app ships

| Component | Version | Source |
|---|---|---|
| FFmpeg (libavcodec, libavdevice, libavfilter, libavformat, libavutil, libswresample, libswscale) | **8.1.2**, unmodified | release asset `ffmpeg-8.1.2.tar.xz` (+ upstream signature `.asc`) — <https://ffmpeg.org/releases/> |
| FFmpegKit wrapper (`libffmpegkit.so`, Java API) | ffmpeg-kit 6.0.LTS scripts | release asset `ffmpeg-kit-v6.0.LTS-build-scripts.zip` — <https://github.com/arthenica/ffmpeg-kit/tree/v6.0.LTS> |
| Android packaging | Maven `com.antonkarpenko:ffmpeg-kit-full:2.2.3` | <https://github.com/sk3llo/ffmpeg_kit_flutter_android/tree/full> |

The libraries are dynamically linked shared objects (`lib*.so` in the APK)
and can be replaced. FFmpeg is built **without** `--enable-gpl` and
`--enable-nonfree`; the build is LGPL-3.0-or-later (it uses `--enable-version3`).

FFmpeg configure flags, as embedded in the shipped `libavutil.so`:

```
--disable-alsa --disable-appkit --disable-audiotoolbox --disable-autodetect --disable-cuda --disable-cuvid --disable-debug --disable-doc --disable-htmlpages --disable-indev=fbdev --disable-manpages --disable-neon-clobber-test --disable-nvenc --disable-openssl --disable-outdev=fbdev --disable-podpages --disable-programs --disable-schannel --disable-sdl2 --disable-securetransport --disable-sndio --disable-static --disable-txtpages --disable-vaapi --disable-vdpau --disable-videotoolbox --disable-xlib --disable-xmm-clobber-test --enable-asm --enable-cross-compile --enable-gmp --enable-gnutls --enable-iconv --enable-inline-asm --enable-jni --enable-libass --enable-libdav1d --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libharfbuzz --enable-libilbc --enable-libkvazaar --enable-libmp3lame --enable-libopencore-amrnb --enable-libopus --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libtheora --enable-libtwolame --enable-libvo-amrwbenc --enable-libvorbis --enable-libvpx --enable-libwebp --enable-libxml2 --enable-libzimg --enable-lto --enable-mediacodec --enable-neon --enable-optimizations --enable-pic --enable-pthreads --enable-shared --enable-small --enable-swscale --enable-v4l2-m2m --enable-version3 --enable-zlib 
```

## External libraries in the build

The FFmpegKit build scripts pin every external library to a tag of the
arthenica mirrors (see `scripts/source.sh` in the build-script archive).
The Android packager states that arm64 libraries were later updated, so the
column *Checked* shows whether the version was confirmed from strings inside
the shipped binaries.

| Library | License | Version | Checked | Source in this repo |
|---|---|---|---|---|
| GnuTLS | LGPL-2.1+ | 3.8.9 | ✔ binary | `gnutls-3.8.9.tar.xz` |
| FriBidi | LGPL-2.1+ | 1.0.13 | ✔ binary | `fribidi-1.0.13.tar.gz` |
| LAME | LGPL-2.0+ | 3.100 | ✔ binary | `lame-3.100.tar.gz` |
| libvpx | BSD-3 | 1.13.0 | ✔ binary | upstream |
| GMP | LGPL-3.0+ / GPL-2.0+ | 6.2.1 | scripts | `gmp-6.2.1.tar.gz` |
| Nettle | LGPL-3.0+ / GPL-2.0+ | 3.8.1 | scripts | `nettle-3.8.1.tar.gz` |
| libiconv | LGPL-2.1+ | 1.17 | scripts | `libiconv-1.17.tar.gz` |
| TwoLAME | LGPL-2.1+ | 0.4.0 | scripts | `twolame-0.4.0.tar.gz` |
| SoX Resampler | LGPL-2.1+ | 0.1.3 | scripts | `soxr-0.1.3.tar.gz` |
| shine | LGPL-2.0+ | 3.1.1 | scripts | `shine-3.1.1.tar.gz` |
| libass | ISC | 0.17.1 | scripts | `libass-0.17.1.tar.gz` |
| dav1d, fontconfig, freetype, harfbuzz, kvazaar, libilbc, libogg, libtheora, libvorbis, libwebp, libxml2, opencore-amr, opus, snappy, speex, vo-amrwbenc, zimg, expat, libpng, libuuid | permissive (BSD, MIT, ISC, Apache-2.0, FTL, zlib, WTFPL) | per build scripts | scripts | upstream, see `scripts/source.sh` |

All archives are attached to the GitHub release
[`ffmpeg-8.1.2-kit-2.2.3`](../../releases/tag/ffmpeg-8.1.2-kit-2.2.3);
`SHA256SUMS` lists their checksums.

If you need the exact source of any component in a version not provided
here, open an issue in this repository.

## Licenses

`COPYING.LGPLv3` and `COPYING.GPLv3` contain the license texts. Each
source archive carries its own license files.
