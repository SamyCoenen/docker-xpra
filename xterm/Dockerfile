# This Dockerfile builds an image with which you can remotely control any application using xpra

FROM samyco/xpra:ubuntu17.10-tcp

MAINTAINER Samy Coenen "contact@samycoenen.be"

ENV DISPLAY :100 
ENV XDG_RUNTIME_DIR /tmp/ 
ENV DBUS_SYSTEM_BUS_ADDRESS unix:path=/host/run/dbus/system_bus_socket
ENV XPRA_USER web

# Add the winswitch/xpra remote source to be able to obtain the latest xpra
RUN apt-get update && apt-get install -y curl \
    && curl https://winswitch.org/gpg.asc | apt-key add - \
    && echo "deb http://winswitch.org/ artful main" > /etc/apt/sources.list.d/winswitch.list
    
# All packages required by xorg and xpra and java
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
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
        xterm && \
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/*

# Add user 
RUN  adduser --disabled-password --gecos "User" --uid 1000 $XPRA_USER 

USER $XPRA_USER

EXPOSE 14500

CMD rm -f /tmp/.X100-lock && XPRA_PASSWORD=$(tr -dc _A-Z-a-z-0-9 < /dev/urandom | head -c 8) && echo "xpra password is: "$XPRA_PASSWORD && xpra start $DISPLAY --tcp-auth=password:value=$XPRA_PASSWORD --bind-tcp=0.0.0.0:14500  --start='xterm' && sleep infinity