# Based on https://codelabs.developers.google.com/codelabs/openthread-hardware/#0

FROM ubuntu

ENV HTM_SERVER /root/nupic-history-server
ENV CELL_VIZ /root/cell-viz
ENV HTM_VIZ /root/htm-school-viz

RUN apt update && apt-get -yq install software-properties-common git curl

RUN cd /root \
  && git clone https://github.com/htm-community/nupic-history-server \
  && git clone https://github.com/numenta/cell-viz \
  && git clone https://github.com/htm-community/htm-school-viz

RUN add-apt-repository ppa:deadsnakes/ppa \
  && apt-get -yq update \
  && apt-get -yq install python2.7

RUN cd tmp \
  && curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
  && python2.7 get-pip.py

RUN python2.7 -m pip install --user numpy

RUN python2.7 -m pip install --upgrade pip setuptools wheel

RUN apt-get -yq install g++ python-dev python3-dev

RUN apt-get -yq install make

RUN curl -O https://capnproto.org/capnproto-c++-0.7.0.tar.gz \
  && tar zxf capnproto-c++-0.7.0.tar.gz \
  && cd capnproto-c++-0.7.0 \
  && ./configure --disable-dependency-tracking \
  && make -j6 check \
  && make install 

RUN pip install nupic

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - 
RUN apt-get install -y nodejs
RUN npm install webpack webpack-cli

RUN pip install ujson web.py

RUN npm install -D babel-loader @babel/core @babel/preset-env webpack
RUN npm install three-obj-loader three-collada-loader three express-http-proxy express express-handlebars

RUN cd /root/cell-viz && /node_modules/.bin/webpack 
RUN ln -s out/dynson.js /root/htm-school-viz/static/js/third/dyson-bundle.js

COPY go /root/go
CMD . /root/go

