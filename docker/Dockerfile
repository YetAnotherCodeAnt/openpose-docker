FROM nvidia/cuda:11.7.1-devel-ubuntu20.04

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -qq install -y \
        libatlas-base-dev libprotobuf-dev libleveldb-dev \
        libsnappy-dev libhdf5-serial-dev protobuf-compiler \
        libgflags-dev libgoogle-glog-dev liblmdb-dev \
        opencl-headers ocl-icd-opencl-dev libviennacl-dev \
        cmake libboost-all-dev libopencv-dev ffmpeg git git-lfs

RUN git clone --depth=1 https://github.com/AlecDusheck/openpose.git
COPY pose_iter_102000.caffemodel openpose/models/hand/pose_iter_102000.caffemodel
COPY pose_iter_584000.caffemodel openpose/models/pose/body_25/pose_iter_584000.caffemodel
COPY pose_iter_116000.caffemodel openpose/models/face/pose_iter_116000.caffemodel

RUN cd openpose && rm -rf build || true && mkdir build && cd build && cmake -DGPU_MODE=CPU_ONLY .. && make -j`nproc`
