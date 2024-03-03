FROM python:3.9.18-slim-bullseye

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=${USER_UID}

LABEL maintainer "Raphael Lekies <raphael.lekies@it4smart.com> (IT4smart GmbH)"

COPY requirements.txt /tmp/requirements.txt

RUN apt-get update -qq \
    && apt-get install -y --no-install-recommends \
        unzip \
        jq \
        git \
        sshpass \
        openssh-client \
    && apt-get autoremove --purge -y \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/* \
    && groupadd --gid ${USER_GID} ${USERNAME} \
    && useradd --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} -s /bin/bash \
    && pip install --upgrade pip setuptools \
    && pip install -r /tmp/requirements.txt

USER ${USERNAME}

COPY --chown=${USERNAME}:${USERNAME} files/post-start.sh /home/${USERNAME}/post-start.sh

RUN mkdir ~/.ssh