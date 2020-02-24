# File for building a Jupyter Notebook Server inside a Docker container
# The Python environment will be based off the requirements.txt that can be found in the same folder
# When building remembeer to pass in the host machine path for notebooks
# TO BUILD: docker build -t jupyter:latest .    
# TO RUN: docker run -v notebook/path/on/host/:/notebooks/ -p 8888:8888 jupyter 

FROM ubuntu:latest

LABEL maintainer="Marcio Ribeiro <https://github.com/marciovai>"

# prepares environment
RUN apt-get update && apt-get upgrade && apt-get install -y software-properties-common locales

# set locales
RUN export LC_ALL="en_US.UTF-8"
RUN export LC_CTYPE="en_US.UTF-8"
RUN dpkg-reconfigure locales

# installs pip
RUN apt-get install -y python3-pip
RUN pip3 install --upgrade pip

# copy python packages to contianer
COPY ./requirements.txt .

RUN pip install -r requirements.txt

RUN mkdir notebooks

# uses tini package for improving the Jupyter Notebook runtime
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

# runs jupyter notebook
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root", "--notebook-dir=/notebooks"]