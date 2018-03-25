# This Dockerfile builds an image with which you can remotely control any application using xpra

FROM samyco/docker-xpra:debian-stretch

MAINTAINER Samy Coenen "contact@samycoenen.be"

RUN apt-get update && apt-get install -y \
        chromium && \
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/*

# Add user 
RUN  adduser --disabled-password --gecos "User" --uid 1000 $XPRA_USER 

USER $XPRA_USER

EXPOSE 14500

CMD rm -f /tmp/.X100-lock && XPRA_PASSWORD=$(tr -dc _A-Z-a-z-0-9 < /dev/urandom | head -c 8) && echo "xpra password is: "$XPRA_PASSWORD && xpra start $DISPLAY --tcp-auth=password:value=$XPRA_PASSWORD --bind-tcp=0.0.0.0:14500  --start='chromium  --no-sandbox' && sleep infinity