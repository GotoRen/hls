# HTTP Live Streaming Configuration
## 🌱 Environment
- Ubuntu Linux 20.04 LTS
  - `$ cat /etc/os-release`
    ```
    NAME="Ubuntu"
    VERSION="20.04.1 LTS (Focal Fossa)"
    ID=ubuntu
    ID_LIKE=debian
    PRETTY_NAME="Ubuntu 20.04.1 LTS"
    VERSION_ID="20.04"
    HOME_URL="https://www.ubuntu.com/"
    SUPPORT_URL="https://help.ubuntu.com/"
    BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
    PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
    VERSION_CODENAME=focal
    UBUNTU_CODENAME=focal
    ```

## 🎧 FFmpeg Configuration
- __🔨 必要なパッケージを準備__
  ```
  $ git clone https://github.com/GotoRen/hls
  $ sudo apt-get -y install autoconf automake build-essential cmake git libass-dev libfreetype6-dev libgpac-dev libsdl1.2-dev libtheora-dev libtool libva-dev libvdpau-dev libvorbis-dev libxcb1-dev libxcb-shm0-dev libxcb-xfixes0-dev mercurial pkg-config texi2html zlib1g-dev
  ```
- `$ cd ffmpeg-configuration/` 
- __🔨 nasm__
  ```
  $ cd nasm-2.15.05/
  $ sudo ./configure
  $ sudo make
  $ sudo make install
  
  $ which nasm
  /usr/local/bin/nasm
  
  $ nasm --version
  NASM version 2.15.05 compiled on Feb  4 2021
  ```
- __🔨 yasm__
  ```
  $ cd yasm-1.3.0/
  $ sudo ./configure
  $ sudo make
  $ sudo make install
  
  $ which yasm
  /usr/local/bin/yasm
  
  $ yasm --version
  yasm 1.3.0
  Compiled on Apr  1 2020.
  Copyright (c) 2001-2014 Peter Johnson and other Yasm developers.
  Run yasm --license for licensing overview and summary.
  ```
- __🔨 fdk-aac__
  ```
  $ cd fdk-aac-0.1.5/
  $ sudo ./configure
  $ sudo make
  $ sudo make install
  ```
- __🔨 x264 / x265__
  ```
  $ sudo apt-get install x264
  $ sudo apt-get install libx264-dev
  $ sudo apt-get install x265
  $ sudo apt-get install libx265-dev

  $ which x264
  /usr/bin/x264

  $ x264 --version
  x264 0.155.2917 0a84d98
  (libswscale 5.1.100)
  (libavformat 58.12.100)
  (ffmpegsource 2.23.0.0)
  built on Sep 27 2018, gcc: 8.2.0
  x264 configuration: --chroma-format=all
  libx264 configuration: --chroma-format=all
  x264 license: GPL version 2 or later
  libswscale/libavformat/ffmpegsource license: GPL version 2 or later

  $ which x265
  /usr/bin/x265

  $ x265 --version
  x265 [info]: HEVC encoder version 3.2.1+1-b5c86a64bbbe
  x265 [info]: build info [Linux][GCC 9.3.0][64 bit] 8bit+10bit+12bit
  x265 [info]: using cpu capabilities: MMX2 SSE2Fast LZCNT SSSE3 SSE4.2 AVX
  ```
- __🔨 libav__
  ```
  $ cd libav/
  $ sudo ./configure --enable-gpl --enable-nonfree --enable-libx264 --enable-libx265 --enable-libfdk-aac
  $ sudo make
  $ sudo make install
  ```
- __🔨 libvpx__
  ```
  $ sudo apt-get install libvpx-dev
  ```
- __🔨 ffmpeg__
  ```
  $ sudo apt-get install ffmpeg√
  $ cd FFmpeg/
  $ PKG_CONFIG_PATH=/opt/intel/mediasdk/lib/pkgconfig ./configure --prefix=/usr/local/ffmpeg --extra-cflags="-I/opt/intel/mediasdk/include" --extra-ldflags="-L/opt/intel/mediasdk/lib" --extra-ldflags="-L/opt/intel/mediasdk/plugins" --enable-vaapi --disable-debug --enable-libvorbis --enable-libvpx  --enable-gpl --cpu=native --enable-libfdk-aac --enable-libx264 --enable-libx265 --extra-libs=-lpthread --enable-nonfree
  $ sudo make
  $ sudo make install

  $ which ffmpeg
  /usr/bin/ffmpeg

  $ ffmpeg -version
  ffmpeg version 4.2.4-1ubuntu0.1 Copyright (c) 2000-2020 the FFmpeg developers
  built with gcc 9 (Ubuntu 9.3.0-10ubuntu2)
  configuration: --prefix=/usr --extra-version=1ubuntu0.1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --arch=amd64 --enable-gpl --disable-stripping --enable-avresample --disable-filter=resample --enable-avisynth --enable-gnutls --enable-ladspa --enable-libaom --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libcodec2 --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libjack --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librsvg --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-lv2 --enable-omx --enable-openal --enable-opencl --enable-opengl --enable-sdl2 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-nvenc --enable-chromaprint --enable-frei0r --enable-libx264 --enable-shared
  libavutil      56. 31.100 / 56. 31.100
  libavcodec     58. 54.100 / 58. 54.100
  libavformat    58. 29.100 / 58. 29.100
  libavdevice    58.  8.100 / 58.  8.100
  libavfilter     7. 57.100 /  7. 57.100
  libavresample   4.  0.  0 /  4.  0.  0
  libswscale      5.  5.100 /  5.  5.100
  libswresample   3.  5.100 /  3.  5.100
  libpostproc    55.  5.100 / 55.  5.100
  ```

## 🚀 FFmpeg Run
- __ffmpeg__
  ```
  $ cd /usr/local/ffmpeg/bin
  $ sudo ffmpeg -s 960x540 -i /dev/video0 -f alsa -i hw:0,0 -vcodec h264 -qmin 1 -qmax 3 -qdiff 8 -i_qfactor 1.40 -qcomp 0.7 -f mpegts udp://[配信先アドレス]:[配信先ポート]
  ```
    - cards：`$ cat /proc/asound/cards`
    - devices：`$ cat /proc/asound/devices`
- __ffplay__ 
  ```
  $ ffplay -fflags nobuffer udp://[配信元アドレス]:[配信元ポート]
  ```

## ☁️⚡ Other
- 🔨 __v4l2-utils__
  ```
  $ sudo apt-get install v4l-utils
  
  $ v4l2-ctl --list-devices
  $ v4l2-ctl -d /dev/video0 --all
  $ v4l2-ctl -d /dev/video0 --list-formats-ext
  ```
- 🔨 __g++ , ccmake__
  ```
  $ sudo apt-get install g++ cmake-curses-gui
  
  $ which g++
  /usr/bin/g++
  
  $ g++ --version
  g++ (Ubuntu 9.3.0-17ubuntu1~20.04) 9.3.0
  Copyright (C) 2019 Free Software Foundation, Inc.
  This is free software; see the source for copying conditions.  There is NO
  warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
  
  $ which ccmake
  /usr/bin/ccmake
  
  $ ccmake --version
  ccmake version 3.16.3
  CMake suite maintained and supported by Kitware (kitware.com/cmake).
  ```
- 🔨 __x264__
  ```
  $ sudo wget https://code.videolan.org/videolan/x264/-/archive/master/x264-master.tar.bz2
  $ tar xjvf x264-master.tar.bz2
  $ cd x264-master/
  
  $ sudo ./configure --enable-static --enable-shared
  $ sudo make
  $ sudo make install

  $ which x264
  /usr/local/bin/x264
  
  $ x264 --version
  x264 0.161.x
  built on Feb  4 2021, gcc: 9.3.0
  x264 configuration: --chroma-format=all
  libx264 configuration: --chroma-format=all
  x264 license: GPL version 2 or later
  ```
- 🔨 __x265__
  ```
  $ git clone https://github.com/videolan/x265.git
  $ cd x265/
  
  $ cd build/linux
  $ sudo ./make-Makefiles.bash
     >> qを押す（変更無し）
  $ sudo make
  $ sudo make install

  $ which x265
  /usr/local/bin/x265
  
  $ x265 --version
  x265 [info]: HEVC encoder version 3.4+28-419182243
  x265 [info]: build info [Linux][GCC 9.3.0][64 bit] 8bit
  x265 [info]: using cpu capabilities: MMX2 SSE2Fast LZCNT SSSE3 SSE4.2 AVX FMA3 BMI2 AVX2
  ```
- 🔨 __opus codec__
  ```
  $ sudo wget https://archive.mozilla.org/pub/opus/opus-1.3.1.tar.gz
  $ tar xzvf opus-1.3.1.tar.gz
  $ cd opus-1.3.1/
  
  $ sudo ./configure
  $ sudo make
  $ sudo make install
  ```
- 🔨 __ALSA__
  ```
  $ sudo apt-get install libasound2-dev
  $ cd /usr/src
  $ git clone git://source.ffmpeg.org/ffmpeg.git
  $ cd ffmpeg/
  
  $ sudo ./configure && sudo make && sudo make install
  
  $ which alsa
  /usr/sbin/alsa
  
  $ alsa --version
  Usage: /sbin/alsa {unload|reload|force-unload|force-reload|suspend|resume}
  ```

## 🚀 AVconverter Run
- __avconv__
  ```
  $ sudo avconv -i /dev/video0 -f video4linux2 -list_formats all
  $ sudo avconv -f video4linux2 -list_formats all -i /dev/video0
  ```
  ```
  $ sudo avconv -f video4linux2 -video_size 1280x720 -framerate 30 -i /dev/video0 \
  -f alsa -ac 2 -ar 44100 -i hw:1,0 \
  -vcodec libx264 -pre veryfast -b:v 512000 \
  -acodec libfdk_aac -b:a 256000 -ar 44100 \
  -f hls -hls_list_size 10 -hls_time 10 ~/out.m3u8
  ```