FROM nvidia/cuda:12.1.0-cudnn8-devel-ubuntu20.04

ENV DEBIAN_FRONTEND=noninteractive

# System packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    software-properties-common \
    curl \
    gnupg2 \
    lsb-release \
    ca-certificates \
    build-essential \
    wget

# Add deadsnakes PPA and install Python 3.9
RUN add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
    python3.9 \
    python3.9-distutils \
    libpython3.9-dev \
    python3-pip

# Set python3 and python to Python 3.9
RUN ln -sf /usr/bin/python3.9 /usr/bin/python3 && \
    ln -sf /usr/bin/python3.9 /usr/bin/python

# Upgrade pip for Python 3.9 and install notebook
RUN python3 -m pip install --upgrade pip && \
    pip install notebook

# Verify installation
RUN python3 --version && pip --version

# Expose ports for notebook (8888) and other services (8000)
EXPOSE 8888
EXPOSE 8000

# Declare data mount
VOLUME ["/data"]

# Default shell
SHELL ["/bin/bash", "-c"]

# Start in bash by default
CMD ["/bin/bash"]