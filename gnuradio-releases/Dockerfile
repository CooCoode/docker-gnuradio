FROM ubuntu:22.04

# Use default Ubuntu sources, update, install all dependencies in one go, and clean up
RUN \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        software-properties-common \
        sudo \
        gpg \
        gpg-agent && \
    add-apt-repository -y ppa:gnuradio/gnuradio-releases && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        gnuradio \
        gnuradio-dev \
        gir1.2-gtk-3.0 \
        cmake \
        git \
        libboost-all-dev \
        libcppunit-dev \
        liblog4cpp5-dev \
        python3-pygccxml \
        pybind11-dev \
        liborc-dev \
        python3-pip \
        libgsl-dev \
        clang-format \
        vim && \
    rm -rf /var/lib/apt/lists/*

LABEL maintainer="Federico 'Larroca' La rocca - flarroca@fing.edu.uy"

ENV DEBIAN_FRONTEND=noninteractive

# create user gnuario with sudo (and password gnuradio)
RUN useradd --create-home --shell /bin/bash -G sudo gnuradio
RUN echo 'gnuradio:gnuradio' | chpasswd

# I create a dir at home which I'll use to persist after the container is closed (need to change it's ownership)
RUN mkdir /home/gnuradio/persistent  && chown gnuradio /home/gnuradio/persistent



# Fix dependency issue as noted on 'InstallingGR' wiki page for 3.10
RUN pip install packaging

USER gnuradio

WORKDIR /home/gnuradio

ENV PYTHONPATH "${PYTHONPATH}:/usr/local/lib/python3/dist-packages"

CMD bash
