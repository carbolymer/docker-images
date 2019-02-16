FROM python:3.7-slim
WORKDIR /tmp
COPY requirements.txt ./
ENV BUILD_DEPS="build-essential gfortran libhdf5-dev"
ENV HDF5_DIR="/usr/lib/x86_64-linux-gnu/hdf5/serial/"
RUN apt-get update && \
    apt-get install -y --no-install-recommends ${BUILD_DEPS} libhdf5-100 hdf5-tools && \
    rm -rf /var/lib/apt/lists/* && \
    xargs -L 1 -n 1 pip install < requirements.txt && \
    apt-get purge -y --auto-remove ${BUILD_DEPS} && \
    rm -rf /root/.cache/pip && rm -rf /tmp/* && rm -rf /usr/share/doc/* && rm -rf /usr/share/man/* && \
    rm -rf /usr/share/locale/*

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /bin/tini
RUN chmod +x /bin/tini
ENTRYPOINT ["/bin/tini", "--"]
CMD ["python3"]

