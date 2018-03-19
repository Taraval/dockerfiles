FROM resin/raspberry-pi-buildpack-deps:jessie

# remove several traces of debian python
RUN apt-get purge -y python.*


ENV LANG C.UTF-8

ENV PYTHON_VERSION 2.7.14

RUN set -x && \
        mkdir -p /tmp/py && \
        cd /tmp/py && \
        curl -SL "https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tgz" -o Python-$PYTHON_VERSION.tar.gz && \
        tar zxvf Python-$PYTHON_VERSION.tar.gz

RUN set -x && \
        cd /tmp/py/Python-$PYTHON_VERSION && \
        ./configure && \
        make -j$(nproc) && \
        make install -j$(nproc) && \
        rm -rf /tmp/py

RUN set -x && \
        mkdir -p /data

# Define working directory
WORKDIR /data

CMD ["bash"]
ENV PYTHONPATH /usr/lib/python2.7/dist-packages:/usr/lib/python2.7/site-packages:$PYTHONPATH

