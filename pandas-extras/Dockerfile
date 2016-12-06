FROM carbolymer/python3:pandas-0.19.1
WORKDIR /tmp
COPY requirements.txt ./
ENV BUILD_DEPS="build-essential gfortran"
RUN apt-get update && apt-get install -y --no-install-recommends ${BUILD_DEPS} && rm -rf /var/lib/apt/lists/* && \
    pip3 install --requirement /tmp/requirements.txt && \
    apt-get purge -y --auto-remove ${BUILD_DEPS} && \
    rm -rf /root/.cache/pip && rm -rf /tmp/* && rm -rf /usr/share/doc/* && rm -rf /usr/share/man/* && \
    rm -rf /usr/share/locale/* && rm -rf /usr/local/lib/python3.5/__pycache__/*
CMD ["python3"]
