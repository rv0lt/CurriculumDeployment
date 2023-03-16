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

COPY --from=pandoc /data/cv/resume.pdf /usr/share/nginx
COPY default.conf /etc/nginx/conf.d/default.conf

FROM scratch

COPY --from=base /etc/passwd /etc/group /etc/
COPY --from=base /usr/share/nginx /usr/share/nginx
COPY --from=base /etc/nginx/ /etc/nginx/
COPY --from=base /sbin/nginx/ /sbin/nginx/

EXPOSE 8080

ENTRYPOINT ["/sbin/nginx"]
CMD ["-g", "daemon off;"]