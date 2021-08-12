FROM centos
RUN yum install httpd -y
WORKDIR /var/www/html
ENV PORT 3200
COPY testingAPIS .
CMD apachectl -DFOREGROUND