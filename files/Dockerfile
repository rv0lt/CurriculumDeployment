FROM pandoc/latex AS pandoc

COPY cv /data/cv/

WORKDIR /data/cv

RUN tlmgr install sourcesanspro
RUN tlmgr install ly1
RUN tlmgr install moresize
RUN tlmgr install anyfontsize
RUN tlmgr install enumitem
RUN tlmgr install titlesec
RUN tlmgr install standalone
RUN tlmgr install svn-prov
RUN tlmgr install blindtext

RUN pdflatex resume.tex -o resume.pdf

FROM ubuntu/nginx as base
#WORKDIR /

COPY --from=pandoc /data/cv/resume.pdf /usr/share/nginx
COPY default.conf /etc/nginx/conf.d/default.conf

#RUN chown -R nginx:nginx /etc/nginx/ /usr/share/nginx
#USER nginx
#RUN chmod 777 /sbin/nginx

FROM scratch 

# nginx: [emerg] getgrnam("www-data") failed (2: No such file or directory) in /etc/nginx/nginx.conf:1
# Something in /etc is making this error if not copied, i don't know which file yet...
# samw wirh var

COPY --from=base /var/ /var/

COPY --from=base /etc/group /etc/group 
COPY --from=base /etc/passwd /etc/passwd

COPY --from=base /usr/lib/ /usr/lib/
COPY --from=base /lib/ /lib/

COPY --from=base /lib/x86_64-linux-gnu/libcrypt.so.1 /lib/x86_64-linux-gnu/libcrypt.so.1
COPY --from=base /lib/x86_64-linux-gnu/libpcre.so.3 /lib/x86_64-linux-gnu/libpcre.so.3
COPY --from=base /lib/x86_64-linux-gnu/libssl.so.3 /lib/x86_64-linux-gnu/libssl.so.3
COPY --from=base /lib/x86_64-linux-gnu/libcrypto.so.3 /lib/x86_64-linux-gnu/libcrypto.so.3
COPY --from=base /lib/x86_64-linux-gnu/libz.so.1 /lib/x86_64-linux-gnu/libz.so.1
COPY --from=base /lib/x86_64-linux-gnu/libc.so.6 /lib/x86_64-linux-gnu/libc.so.6
COPY --from=base  /lib64/ld-linux-x86-64.so.2  /lib64/ld-linux-x86-64.so.2

COPY --from=base /var/lib/nginx/ /var/lib/nginx/
COPY --from=base /usr/lib/nginx/ /usr/lib/nginx/
COPY --from=base /usr/share/nginx/ /usr/share/nginx/
COPY --from=base /var/log/nginx/ /var/log/nginx/ 
COPY --from=base /etc/nginx/ /etc/nginx/
COPY --from=base /sbin/nginx /sbin/nginx

EXPOSE 8080
#USER nginx
#ENTRYPOINT ["/sbin/nginx"]
CMD ["/sbin/nginx","-g", "daemon off;"]
