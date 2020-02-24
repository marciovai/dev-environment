FROM ubuntu:latest

MAINTAINER "Marcio Ribeiro <https://github.com/marciovai>"

RUN apt-get update && apt-get upgrade && apt-get install -y software-properties-common locales

RUN export LC_ALL="en_US.UTF-8"
RUN export LC_CTYPE="en_US.UTF-8"
RUN dpkg-reconfigure locales

RUN apt-get install -y python3-pip
RUN pip3 install --upgrade pip

COPY ./requirements.txt .

RUN pip install -r requirements.txt

RUN mkdir notebooks

# CMD /bin/bash -c "source env/bin/activate ; jupyter-notebook --ip=0.0.0.0 --port=8888 --no-browser" 

# Add Tini. Tini operates as a process subreaper for jupyter. This prevents kernel crashes.
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]