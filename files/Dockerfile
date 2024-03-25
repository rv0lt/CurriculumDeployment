FROM ubuntu/nginx:1.18-21.10_edge as base

COPY ./files/cv/resume.pdf /usr/share/nginx
COPY ./files/default.conf /etc/nginx/conf.d/default.conf

# create empty run directory
RUN mkdir -p /run/run

EXPOSE 8080
# no need to use the USER directive bc the nginx process already runs as a non-priviledged user and we have no shell
CMD ["/sbin/nginx","-g", "daemon off;"]
