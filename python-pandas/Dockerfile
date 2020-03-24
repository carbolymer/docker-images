FROM python:3.8
WORKDIR /tmp
COPY requirements.txt ./
ENV BUILD_DEPS="build-essential gfortran libhdf5-dev"
ENV HDF5_DIR="/usr/lib/x86_64-linux-gnu/hdf5/serial/"
RUN apt-get update && \
    apt-get install -y --no-install-recommends ${BUILD_DEPS} locales libhdf5-103 hdf5-tools && \
    sed -i 's/^# en_GB.UTF-8 UTF-8$/en_GB.UTF-8 UTF-8/g' /etc/locale.gen && \
    locale-gen && \
    update-locale LANG=en_GB.UTF-8 LC_ALL=en_GB.UTF-8 \
    groupadd -g 1000 workusr && \
    useradd -s /bin/bash -d /work -m -u 1000 -o workusr && \
    rm -rf /var/lib/apt/lists/* && \
    xargs -L 1 -n 1 pip install < requirements.txt && \
    apt-get purge -y --auto-remove ${BUILD_DEPS} && \
    rm -rf /root/.cache/pip && rm -rf /tmp/* && rm -rf /usr/share/doc/* && rm -rf /usr/share/man/* && \
    rm -rf /usr/share/locale/*

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /bin/tini
RUN chmod +x /bin/tini
WORKDIR /work
ENTRYPOINT ["/bin/tini", "--"]
CMD ["python3"]

