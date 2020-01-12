# We will use Ubunu for our image
FROM nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04

# Adding wget and bzip2
RUN apt-get update; apt-get install -y wget bzip2 sudo 

# Add user ubuntu with no password, add to sudo group
RUN adduser --disabled-password --gecos '' ubuntu
RUN adduser ubuntu sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER ubuntu
WORKDIR /home/ubuntu/
RUN chmod a+rwx /home/ubuntu/
#RUN echo `pwd`

# Anaconda installing
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN bash Miniconda3-latest-Linux-x86_64.sh -b
RUN rm Miniconda3-latest-Linux-x86_64.sh

# Set path to conda
ENV PATH /home/ubuntu/miniconda3/bin:$PATH

# Updating Anaconda packages
RUN conda update conda
RUN conda update --all
RUN conda install cmake gcc_linux-64 gxx_linux-64 gfortran_linux-64

RUN conda install pytorch torchvision cudatoolkit=10.1 -c pytorch

RUN conda install mkl-include libboost

RUN sudo apt-get install git -y; git clone https://github.com/opencv/opencv.git; \
    git clone https://github.com/opencv/opencv_contrib.git; cd opencv_contrib; git checkout 4.2.0; \
    cd ../opencv; git checkout 4.2.0




 
