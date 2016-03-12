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

RUN omd create prod
RUN omd config prod set INFLUXDB on
RUN omd config prod set GRAFANA on 
RUN omd config prod set CORE nagios
RUN omd config prod set APACHE_TCP_ADDR 0.0.0.0
RUN omd start prod
