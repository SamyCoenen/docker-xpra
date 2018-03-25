# This Dockerfile builds a base-image with xpra

FROM alpine:3.7

MAINTAINER Samy Coenen "contact@samycoenen.be"

ENV DISPLAY=:100 XDG_RUNTIME_DIR=/tmp/ DBUS_SYSTEM_BUS_ADDRESS='unix:path=/host/run/dbus/system_bus_socket' XPRA_USER=web DEBIAN_FRONTEND=noninteractive

# packages for xorg and xpra
# https://www.xpra.org/trac/wiki/Dependencies
RUN apk add --no-cache \
        py3-netifaces \
        py3-lz4 \
        py3-numpy \
        py3-gst \
        xpra \
        xvfb \
        openssh-server