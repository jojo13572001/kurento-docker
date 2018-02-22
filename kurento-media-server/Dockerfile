# stream oriented kurento
#
# VERSION               4.4.3

FROM      ubuntu:14.04
MAINTAINER Patxi Gortázar <patxi.gortazar@gmail.com>

RUN apt-get update \
  && apt-get -y dist-upgrade \
	&& apt-get install -y wget curl

RUN	echo "deb http://ubuntu.kurento.org/ trusty kms6" | tee /etc/apt/sources.list.d/kurento.list \
	&& wget -O - http://ubuntu.kurento.org/kurento.gpg.key | apt-key add - \
	&& apt-get update \
	&& apt-get -y install kurento-media-server-6.0 \
	&& apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install kms-crowddetector-6.0
RUN curl -sL https://deb.nodesource.com/setup_4.x | sudo bash -
RUN apt-get install -y nodejs
RUN npm install -g bower
RUN npm install http-server -g
RUN apt-get install -y git 
#RUN git clone -b streetlight https://github.com/jojo13572001/kurento-IPCam-H264.git
#RUN cd kurento-IPCam-H264 && bower install --allow-root

EXPOSE 30063 8443

COPY ./entrypoint.sh /entrypoint.sh
COPY ./healthchecker.sh /healthchecker.sh

HEALTHCHECK --interval=5m --timeout=3s --retries=1 CMD /healthchecker.sh

ENV GST_DEBUG=Kurento*:5

ENTRYPOINT ["/entrypoint.sh"]
