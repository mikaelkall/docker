# Basic OMD installation for testing
# ==================================
FROM centos:centos7
MAINTAINER Mikael Kall <mikael.kall@unibet.com>

# install main packages:
ADD files/labs-consol-stable.repo /etc/yum.repos.d/labs-consol-stable.repo
RUN yum -y install epel-release
RUN yum -y update

# install omd 
RUN yum install -y omd-labs-edition-daily || true
RUN yum install -y libdbi
RUN yum install -y which

EXPOSE 5000
ADD files/start.sh /tmp/start.sh

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
