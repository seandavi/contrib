FROM ubuntu:14.04
MAINTAINER danb@renci.org

RUN apt-get update ; apt-get upgrade -y

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV LC_ALL en_US.UTF-8

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y postgresql wget libcurl4-gnutls-dev

#install iRODS
RUN wget ftp://ftp.renci.org/pub/irods/releases/4.1.2/ubuntu14/irods-resource-4.1.2-ubuntu14-x86_64.deb -O /tmp/irods-iresc.deb

# install package dependencies to prevent Docker build from erring out
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y `dpkg -I /tmp/irods-iresc.deb | sed -n 's/^ Depends: //p' | sed 's/,//g'`
RUN dpkg -i /tmp/irods-iresc.deb

RUN mkdir /opt/irods

ADD ./genresp.sh /opt/irods/genresp.sh
ADD ./config.sh /opt/irods/config.sh
ADD ./bootstrap.sh /opt/irods/bootstrap.sh
RUN chmod a+x /opt/irods/*.sh

EXPOSE 1247
ENTRYPOINT [ "/opt/irods/bootstrap.sh" ]
