FROM ubuntu:latest

# Install necessary packages
RUN apt-get update && apt-get install -y python3 python3-pip python3.12-venv git wget build-essential

# Set up Python environment and install Python packages
RUN python3 -m venv /opt/venv
RUN /opt/venv/bin/pip install --no-cache-dir numpy pandas scikit-learn joblib
ENV PATH="/opt/venv/bin:$PATH"

# Install Boost
RUN wget https://archives.boost.io/release/1.86.0/source/boost_1_86_0.tar.gz && \
    tar -xvf boost_1_86_0.tar.gz && \
    mv boost_1_86_0 /opt/boost
ENV BOOST="/opt/boost"

# Install HTSLib with --prefix=/usr/local
RUN wget -L https://github.com/samtools/htslib/releases/download/1.21/htslib-1.21.tar.bz2 && \
    tar -xf htslib-1.21.tar.bz2 && \
    cd htslib-1.21 && \
    ./configure --prefix=/usr/local --disable-bz2 --disable-lzma --disable-gcs --disable-s3 --enable-libcurl=no && \
    make && \
    make install

# Set HTSLIB_ROOT and LD_LIBRARY_PATH to include /usr/local/lib
ENV HTSLIB="/usr/local"
ENV LD_LIBRARY_PATH="/usr/local/lib"

# Install Aletsch with Boost and HTSlib paths specified
RUN wget https://github.com/Shao-Group/aletsch/releases/download/v1.1.2/aletsch-1.1.2.tar.gz && \
    tar -xvf aletsch-1.1.2.tar.gz && \
    cd aletsch-1.1.2 && mkdir build && cd build && \
    ../configure --with-boost=$BOOST --with-htslib=$HTSLIB && \
    make && \
    cp aletsch /usr/local/bin/
