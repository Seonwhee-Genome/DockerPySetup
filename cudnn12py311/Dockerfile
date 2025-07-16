FROM nvidia/cuda:12.1.0-cudnn8-devel-ubuntu20.04

ENV DEBIAN_FRONTEND=noninteractive

# System dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    software-properties-common \
    curl \
    gnupg2 \
    lsb-release \
    ca-certificates \
    build-essential \
    wget

# Add Python 3.11
RUN add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
    python3.11 \
    python3.11-distutils \
    libpython3.11-dev

# Point python3 and python to python3.11
RUN ln -sf /usr/bin/python3.11 /usr/bin/python3 && \
    ln -sf /usr/bin/python3.11 /usr/bin/python

# Copy get-pip.py from mounted volume (/data)
COPY get-pip.py /tmp/get-pip.py

# Install pip using the copied script
RUN python3 /tmp/get-pip.py && \
    ln -sf /usr/local/bin/pip3 /usr/bin/pip && \
    ln -sf /usr/local/bin/pip3 /usr/bin/pip3

# Optional: verify versions
RUN python3 --version && pip --version

# Set shell
SHELL ["/bin/bash", "-c"]

# Ports and volume
EXPOSE 8888
EXPOSE 6666
VOLUME ["/data"]

CMD ["/bin/bash"]
