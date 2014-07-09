FROM fedora:20
MAINTAINER Aquarius Interactive <m@aquariusinteractive.com>

WORKDIR /tmp

RUN rpm -Uvh  http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-20.noarch.rpm
RUN rpm -Uvh  http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-20.noarch.rpm
RUN rpm -Uvh http://rpms.famillecollet.com/remi-release-20.rpm

RUN yum -y install drpmsync deltarpam gem mm
RUN yum -y install libwebp-tools gstreamer-plugins-good gstreamer-plugins-bad gstreamer-plugins-ugly gstreamer gstreamer-rtsp gstreamer-ffmpeg gstreamer-tools
RUN yum -y install ffmpeg ffmpeg-libs ImageMagick mencoder oggconvert oggvideotools ogmtools gd-progs

RUN yum -y update
RUN gem install flvtool2

RUN yum clean all
