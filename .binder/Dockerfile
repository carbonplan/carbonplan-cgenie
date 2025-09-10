#TODO
FROM ghcr.io/astral-sh/uv:debian-slim


# This is meant to use repo2docker to build and publish a
# Docker image that can be used for our PMTiles generation
# It is published with the help of the repo2docker github action

USER root

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
  
&& rm -rf /var/lib/apt/lists/*


WORKDIR /tmp 



RUN wget https://downloads.unidata.ucar.edu/netcdf-c/4.9.2/netcdf-c-4.9.2.tar.gz  \
    && tar xzf netcdf-c-4.9.2.tar.gz \
    && cd netcdf-c-4.9.2 \
    && export LDFLAGS="-L/usr/lib/x86_64-linux-gnu/hdf5/serial/lib" \
    && export export CFLAGS="-I/usr/lib/x86_64-linux-gnu/hdf5/serial/include" \
    && ./configure \
    && make check \
    && make install 



# # install tippecanoe
# WORKDIR /tmp
# RUN git clone https://github.com/felt/tippecanoe.git /tmp/tippecanoe-src
# WORKDIR /tmp/tippecanoe-src
# RUN make

# # move tippecanoe
# WORKDIR /tmp/tippecanoe-src
# RUN cp tippecanoe /usr/local/bin/
# RUN cp tile-join /usr/local/bin/


# # Download and install the pre-built s5cmd binary
# WORKDIR /tmp
# RUN curl -L https://github.com/peak/s5cmd/releases/download/v2.3.0/s5cmd_2.3.0_Linux-64bit.tar.gz -o /tmp/s5cmd.tar.gz \
#     && tar -xvzf /tmp/s5cmd.tar.gz -C /usr/local/bin/ \
#     && rm /tmp/s5cmd.tar.gz

# # Install duckdb
# RUN curl -L https://github.com/duckdb/duckdb/releases/download/v1.3.2/duckdb_cli-linux-amd64.zip -o duckdb_cli-linux.zip && unzip duckdb_cli-linux.zip -d /usr/local/bin/ && rm duckdb_cli-linux.zip

# RUN duckdb -c "install httpfs; install spatial;"

# # install gpq
# RUN curl -L https://github.com/planetlabs/gpq/releases/download/v0.24.0/gpq-linux-amd64.tar.gz -o /tmp/gpq.tar.gz \
#     && tar -xvzf /tmp/gpq.tar.gz -C /usr/local/bin/ \
#     && rm /tmp/gpq.tar.gz


WORKDIR /app
