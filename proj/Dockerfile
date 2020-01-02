FROM continuumio/miniconda3:latest

RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y \
        libpq-dev \
        build-essential \
        git \
        sudo \
        cmake zlib1g-dev libjpeg-dev xvfb ffmpeg xorg-dev libboost-all-dev libsdl2-dev swig \
        unzip zip \
    && rm -rf /var/lib/apt/lists/*

COPY environment.yml /tmp/

RUN conda update -y -n base conda \
    && echo '    - pyvirtualdisplay' >> /tmp/environment.yml \
    && conda env create -f /tmp/environment.yml \
    && conda clean -y -t \
    && rm /tmp/environment.yml

ARG username
ARG userid

ARG home=/home/${username}
ARG workdir=${home}/basic_data_science

RUN adduser ${username} --uid ${userid} --gecos '' --disabled-password \
    && echo "${username} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${username} \
    && chmod 0440 /etc/sudoers.d/${username}

WORKDIR ${workdir}
RUN chown ${username}:${username} ${workdir}

USER ${username}
WORKDIR ${workdir}

ENV PATH /opt/conda/envs/jx_ds/bin:$PATH
# COPY ./requirement.txt /app/

RUN git-nbdiffdriver config --enable --global

RUN git config --global diff.jupyternotebook.command 'git-nbdiffdriver diff --ignore-details'

COPY bashrc.bash /tmp/
RUN cat /tmp/bashrc.bash >> ${home}/.bashrc \
    && echo "export PATH=\"${workdir}/docker/bin:$PATH\"" >> ${home}/.bashrc \
    && sudo rm /tmp/bashrc.bash

ENV USERNAME=ji
