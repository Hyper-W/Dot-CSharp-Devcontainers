ARG DEBIAN_VERSION_NAME=stable

FROM debian:${DEBIAN_VERSION_NAME}-slim

# Your Property
ARG USER=user
ARG USER_ID=1000
ARG GROUP_ID=1000
ARG DOTNET_VERSION=8.0

RUN apt-get update && apt-get install -y --no-install-recommends sudo curl wget ca-certificates apt-transport-https \
    && wget https://packages.microsoft.com/config/debian/`cut -f 1 -d '.' /etc/debian_version`/packages-microsoft-prod.deb -O packages-microsoft-prod.deb \
    && apt-get install -y --no-install-recommends ./packages-microsoft-prod.deb && rm packages-microsoft-prod.deb \
    && apt-get update && apt-get install -y --no-install-recommends dotnet-sdk-${DOTNET_VERSION} \
    && apt-get remove -y --autoremove --purge wget && apt-get clean && rm -rf /var/lib/apt/lists/* \
    && groupadd -g "${GROUP_ID}" "${USER}" \
    && useradd -u "${USER_ID}" -m -s /bin/bash -g "${USER}" -G sudo "${USER}" \
    && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER ${USER}

ENV PATH=/home/${USER}/.dotnet/tools:$PATH

# TMP Docker Volume
VOLUME ["/WORKDIR"]

WORKDIR /WORKDIR