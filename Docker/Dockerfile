FROM ubuntu:14.04
MAINTAINER Max Droog Hayes

############################################
# needed for add-apt-repository
RUN apt-get update && apt-get -y install python-software-properties

############################################
# Install oracle jdk
RUN apt-get -y install software-properties-common python-software-properties	

RUN add-apt-repository -y ppa:webupd8team/java

RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections

RUN apt-get -y update

RUN apt-get -y -f install oracle-java7-installer


######################################
Install Cassandra

RUN echo "deb http://debian.datastax.com/community stable main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list

RUN apt-get -y install curl

RUN curl -L http://debian.datastax.com/debian/repo_key | sudo apt-key add -

RUN sudo apt-get -y update

RUN sudo apt-get -y install dsc20

RUN sudo service cassandra stop

RUN sudo rm -rf /var/lib/cassandra/data/system/*

RUN sed -i 's/rpc_address: localhost/rpc_address: 0.0.0.0/' "/etc/cassandra/cassandra.yaml"

############################################
# Make Oracle JDK the default.
RUN apt-get -y -f install oracle-java7-set-default

ENV JVM_OPTS -Djava.net.preferIPv4Stack=true
CMD ["/usr/sbin/cassandra","-f"]

# 9042 is CQL, 9160 is thrift
# TODO - remove thrift?
EXPOSE 9042 9160
