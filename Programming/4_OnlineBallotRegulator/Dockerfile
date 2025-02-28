##################################################
# 
# Dockerfile to build the Application Server
# Based on: Python 3.4
# 
##################################################

# Set the base image to ubuntu
FROM ubuntu:bionic

# Do not buffer the output from stdout.
ENV PYTHONUNBUFFERED 1
ENV DEBIAN_FRONTEND noninteractive

# Set the working directory.
WORKDIR /usr/src/onlineballotregulator/

# Copy our python server over.
COPY . /usr/src/onlineballotregulator/


RUN apt-get update && \
    apt-get install -y \
        apt-utils \
        software-properties-common 

RUN     add-apt-repository ppa:jonathonf/python-3.6 && \
        apt-get install -y build-essential python3.6 python3.6-dev python3-pip && \
        # update pip
        python3.6 -m pip install pip --upgrade && \
        python3.6 -m pip install wheel

RUN add-apt-repository -y ppa:ethereum/ethereum

# Install our dependencies
RUN apt-get update && \
    apt-get install -y \
#        python3 \
        libpq-dev \
        libffi-dev \
        libssl-dev \
        libyaml-dev \
        postgresql \
        golang \
        git \
        make \
        gcc \
        libc-dev \
        ca-certificates \
        ethereum \
        solc

#RUN git clone --depth 1 https://github.com/ethereum/go-ethereum /usr/src/onlineballotregulator/go-ethereum

# Install our server via pip
RUN pip3 install .

# Expose our ports
EXPOSE 5434 8545 30303

# Run load our entrypoint
ENTRYPOINT [ "./bin/docker_entrypoint" ]
