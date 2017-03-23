FROM carbolymer/python3:pandas-0.19.2
WORKDIR /tmp
COPY requirements.txt ./
ENV BUILD_DEPS="build-essential gfortran"
RUN apt-get update && apt-get install -y --no-install-recommends ${BUILD_DEPS} && rm -rf /var/lib/apt/lists/* && \
    pip3 install --requirement /tmp/requirements.txt && \
    jupyter nbextension install --py hide_code && jupyter nbextension enable --py hide_code && jupyter serverextension enable --py hide_code && \
    apt-get purge -y --auto-remove ${BUILD_DEPS} && \
    rm -rf /root/.cache/pip && rm -rf /tmp/* && rm -rf /usr/share/doc/* && rm -rf /usr/share/man/* && \
    rm -rf /usr/share/locale/*
CMD ["python3"]
