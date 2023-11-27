ARG UBUNTU_VERSION_NAME=latest

FROM ubuntu:${UBUNTU_VERSION_NAME}

# Your Property
ARG USER=user
ARG USER_ID=1000
ARG GROUP_ID=1000
ARG DOTNET_VERSION=8.0

RUN apt-get update && apt-get install -y --no-install-recommends sudo curl dotnet-sdk-${DOTNET_VERSION} \
    && apt-get clean && rm -rf /var/lib/apt/lists/* \
    && groupadd -g ${GROUP_ID} ${USER} \
    && useradd -u ${USER_ID} -m -s /bin/bash -g ${USER} -G sudo ${USER} \
    && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER ${USER}

ENV PATH=/home/${USER}/.dotnet/tools:$PATH

# TMP Docker Volume
VOLUME ["/WORKDIR"]

WORKDIR /WORKDIR