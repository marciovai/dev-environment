# Builds a Jupyter Notebook Server inside a Docker container
# The Python environment will be based on requirements.txt from the same folder
# when building don't forget to point to the correct location in the host
# BUILD: docker build -t jupyter:latest .    
# RUN: docker run -v notebook/path/on/host/:/notebooks/ -p 8888:8888 jupyter 

FROM ubuntu:latest

LABEL maintainer="Marcio Ribeiro <https://github.com/marciovai>"

# install dependencies
RUN apt-get update && apt-get upgrade && apt-get install -y software-properties-common locales

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

RUN mkdir notebooks

# use tini package for improving the Jupyter Notebook runtime
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

# run jupyter notebook
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root", "--notebook-dir=/notebooks"]