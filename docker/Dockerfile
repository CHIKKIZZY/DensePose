  GNU nano 2.9.3                                                                                                 docker/Dockerfile                                                                                                           
# Use PyTorch image with Caffe2 as parent image
#FROM pytorch/pytorch:nightly-devel-cuda9.2-cudnn7
FROM caffe2/caffe2:snapshot-py2-cuda9.0-cudnn7-ubuntu16.04

RUN mv /usr/local/caffe2 /usr/local/caffe2_build
ENV Caffe2_DIR /usr/local/caffe2_build
#ENV PYTORCH_DIR /usr/local

ENV PYTHONPATH /usr/local/caffe2_build:${PYTHONPATH}
ENV LD_LIBRARY_PATH /usr/local/caffe2_build/lib:${LD_LIBRARY_PATH}
#ENV PYTHONPATH /usr/local:${PYTHONPATH}
#ENV LD_LIBRARY_PATH /usr/local/lib:${LD_LIBRARY_PATH}

# Clone the Detectron repository
#RUN git clone https://github.com/facebookresearch/Detectron /detectron
RUN git clone https://github.com/CHIKKIZZY/DensePose /densepose

# Upgrade pip
#RUN pip install --upgrade pip

# For opencv
RUN apt-get update
RUN apt-get install -y libsm6 libxext6 libgtk2.0-dev libxrender-dev

# Install needed libraries for Detectron & Caffe2
RUN pip install protobuf
RUN pip install future
RUN pip install six

# Install Python dependencies
RUN pip install -r /densepose/requirements.txt

# Install Detectron
#WORKDIR /detectron
#RUN make

# Install DensePose
#WORKDIR /densepose
#RUN make

# Install the COCO API
RUN git clone https://github.com/cocodataset/cocoapi.git /cocoapi
WORKDIR /cocoapi/PythonAPI
RUN make install

# Install Detectron
#WORKDIR /detectron
#RUN make

# Go to Densepose root
WORKDIR /densepose
# Set up Python modules
RUN make

# [Optional] Build custom ops
RUN make ops
