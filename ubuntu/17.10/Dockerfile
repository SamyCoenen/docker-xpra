# This Dockerfile builds a base-image with xpra

FROM ubuntu:17.10

MAINTAINER Samy Coenen "contact@samycoenen.be"

ENV DISPLAY=:100 XDG_RUNTIME_DIR=/tmp/ DBUS_SYSTEM_BUS_ADDRESS='unix:path=/host/run/dbus/system_bus_socket' XPRA_USER=web DEBIAN_FRONTEND=noninteractive

# Add the winswitch/xpra remote source to be able to obtain the latest xpra
RUN apt-get update && apt-get install -y curl \
    && curl https://winswitch.org/gpg.asc | apt-key add - \
    && echo "deb http://winswitch.org/ artful main" > /etc/apt/sources.list.d/winswitch.list
    
# packages for xorg and xpra
# https://www.xpra.org/trac/wiki/Dependencies
RUN apt-get update && apt-get install -y \
        software-properties-common \
        python-netifaces \
        python-lz4 \
        python-numpy \
        python-gst-1.0 \
        xserver-xorg-input-kbd \
        xserver-xorg-input-mouse \
        xserver-xorg-input-libinput \
        xserver-xephyr \
        xpra \
        xvfb \
        websockify \
        openssh-server