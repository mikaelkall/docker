# Basic OMD installation for testing
# ==================================
FROM centos:centos7
MAINTAINER Mikael Kall <mikael.kall@unibet.com>

# install main packages:
RUN rpm -Uvh "https://labs.consol.de/repo/stable/rhel7/x86_64/labs-consol-stable.rhel7.noarch.rpm"
RUN yum -y install epel-release
RUN yum -y update

# install omd 
RUN yum install -y omd-2.10-labs-edition || true
RUN yum install -y libdbi
RUN yum install -y which

EXPOSE 5000
ADD start.sh /tmp/start.sh

RUN omd create prod || true
RUN sed "s/CONFIG_TMPFS='on'/CONFIG_TMPFS='off'/" -i /omd/sites/prod/etc/omd/site.conf 
RUN ["omd","config","prod","set","TMPFS","off"]
RUN ["omd","config","prod","set","DEFAULT_GUI","check_mk"]
RUN ["omd","config","prod","set","INFLUXDB","on"]
RUN ["omd","config","prod","set","GRAFANA","on"] 
RUN ["omd","config","prod","set","MYSQL","on"]
RUN ["omd","config","prod","set","CORE","nagios"]
RUN ["omd","config","prod","set","THRUK_COOKIE_AUTH","off"]
RUN ["omd","config","prod","set","APACHE_TCP_ADDR","0.0.0.0"]
CMD /tmp/start.sh
