FROM carbolymer/python:python-pandas-1.2.2-1
WORKDIR /tmp
COPY requirements.txt ./
COPY apache-airflow /usr/bin
ENV BUILD_DEPS="build-essential gfortran git"
RUN apt-get update && \
    apt-get install -y --no-install-recommends ${BUILD_DEPS} netcat tesseract-ocr tesseract-ocr-eng vim patch && \
    rm -rf /var/lib/apt/lists/* && \
    xargs -L 1 -n 1 pip install < requirements.txt && \
    pip install --no-warn-conflicts cattrs==1.0 && \
    jupyter nbextension install --py hide_code && \
    jupyter nbextension enable --py hide_code && \
    jupyter serverextension enable --py hide_code && \
    cp -r /usr/local/lib/python3.8/site-packages/jupyter_contrib_nbextensions/nbextensions/* /usr/local/share/jupyter/nbextensions && \
    chmod +x /usr/bin/apache-airflow && \
    apt-get purge -y --auto-remove ${BUILD_DEPS} && \
    rm -rf /root/.cache/pip && rm -rf /tmp/* && rm -rf /usr/share/doc/* && rm -rf /usr/share/man/* && \
    rm -rf /usr/share/locale/* && \
    mkdir -p /work/.cache /work/.local/share /work/.ipython/profile_default && \
    chown -R workusr:workusr /work
WORKDIR /work
CMD ["python3"]
