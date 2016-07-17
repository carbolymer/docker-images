FROM python:3.5.2-slim
WORKDIR /tmp
COPY requirements.txt ./
ENV BUILD_DEPS="build-essential gfortran libhdf5-dev"
RUN apt-get update && apt-get install -y --no-install-recommends ${BUILD_DEPS} && rm -rf /var/lib/apt/lists/*
RUN pip3 install --requirement /tmp/requirements.txt
RUN apt-get purge -y --auto-remove ${BUILD_DEPS}
ENTRYPOINT ["python3"]
