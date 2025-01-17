FROM nvidia/cuda:12.3.1-base-ubuntu22.04

ENV PATH="/home/erwan/.local/bin:${PATH}"

ENV TZ=Europe/London
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install packages
RUN apt-get update && apt-get install -y \
   build-essential \
   libffi-dev \
   libgdbm-dev \
   libc6-dev \
   libssl-dev \
   zlib1g-dev \
   libbz2-dev \
   libreadline-dev \
   libsqlite3-dev \
   libncurses5-dev \
   libncursesw5-dev \
   xz-utils \
   tk-dev \
   libxml2-dev \
   libxmlsec1-dev \
   liblzma-dev \
   wget \
   netcdf-bin

# Download and install Python 3.11.8 from source
ENV PYTHON_VERSION=3.11.8
RUN wget https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tar.xz && \
   tar -xf Python-$PYTHON_VERSION.tar.xz && \
   cd Python-$PYTHON_VERSION && \
   ./configure --enable-optimizations && \
   make -j 8 && \
   make altinstall && \
   cd ..

# Remove the Python tarball to reduce image size
RUN rm Python-$PYTHON_VERSION.tar.xz && \
   rm -rf Python-$PYTHON_VERSION

# Set Python 3.11.8 as the default python
RUN update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.11 1

# # Upgrade pip
RUN python3.11 -m pip install --upgrade pip

# # Create symlink for pip
# RUN ln -s /usr/local/bin/pip3.11 /usr/local/bin/pip

RUN python3.11 -m pip install torch torchvision torchaudio


RUN apt-get update && \
    apt-get -y install ncl-ncarg && \
    apt-get -y install cdo && \
    apt-get -y install vim
    
RUN python3.11 -m pip install numpy pandas xarray netcdf4 matplotlib seaborn scikit-learn scipy Pyarrow notebook ipython cartopy xee seaborn google ee netCDF4 zarr xclim

RUN apt-get update && apt-get install -y sudo

RUN python3.11 -m pip install xmip

RUN python3.11 -m pip install earthengine-api --upgrade && python3.11 -m pip install -U tensorboard

# RUN python3.11 -m pip install neuralhydrology

