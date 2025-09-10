FROM ghcr.io/astral-sh/uv:debian-slim

USER root

# Install system dependencies
RUN apt-get update \
    && apt-get -y install \
        make \
        gfortran \
        xsltproc \
        libxml2-dev \
        m4 \
        libcurl4-openssl-dev \
        libz-dev \
        libhdf5-dev \
        curl \
        git \
        wget \
        build-essential \
    && rm -rf /var/lib/apt/lists/*

# NetCDF C libs
WORKDIR /tmp
RUN wget https://downloads.unidata.ucar.edu/netcdf-c/4.9.2/netcdf-c-4.9.2.tar.gz \
    && tar xzf netcdf-c-4.9.2.tar.gz \
    && cd netcdf-c-4.9.2 \
    && export LDFLAGS="-L/usr/lib/x86_64-linux-gnu/hdf5/serial/lib" \
    && export CFLAGS="-I/usr/lib/x86_64-linux-gnu/hdf5/serial/include" \
    && ./configure \
    && make install \
    && ldconfig
WORKDIR /tmp
RUN rm -rf netcdf-c-4.9.2*

# fortran stuff
RUN wget https://downloads.unidata.ucar.edu/netcdf-fortran/4.6.1/netcdf-fortran-4.6.1.tar.gz \
    && tar xzf netcdf-fortran-4.6.1.tar.gz \
    && cd netcdf-fortran-4.6.1 \
    && ./configure \
    && make install \
    && ldconfig
WORKDIR /tmp
RUN rm -rf netcdf-fortran-4.6.1*

# switch to workspace?
WORKDIR /workspace
