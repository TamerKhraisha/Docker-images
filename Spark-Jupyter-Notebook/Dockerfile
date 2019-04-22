FROM continuumio/anaconda3
 
RUN set -ex \
    && apt-get update -yqq \
    && apt-get upgrade -yqq \
    && apt-get install -yqq  \
       apt-utils \
       python3-pip \
       python3-requests \
       wget \
       default-jre \
       scala \
   && mkdir certs \
   && openssl req -x509 -nodes -days 365 -subj '/C=no/ST=no/L=no/CN=no' -newkey rsa:1024 -keyout mycert.pem -out certs/mycert.pem \
   && wget http://archive.apache.org/dist/spark/spark-2.1.1/spark-2.1.1-bin-hadoop2.7.tgz && tar -zxvf spark-2.1.1-bin-hadoop2.7.tgz \
   && pip3 install findspark \
   && pip3 install numpy \
   && pip3 install p4j \
   && pip3 install pyspark

ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LC_CTYPE en_US.UTF-8
ENV LC_MESSAGES en_US.UTF-8
