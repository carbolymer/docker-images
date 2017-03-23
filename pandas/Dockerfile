FROM python:3.6.1-slim
WORKDIR /tmp
COPY requirements.txt ./
ENV BUILD_DEPS="build-essential gfortran libhdf5-dev"
RUN apt-get update && apt-get install -y --no-install-recommends ${BUILD_DEPS} libhdf5-8 && rm -rf /var/lib/apt/lists/* && \
    HDF5_DIR=/usr/lib/x86_64-linux-gnu/hdf5/serial/ pip3 install --requirement /tmp/requirements.txt && \
    apt-get purge -y --auto-remove ${BUILD_DEPS} && \
    rm -rf /root/.cache/pip && rm -rf /tmp/* && rm -rf /usr/share/doc/* && rm -rf /usr/share/man/* && \
    rm -rf /usr/share/locale/* && rm -rf /usr/local/lib/python3.5/__pycache__/*

ENV TINI_VERSION v0.14.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /bin/tini
RUN chmod +x /bin/tini
ENTRYPOINT ["/bin/tini", "--"]
CMD ["python3"]

