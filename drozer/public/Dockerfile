FROM ubuntu:14.04
MAINTAINER Huang Xiaofang 

# Set up insecure default key
RUN mkdir -m 0750 /.android

# Note: ADB needs 32-bit libs
RUN export DEBIAN_FRONTEND=noninteractive && \
    dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get -y install libc6:i386 libstdc++6:i386 && \
    apt-get -y install wget unzip openjdk-6-jre-headless && \
    wget --progress=dot:giga -O /opt/adt.tgz \
      https://dl.google.com/android/android-sdk_r24.0.2-linux.tgz && \
    tar xzf /opt/adt.tgz -C /opt && \
    rm /opt/adt.tgz && \
    echo y | /opt/android-sdk-linux/tools/android update sdk --filter platform-tools --no-ui --force && \
    apt-get clean && \
    rm -rf /var/cache/apt/*

# Set up PATH
ENV PATH $PATH:/opt/android-sdk-linux/platform-tools:/opt/android-sdk-linux/tools

# for base ubuntu
RUN apt-get -y install usbutils
RUN apt-get -y install android-tools-adb
RUN apt-get -y install vim

# for drozer
WORKDIR /etc/apt
RUN echo "deb http://us.archive.ubuntu.com/ubuntu/ trusty main restricted" >> sources.list && \
    echo "deb-src http://us.archive.ubuntu.com/ubuntu/ trusty main restricted" >> sources.list && \
    echo "deb http://us.archive.ubuntu.com/ubuntu/ trusty-updates main restricted" >> sources.list && \
    echo "deb-src http://us.archive.ubuntu.com/ubuntu/ trusty-updates main restricted" >> sources.list && \
    echo "deb http://us.archive.ubuntu.com/ubuntu/ trusty universe" >> sources.list && \
    echo "deb-src http://us.archive.ubuntu.com/ubuntu/ trusty universe" >> sources.list && \
    echo "deb http://us.archive.ubuntu.com/ubuntu/ trusty-updates universe" >> sources.list && \
    echo "deb http://us.archive.ubuntu.com/ubuntu/ trusty multiverse" >> sources.list && \
    echo "deb-src http://us.archive.ubuntu.com/ubuntu/ trusty multiverse" >> sources.list && \
    echo "deb http://us.archive.ubuntu.com/ubuntu/ trusty-updates multiverse" >> sources.list && \
    echo "deb-src http://us.archive.ubuntu.com/ubuntu/ trusty-updates multiverse" >> sources.list && \
    echo "deb http://us.archive.ubuntu.com/ubuntu/ trusty-backports main restricted universe multiverse" >> sources.list && \
    echo "deb-src http://us.archive.ubuntu.com/ubuntu/ trusty-backports main restricted universe multiverse" >> sources.list

RUN apt-get update
RUN apt-get -y install openjdk-6-jdk

RUN apt-get -y install python-setuptools
RUN easy_install --allow-hosts pypi.python.org protobuf==2.4.1
RUN apt-get -y install python-openssl
RUN apt-get -y install python-dev
RUN easy_install twisted==10.2.0

# download drozer project
RUN apt-get -y install git
WORKDIR /home
RUN git clone git://github.com/apksec2015/apksec
