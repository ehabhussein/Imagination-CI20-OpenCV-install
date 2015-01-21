# Imagination-CI20-OpenCV-install: C++ & no python support
Out of the Box the default debian image doesnt support webcams thus no /dev/video0

To get webcam support:

1- Download http://mipscreator.imgtec.com/CI20/images/default_NAND/Debian7_20150115/debian7_2015_01_15.img

2- Follow instructions : http://elinux.org/CI20_Dev_Zone#NAND_Flashing_SD_card
  a- switch the jumper on the board to short pins 2,3
  
  b- power on , led: from red -> Blue -> Red, power off ; remove SD card change back the jumper to short pins 1,2
  
  c- power on

3- prepare you debian image
  a- dpkg-reconfigure locales ; add en_US.utf8 remove others ; add to .bashrc ->
    a.1 export LC_ALL=en_US.utf8
        export LANGUAGE=en_US.utf8
    
  b- sudo apt-get install -y build-essential cmake pkg-config libpng12-0 libpng12-dev libpng++-dev libpng3 libpnglite-dev zlib1g-dbg zlib1g zlib1g-dev pngtools libtiff4-dev libtiff4 libtiffxx0c2 libtiff-tools libjpeg8 libjpeg8-dev libjpeg8-dbg libjpeg-progs ffmpeg libavcodec-dev libavcodec53 libavformat53 libavformat-dev libgstreamer0.10-0-dbg libgstreamer0.10-0  libgstreamer0.10-dev libxine1-ffmpeg  libxine-dev libxine1-bin libunicap2 libunicap2-dev libdc1394-22-dev libdc1394-22 libdc1394-utils swig libv4l-0 libv4l-dev libgtk2.0-dev pkg-config libogg-dev libopencore-amrnb-dev libopencore-amrnb0 libopencore-amrwb-dev libopencore-amrwb0 libswscale-dev libtheora-dev libvorbis-dev libx264-dev libxvidcore-dev yasm libeigen3-dev unzip libqt4-dev libqt4-opengl-dev vim screen libgstreamer-plugins-base0.10-dev libgstreamer-plugins-base0.10-0
  
4- download OpenCV from http://opencv.org/downloads.html
  a- unzip the archive
  
  b- cd opencv<version> ; mkdir release ; cd release
  
  c- cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_OPENGL=ON -DWITH_XINE=ON -D WITH_V4L=ON -D WITH_GSTREAMER=ON -D WITH_OPENEXR=ON -D WITH_UNICAP=ON -D INSTALL_C_EXAMPLES=ON -D BUILD_EXAMPLES=ON ..
  
    c.1- If you want QT instead of GTK
      c.1.1- -D WITH_QT=ON
  
  d- make -j4
  
  e-  go for a long break
  
  f- sudo make install
  
  g- vim /etc/ld.so.conf.d/opencv.conf
    g.1- /usr/local/lib
    g.2- save and exit ":wq"
    g.3- sudo ldconfig
    
