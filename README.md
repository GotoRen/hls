# HTTP Live Streaming Configuration
## 🌱 Environment
- Ubuntu Linux 20.04 LTS
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

## 🔨 v4l-utils
```
$ sudo apt-get install v4l-utils
$ v4l2-ctl --list-devices
$ v4l2-ctl -d /dev/video0 --all
$ v4l2-ctl -d /dev/video0 --list-formats-ext
```

## 🔨 NASM
```
$ sudo wget https://www.nasm.us/pub/nasm/stable/nasm-2.15.05.tar.bz2
$ tar xjvf nasm-2.15.05.tar.bz2 
$ cd nasm-2.15.05/
$ ./configure
$ make
$ sudo make install
```

## 🔨 YASM
```
$ sudo wget http://www.tortall.net/projects/yasm/releases/yasm-1.3.0.tar.gz
$ sudo tar xvf yasm-1.3.0.tar.gz 
$ cd yasm-1.3.0/
$ ./configure
```

## 🔨 g++ , ccmake
```
$ sudo apt-get install g++ cmake-curses-gui
```

## 🔨 x264
```
$ sudo wget https://code.videolan.org/videolan/x264/-/archive/master/x264-master.tar.bz2
$ tar xjvf x264-master.tar.bz2
$ cd x264-master/
$ ./configure --enable-static --enable-shared
$ make
$ sudo make install
$ sudo apt-get install x264
$ sudo apt-get install libx264-dev
```

## 🔨 x265
```
$ git clone https://github.com/videolan/x265.git
$ cd x265
$ cd build/linux
$ ./make-Makefiles.bash
   >> qを押す（変更無し）
$ make
$ sudo make install
```
🔨
## 🔨 fdk-aac
```
$ sudo wget https://sourceforge.net/projects/opencore-amr/files/fdk-aac/fdk-aac-0.1.5.tar.gz
$ tar xzvf fdk-aac-0.1.5.tar.gz 
$ cd fdk-aac-0.1.5
$ ./configure
$ make
$ sudo make install
```

## 🔨 opus codec
```
$ sudo wget https://archive.mozilla.org/pub/opus/opus-1.3.1.tar.gz
$ ./configure
$ make
$ sudo make install
```

## 🔨 ALSA
```
$ sudo apt-get install libasound2-dev
$ cd /usr/src
$ sudo git clone git://source.ffmpeg.org/ffmpeg.git
$ cd ffmpeg/
$ sudo ./configure && sudo make && sudo make install
```

## 🔨 livav
```
$ sudo git clone git://git.libav.org/libav.git
$ cd libav/
$ ./configure --enable-gpl --enable-nonfree --enable-libx264 --enable-libx265 --enable-libfdk-aac
$ make
$ sudo make install
```

## 🚀 Running
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
```
$ sudo ffmpeg -s 960x540   -i /dev/video0   -f alsa   -ac 2   -i hw:1,0   -acodec aac   -ab 128k   -ar 44100   -s 960x540 -vcodec libx264 -f mpegts udp://10.0.1.139:50000
```
 