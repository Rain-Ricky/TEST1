FROM hub.c.163.com/library/httpd:latest
MAINTAINER bob botopcoder@163

RUN mkdir -p /usr/local/apache2/htdocs/img
WORKDIR /usr/local/apache2
COPY img/1/1.png /usr/local/apache2/htdocs/img

EXPOSE 80
ENTRYPOINT ["httpd"]
CMD ["-D","FOREGROUND"]