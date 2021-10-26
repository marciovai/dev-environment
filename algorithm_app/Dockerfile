# Allows for deploying an external library (or API) from inside a container
'# The Python environment will be based on requirements.txt from the same folder'
# BUILD: docker build -t jupyter:latest .
# RUN: docker run -v notebook/path/on/host/:/notebooks/ -p 8888:8888 jupyter

FROM ubuntu:latest

LABEL maintainer="Marcio Ribeiro <https://github.com/marciovai>"

ARG external_lib_path

# install dependencies
RUN apt-get update && apt-get upgrade -y && apt-get install -y software-properties-common locales

# set locale
RUN export LC_ALL="en_US.UTF-8"
RUN export LC_CTYPE="en_US.UTF-8"
RUN dpkg-reconfigure locales

# install/upgrade pip
RUN apt-get install -y python3-pip
RUN pip3 install --upgrade pip

# install requirements
COPY ./requirements.txt .
RUN pip install -r requirements.txt

RUN mkdir external_lib