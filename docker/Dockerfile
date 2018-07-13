FROM centos:6


RUN echo "NETWORKING=yes" > /etc/sysconfig/network


# deps
RUN yum install -y postfix ntp wget
RUN chkconfig postfix on
RUN chkconfig ntpd on
RUN sed -i 's@^inet_protocols = all@inet_protocol = ipv4@g' /etc/postfix/main.cf
RUN service postfix start
RUN service ntpd start

# grafana
RUN wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-5.2.1-1.x86_64.rpm -O /tmp/grafana-5.2.1-1.x86_64.rpm
RUN yum localinstall /tmp/grafana-5.2.1-1.x86_64.rpm


# kaltura prometheus packages
RUN rpm -ihv http://installrepo.kaltura.org/releases/kaltura-release.noarch.rpm
RUN sed -i 's@installrepo.kaltura.org@installrepo.origin.kaltura.org@g' /etc/yum.repos.d/kaltura.repo
RUN sed -i 's@^tsflags=nodocs@#tsflags=nodocs@g' /etc/yum.conf
RUN yum install -y kaltura-prometheus kaltura-alertmanager kaltura-consul kaltura-apache-exporter kaltura-node-exporter


EXPOSE 80 443 9090 8080 3000


# start services
CMD ["/sbin/init"]
