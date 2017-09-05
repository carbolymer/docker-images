FROM carbolymer/python:python-pandas-0.20.3
WORKDIR /tmp
COPY requirements.txt ./
ENV BUILD_DEPS="build-essential gfortran"
RUN apt-get update && apt-get install -y --no-install-recommends ${BUILD_DEPS} tesseract-ocr tesseract-ocr-eng && rm -rf /var/lib/apt/lists/* && \
    pip3 install --requirement /tmp/requirements.txt && \
    jupyter nbextension install --py hide_code && jupyter nbextension enable --py hide_code && jupyter serverextension enable --py hide_code && \
    cp -r /usr/local/lib/python3.6/site-packages/jupyter_contrib_nbextensions/nbextensions/* /usr/local/share/jupyter/nbextensions && \
    apt-get purge -y --auto-remove ${BUILD_DEPS} && \
    rm -rf /root/.cache/pip && rm -rf /tmp/* && rm -rf /usr/share/doc/* && rm -rf /usr/share/man/* && \
    rm -rf /usr/share/locale/*
CMD ["python3"]
