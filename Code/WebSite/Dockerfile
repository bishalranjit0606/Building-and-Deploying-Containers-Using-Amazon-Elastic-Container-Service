FROM rockylinux/rockylinux

ARG ELBDNS
ENV ServerName=Storyizer-site ELBDNS=${ELBDNS}

RUN yum -y update && \
    yum -y install httpd unzip && \
    yum clean all

# Install app
COPY ./code/ /var/www/html/

# Config App
RUN echo "ServerName storyizer.training " >> /etc/httpd/conf/httpd.conf \
  && sed -i -- "s|APIELB|$ELBDNS|g" /var/www/html/js/env.js \
  && sed -i -- "s|SaveELB|$ELBDNS|g" /var/www/html/js/env.js

EXPOSE 80

ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]
