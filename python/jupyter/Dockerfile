FROM vkyii/anaconda:latest

MAINTAINER twist@vkyii.com

RUN yum -y install gcc make \
 && wget http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz \
 && tar -zxvf ta-lib-0.4.0-src.tar.gz \
 && cd ta-lib \
 && ./configure --prefix=/usr \
 && make \
 && make install \
 && cd .. \
 && rm -rf ta-lib \
 && rm -f ta-lib-0.4.0-src.tar.gz \
 && yum clean all

RUN pip install --upgrade pip \
 && pip install tushare \
 && pip install TA-Lib

# config
ADD .jupyter/jupyter_notebook_config.py /root/.jupyter/jupyter_notebook_config.py
ADD ./jupyter.sh /usr/local/bin/jupyter.sh

VOLUME /notebooks
WORKDIR /notebooks

ENV LD_LIBRARY_PATH /usr/lib:$LD_LIBRARY_PATH
ENTRYPOINT ["/tini", "--"]
EXPOSE 8888

CMD ["bash", "/usr/local/bin/jupyter.sh"]