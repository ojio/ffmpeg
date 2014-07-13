# This builds off of a base Ubuntu 14.04 system and compiles ffmpeg and mplayer/mencoder from source.

## FFMPEG is compiled with:

```
configuration: --shlibdir=/usr/lib64 --prefix=/usr --mandir=/usr/share/man --libdir=/usr/lib64 --enable-static --extra-cflags='-fmessage-length=0 -grecord-gcc-switches -fstack-protector -O2 -Wall -D_FORTIFY_SOURCE=2 -funwind-tables -fasynchronous-unwind-tables -g -fPIC -I/usr/include/gsm' --enable-gpl --disable-x11grab --enable-version3 --enable-pthreads --enable-avfilter --enable-libpulse --enable-libvpx --enable-libopus --enable-libass --disable-libx265 --enable-libmp3lame --enable-libvorbis --enable-libtheora --enable-libspeex --enable-libxvid --enable-libx264 --enable-libschroedinger --enable-libgsm --enable-libopencore-amrnb --enable-libopencore-amrwb --enable-postproc --disable-libdc1394 --enable-librtmp --enable-libfreetype --enable-avresample --enable-libtwolame --enable-libvo-aacenc --enable-gnutls --enable-nonfree --enable-libfdk-aac --enable-libfaac --enable-libopenjpeg --enable-gray --enable-libwebp
  libavutil      52. 92.100 / 52. 92.100
  libavcodec     55. 69.100 / 55. 69.100
  libavformat    55. 46.100 / 55. 46.100
  libavdevice    55. 13.102 / 55. 13.102
  libavfilter     4. 10.100 /  4. 10.100
  libavresample   1.  3.  0 /  1.  3.  0
  libswscale      2.  6.100 /  2.  6.100
  libswresample   0. 19.100 /  0. 19.100
  libpostproc    52.  3.100 / 52.  3.100
```

## and MPLAYER/MENCODER is set to query CPU capabilities at runtime to get something like:

```
MPlayer SVN-r37239-4.8 (C) 2000-2014 MPlayer Team
CPU vendor name: GenuineIntel  max cpuid level: 13
CPU: Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz (Family: 6, Model: 62, Stepping: 4)
extended cpuid-level: 8
extended cache-info: 16801856
Detected cache-line size is 64 bytes
CPUflags:  MMX: 1 MMX2: 1 3DNow: 0 3DNowExt: 0 SSE: 1 SSE2: 1 SSE3: 1 SSSE3: 1 SSE4: 1 SSE4.2: 1 AVX: 1
Compiled for x86 CPU with extensions: MMX MMX2 SSE SSE2 SSE3 SSSE3 SSE4 SSE4.2 AVX CMOV
```

