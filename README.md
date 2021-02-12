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
- Execution by UDP Stream

## 🔨 v4l2-utils
```
### インストール
$ sudo apt-get install v4l-utils

### 確認
$ v4l2-ctl --list-devices
$ v4l2-ctl -d /dev/video0 --all
$ v4l2-ctl -d /dev/video0 --list-formats-ext
```

## 🔨 NASM
```
### インストール
$ sudo wget https://www.nasm.us/pub/nasm/stable/nasm-2.15.05.tar.bz2
$ tar xjvf nasm-2.15.05.tar.bz2 
$ cd nasm-2.15.05/

### 実行
$ sudo ./configure
$ sudo make
$ sudo make install

### 確認
$ which nasm
/usr/local/bin/nasm

$ nasm --version
NASM version 2.15.05 compiled on Feb  4 2021
```

## 🔨 YASM
```
### インストール
$ sudo wget http://www.tortall.net/projects/yasm/releases/yasm-1.3.0.tar.gz
$ sudo tar xvf yasm-1.3.0.tar.gz 
$ cd yasm-1.3.0/

### 実行
$ sudo ./configure

### 確認
$ which yasm
/usr/bin/yasm

$ yasm --version
yasm 1.3.0
Compiled on Apr  1 2020.
Copyright (c) 2001-2014 Peter Johnson and other Yasm developers.
Run yasm --license for licensing overview and summary.
```

## 🔨 g++ , ccmake
```
### インストール
$ sudo apt-get install g++ cmake-curses-gui

### 確認
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

## 🔨 x264
```
### インストール
$ sudo apt-get install x264
$ sudo apt-get install libx264-dev
$ sudo wget https://code.videolan.org/videolan/x264/-/archive/master/x264-master.tar.bz2
$ tar xjvf x264-master.tar.bz2
$ cd x264-master/

### 実行
$ sudo ./configure --enable-static --enable-shared
$ sudo make
$ sudo make install

### 確認
$ which x264
/usr/local/bin/x264

$ x264 --version
x264 0.161.x
built on Feb  4 2021, gcc: 9.3.0
x264 configuration: --chroma-format=all
libx264 configuration: --chroma-format=all
x264 license: GPL version 2 or later
```

## 🔨 x265
```
### インストール
$ git clone https://github.com/videolan/x265.git
$ cd x265

### 実行
$ cd build/linux
$ sudo ./make-Makefiles.bash
   >> qを押す（変更無し）
$ sudo make
$ sudo make install

### 確認
$ which x265
/usr/local/bin/x265

$ x265 --version
x265 [info]: HEVC encoder version 3.4+28-419182243
x265 [info]: build info [Linux][GCC 9.3.0][64 bit] 8bit
x265 [info]: using cpu capabilities: MMX2 SSE2Fast LZCNT SSSE3 SSE4.2 AVX FMA3 BMI2 AVX2
```

## 🔨 fdk-aac
```
### インストール
$ sudo wget https://sourceforge.net/projects/opencore-amr/files/fdk-aac/fdk-aac-0.1.5.tar.gz
$ tar xzvf fdk-aac-0.1.5.tar.gz 
$ cd fdk-aac-0.1.5

### 実行
$ sudo ./configure
$ sudo make
$ sudo make install
```

## 🔨 opus codec
```
### インストール
$ sudo wget https://archive.mozilla.org/pub/opus/opus-1.3.1.tar.gz
$ tar xzvf opus-1.3.1.tar.gz
$ cd opus-1.3.1

### 実行
$ sudo ./configure
$ sudo make
$ sudo make install
```

## 🔨 ALSA
```
### インストール
$ sudo apt-get install libasound2-dev
$ cd /usr/src
$ sudo git clone git://source.ffmpeg.org/ffmpeg.git
$ cd ffmpeg/

### 実行
$ sudo ./configure && sudo make && sudo make install

### 確認
$ which alsa
/usr/sbin/alsa

$ alsa --version
Usage: /sbin/alsa {unload|reload|force-unload|force-reload|suspend|resume}
```

## 🔨 FFmpeg
```
### インストール
$ sudo apt install ffmpeg
$ cd $HOME
$ mkdir git
$ cd git
$ git clone https://github.com/FFmpeg/FFmpeg.git
$ cd FFmpeg
$ sudo apt-get -y install build-essential automake libsodium-dev libsodium uuid uuid-dev libssl-dev
$ sudo apt-get -y install autoconf automake build-essential cmake git libass-dev libfreetype6-dev libgpac-dev libsdl1.2-dev libtheora-dev libtool libva-dev libvdpau-dev libvorbis-dev libxcb1-dev libxcb-shm0-dev libxcb-xfixes0-dev mercurial pkg-config texi2html zlib1g-dev

### パスの設定
$ PKG_CONFIG_PATH=/opt/intel/mediasdk/lib/pkgconfig ./configure --prefix=/usr/local/ffmpeg --extra-cflags="-I/opt/intel/mediasdk/include" --extra-ldflags="-L/opt/intel/mediasdk/lib" --extra-ldflags="-L/opt/intel/mediasdk/plugins" --enable-vaapi --disable-debug --enable-libvorbis --enable-libvpx  --enable-gpl --cpu=native --enable-libfdk-aac --enable-libx264 --enable-libx265 --extra-libs=-lpthread --enable-nonfree

### 確認
$ sudo /usr/local/ffmpeg/bin/ffmpeg
$ sudo /usr/local/ffmpeg/bin/ffmpeg -encoders

### 実行
$ cd /usr/local/ffmpeg/bin
$ sudo make
$ sudo make install

### 確認
$ which ffmpeg
/home/ren/bin/ffmpeg

$ ffmpeg -version
ffmpeg version N-100946-ge6254d5 Copyright (c) 2000-2021 the FFmpeg developers
built with gcc 9 (Ubuntu 9.3.0-17ubuntu1~20.04)
configuration: --prefix=/home/ren/ffmpeg_build --pkg-config-flags=--static --extra-cflags=-I/home/ren/ffmpeg_build/include --extra-ldflags=-L/home/ren/ffmpeg_build/lib --extra-libs='-lpthread -lm' --bindir=/home/ren/bin --enable-gpl --enable-libass --enable-libfdk-aac --enable-libfreetype --enable-libmp3lame --enable-libopus --enable-libtheora --enable-libvorbis --enable-libvpx --enable-libx264 --enable-libx265 --enable-nonfree
libavutil      56. 64.100 / 56. 64.100
libavcodec     58.120.100 / 58.120.100
libavformat    58. 65.101 / 58. 65.101
libavdevice    58. 11.103 / 58. 11.103
libavfilter     7.102.100 /  7.102.100
libswscale      5.  8.100 /  5.  8.100
libswresample   3.  8.100 /  3.  8.100
libpostproc    55.  8.100 / 55.  8.100
```

## 🔨 livav
```
### インストール
$ sudo git clone git://git.libav.org/libav.git
$ cd libav/

### 実行
$ sudo ./configure --enable-gpl --enable-nonfree --enable-libx264 --enable-libx265 --enable-libfdk-aac
$ sudo make
$ sudo make install
```

## 🚀 Running
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
- __ffmpeg__
  ```
  $ sudo ffmpeg -s 960x540 -i /dev/video0 -f alsa -ac 2 -i hw:1,0 -acodec aac -ab 128k -ar 44100 -vcodec libx264 -f mpegts udp://[配信先アドレス]:[配信先ポート]
  ```
  ```
  $ cd /usr/local/ffmpeg/bin
  $ sudo ffmpeg -s 960x540 -i /dev/video0 -f alsa -i hw:0,0 -vcodec h264 -qmin 1 -qmax 3 -qdiff 8 -i_qfactor 1.40 -qcomp 0.7 -f mpegts udp://[配信先アドレス]:[配信先ポート]
  ```
- __ffplay__ 
  ```
  $ ffplay -fflags nobuffer udp://[配信元アドレス]:[配信元ポート]
  ```