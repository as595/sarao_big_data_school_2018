FROM kernsuite/base:3
MAINTAINER Ben Hugo "bhugo@ska.ac.za"

ENV DEB_REQ casacore-dev \
            casacore-data \
            python-casacore \
            libcasa* \
            aoflagger \
            graphviz \
            vim \
            virtualenv \
            build-essential \
            libpython2.7-dev \
            libboost-all-dev \
	    wcslib-dev \
	    libcfitsio3-dev \
            openssh-server \
	    sudo \
	    libpam0g-dev \
	    npm \
            nodejs-legacy \
	    python-dev \
            python3-dev \
            python3-pip \
            python-pip

RUN mkdir /src

RUN apt-get update
RUN apt-get install -y --allow-unauthenticated $DEB_REQ
RUN npm install -g configurable-http-proxy

COPY requirements.txt /src/requirements.txt
RUN pip3 install -r /src/requirements.txt
RUN pip3 install jupyterhub
RUN pip install -U pip setuptools wheel
RUN pip install -r /src/requirements.txt
RUN python2 -m ipykernel install
RUN python3 -m ipykernel install

# bake in an SSH server for quick access
RUN /usr/bin/ssh-keygen -A
RUN mkdir /var/run/sshd
RUN sed 's/Port 22/Port 50100/g' -i /etc/ssh/sshd_config 

ENTRYPOINT /bin/bash
