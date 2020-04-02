# File for building a Algorith App inside a ocker container
# The Python environment will be based off the requirements.txt that can be found in the same folder
# TO BUILD: docker build -t jupyter:latest .    ## FIX
# TO RUN: docker run -v notebook/path/on/host/:/notebooks/ -p 8888:8888 jupyter  ## FIX

FROM ubuntu:latest

LABEL maintainer="Marcio Ribeiro <https://github.com/marciovai>"

ARG external_lib_path

# prepares environment
RUN apt-get update && apt-get upgrade -y && apt-get install -y software-properties-common locales

# set locales
RUN export LC_ALL="en_US.UTF-8"
RUN export LC_CTYPE="en_US.UTF-8"
RUN dpkg-reconfigure locales

# installs pip
RUN apt-get install -y python3-pip
RUN pip3 install --upgrade pip

# copy python packages list to contianer and install
COPY ./requirements.txt .
RUN pip install -r requirements.txt

RUN mkdir external_lib