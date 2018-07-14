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
RUN yum -y localinstall /tmp/grafana-5.2.1-1.x86_64.rpm
RUN /etc/init.d/grafana-server start

# kaltura prometheus packages
RUN rpm -ihv http://installrepo.kaltura.org/releases/kaltura-release.noarch.rpm
RUN sed -i -e 's@installrepo.kaltura.org@installrepo.origin.kaltura.org@g' -e 's@latest@nightly@g'  /etc/yum.repos.d/kaltura.repo
RUN sed -i 's@^tsflags=nodocs@#tsflags=nodocs@g' /etc/yum.conf
RUN yum install -y kaltura-prometheus kaltura-alertmanager kaltura-consul kaltura-apache-exporter kaltura-node-exporter 

# utils needed to for demo purposes, on Prod, these are not mandatory
RUN yum install -y links curl vim-enhanced

EXPOSE 80 443 9090 8080 3000 9093 8300 8301 8302


# start services
CMD ["/sbin/init"]
