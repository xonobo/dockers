FROM ubuntu:16.04

RUN mkdir /etc/sudoers.d
# Replace 1000 with your user / group id
RUN export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer

RUN apt-get update
RUN apt-get install -y software-properties-common
RUN apt-get install -y python-software-properties debconf-utils
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN apt-get install -y oracle-java9-installer
RUN apt-get install -y oracle-java9-set-default






USER developer
ENV HOME /home/developer
CMD bash


#docker run -ti --rm \
#       -e DISPLAY=$DISPLAY \
#       -v /tmp/.X11-unix:/tmp/.X11-unix \
#       x-dev
