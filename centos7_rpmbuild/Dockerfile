FROM centos:centos7

# install main packages:
RUN yum -y update; yum clean all;
RUN yum -y install epel-release; yum clean all;

# install rpmbuild tools
RUN yum -y install rpm-libs
RUN yum -y install rpm-build
RUN yum -y install rpmdevtools

# create builddir
RUN mkdir -p /root/rpmbuild/{BUILD,BUILDROOT,RPMS,SOURCES,SPECS,SRPMS}

# add rpmmacros file
ADD files/rpmmacros /root/.rpmmacros
