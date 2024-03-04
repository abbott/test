# syntax=docker/dockerfile:1.6.0

FROM debian:bullseye-slim

ARG DEBIAN_FRONTEND=noninteractive
ARG USER=nonroot
ARG UID=1000
ARG GID=1000

ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8 \
    NVIDIA_VISIBLE_DEVICES=all \
    NVIDIA_DRIVER_CAPABILITIES=compute,utility \
    TZ=America/New_York \
    PYTHONUNBUFFERED=1

RUN apt-get update --fix-missing \
    && apt-get install --no-install-recommends --yes \
      apt-utils \
      aria2 \
      bash-completion \
      curl \
      dnsutils \
      dstat \
      ffmpeg \
      file \
      git \
      htop \
      iproute2 \
      nano \
      net-tools \
      pkg-config \
      procps \
      python3 \
      sudo \
      tmux \
      traceroute \
      tzdata \
      wget \
      zip \
    && apt-get autoremove --yes \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && addgroup --gid $GID $USER \
    && useradd \
      --create-home \
      --home-dir /home/$USER \
      --system \
      --uid $UID \
      --gid $GID \
      --groups sudo \
      --shell /bin/bash \
      $USER \
    && echo "$USER ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/$USER \
    && chmod 0440 /etc/sudoers.d/$USER \
    && chown -R $USER:$GID /home/$USER

ENV HOME=/home/$USER

USER $USER
WORKDIR $HOME