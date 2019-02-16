FROM carbolymer/python:python-pandas-0.24.1
WORKDIR /tmp
COPY requirements.txt ./
COPY influxdb-5.2.1.patch ./
ENV BUILD_DEPS="build-essential gfortran git"
RUN apt-get update && \
    apt-get install -y --no-install-recommends ${BUILD_DEPS} tesseract-ocr tesseract-ocr-eng patch && \
    rm -rf /var/lib/apt/lists/* && \
    xargs -L 1 -n 1 pip install < requirements.txt && \
    jupyter nbextension install --py hide_code && \
    jupyter nbextension enable --py hide_code && \
    jupyter serverextension enable --py hide_code && \
    cp -r /usr/local/lib/python3.7/site-packages/jupyter_contrib_nbextensions/nbextensions/* /usr/local/share/jupyter/nbextensions && \
    ( cd /usr/local/lib/python3.7/site-packages && git apply /tmp/influxdb-5.2.1.patch ) && \
    apt-get purge -y --auto-remove ${BUILD_DEPS} && \
    rm -rf /root/.cache/pip && rm -rf /tmp/* && rm -rf /usr/share/doc/* && rm -rf /usr/share/man/* && \
    rm -rf /usr/share/locale/*
CMD ["python3"]
