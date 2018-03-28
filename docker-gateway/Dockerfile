FROM alpine:latest
MAINTAINER Mikael Kall <mikael.kall@kindredgroup.com>

ENV ROOT_PASSWORD root

RUN set -x \
  && apk update \
  && apk add \
     vim \
     nmap    

RUN apk --update add openssh \
		&& sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
		&& sed -i 's/#Port 22/Port 2222/' /etc/ssh/sshd_config \
        && echo "root:${ROOT_PASSWORD}" | chpasswd \
		&& rm -rf /var/cache/apk/* /tmp/* \
                && /usr/bin/ssh-keygen -A

COPY files/profile /root/.profile
COPY entrypoint.sh /usr/local/bin/
COPY files/motd /etc/motd

EXPOSE 2222

CMD ["/usr/local/bin/entrypoint.sh"]
