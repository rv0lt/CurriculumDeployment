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

FROM nginx:stable-alpine as base

RUN chown -R nginx:nginx /var/cache/nginx /etc/nginx/

FROM scratch

COPY --from=base /etc/passwd /etc/passwd

COPY --from=base [ \
    "/lib/ld-musl-x86_64.so.1", \
    "/lib/libssl.so.1.1", \
    "/lib/libcrypto.so.1.1", \
    "/lib/libz.so.1", \
    "/lib/ld-musl-x86_64.so.1", \
    "/lib/" \
    ]

COPY --from=base ["/usr/lib/libpcre2-8.so.0", "/usr/lib/"]
COPY --from=base ["/usr/sbin/nginx", "/usr/sbin/nginx"]
COPY --from=base ["/var/log/nginx", "/var/log/nginx"]
COPY --from=base ["/etc/nginx", "/etc/nginx"]
COPY --from=base ["/usr/share/nginx/html/index.html", "/usr/share/nginx/html/index.html"]


COPY --from=pandoc /data/cv/resume.pdf /usr/share/nginx
COPY default.conf /etc/nginx/conf.d/default.conf

EXPOSE 8080

USER nginx
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]