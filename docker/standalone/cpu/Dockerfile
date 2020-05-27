FROM ubuntu:16.04
MAINTAINER caffe-maint@googlegroups.com
# ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive

RUN sed -i s@/archive.ubuntu.com/@/mirrors.tencent.com/@g /etc/apt/sources.list
RUN sed -i s@/security.ubuntu.com/@/mirrors.tencent.com/@g /etc/apt/sources.list

RUN rm -Rf /var/lib/apt/lists/* && apt-get -y update && apt-get install -y fortunes

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        wget \
        libatlas-base-dev \
        libboost-all-dev \
        libgflags-dev \
        libgoogle-glog-dev \
        libhdf5-serial-dev \
        libleveldb-dev \
        liblmdb-dev \
        libopencv-dev \
        libprotobuf-dev \
        libsnappy-dev \
        protobuf-compiler \
        python3 \
        python3-dev \
        python3-numpy \
        python3-pip \
        python3-setuptools \
        python3-scipy && \
        rm -rf /var/lib/apt/lists/*
RUN mkdir -p  /root/.pip && echo "[global]\n index-url = https://mirrors.tencent.com/pypi/simple/" >> /root/.pip/pip.conf && python3 -m pip install --upgrade pip

ENV CAFFE_ROOT=/opt/caffe
WORKDIR $CAFFE_ROOT

# FIXME: clone a specific git tag and use ARG instead of ENV once DockerHub supports this.
ENV CLONE_TAG=ssd

RUN git clone -b ${CLONE_TAG} --depth 1 https://github.com/gttiankai/caffe.git . && \
    for req in $(cat python/requirements.txt) pydot; do pip3 install $req; done
#     mkdir build && cd build && \
#     cmake -DCPU_ONLY=1 .. && \
#     make -j"$(nproc)"

# ENV PYCAFFE_ROOT $CAFFE_ROOT/python
# ENV PYTHONPATH $PYCAFFE_ROOT:$PYTHONPATH
# ENV PATH $CAFFE_ROOT/build/tools:$PYCAFFE_ROOT:$PATH
# RUN echo "$CAFFE_ROOT/build/lib" >> /etc/ld.so.conf.d/caffe.conf && ldconfig

WORKDIR /workspace
