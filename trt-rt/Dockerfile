FROM nvcr.io/nvidia/cuda:11.5.0-runtime-ubuntu18.04

RUN apt update && \
    apt install wget -y

# TensorRT
RUN mkdir /tmp/tensorrt && \
    cd /tmp/tensorrt && \
    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/libcudnn8_8.3.2.44-1+cuda11.5_amd64.deb && \
    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/libnvinfer8_8.2.3-1+cuda11.4_amd64.deb && \
    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/libnvinfer-plugin8_8.2.3-1+cuda11.4_amd64.deb && \
    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/libnvonnxparsers8_8.2.3-1+cuda11.4_amd64.deb && \
    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/libnvparsers8_8.2.3-1+cuda11.4_amd64.deb && \
    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/./python3-libnvinfer_8.2.3-1+cuda11.4_amd64.deb

#RUN cd /tmp/tensorrt && \
#    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/libcudnn8-dev_8.3.2.44-1+cuda11.5_amd64.deb && \
#    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/libnvinfer-dev_8.2.3-1+cuda11.4_amd64.deb && \
#    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/libnvinfer-plugin-dev_8.2.3-1+cuda11.4_amd64.deb && \
#    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/libnvonnxparsers-dev_8.2.3-1+cuda11.4_amd64.deb && \
#    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/libnvparsers-dev_8.2.3-1+cuda11.4_amd64.deb && \
#    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/python3-libnvinfer-dev_8.2.3-1+cuda11.4_amd64.deb


RUN cd /tmp/tensorrt && \
    apt install python3 -y && \
    dpkg -i *.deb && \
    rm -rf /tmp/tensorrt

# Video Codec SDK
ENV VIDEOSDK_VERSION 11.1.5
ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs${LIBRARY_PATH:+:${LIBRARY_PATH}}
ENV NVIDIA_DRIVER_CAPABILITIES ${NVIDIA_DRIVER_CAPABILITIES},video

WORKDIR /opt/nvidia/video-sdk
COPY Video_Codec_SDK_${VIDEOSDK_VERSION}.zip /opt/nvidia/video-sdk

RUN apt install -y unzip && \
    unzip -j Video_Codec_SDK_${VIDEOSDK_VERSION}.zip \
          Video_Codec_SDK_${VIDEOSDK_VERSION}/Interface/cuviddec.h \
          Video_Codec_SDK_${VIDEOSDK_VERSION}/Interface/nvcuvid.h \
          Video_Codec_SDK_${VIDEOSDK_VERSION}/Interface/nvEncodeAPI.h \
          -d /usr/local/cuda/include && \
    unzip -j Video_Codec_SDK_${VIDEOSDK_VERSION}.zip \
          Video_Codec_SDK_${VIDEOSDK_VERSION}/Lib/linux/stubs/x86_64/libnvcuvid.so \
          Video_Codec_SDK_${VIDEOSDK_VERSION}/Lib/linux/stubs/x86_64/libnvidia-encode.so \
          -d /usr/local/cuda/lib64/stubs && \
    rm -rf /opt/nvidia/video-sdk
# pkg-config files
COPY usr /usr


RUN rm -rf /var/lib/apt/lists/*





