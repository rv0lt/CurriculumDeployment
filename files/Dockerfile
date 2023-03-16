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
WORKDIR /

COPY --from=pandoc /data/cv/resume.pdf /usr/share/nginx
COPY default.conf /etc/nginx/conf.d/default.conf

RUN useradd -u 10001 scratchuser
RUN chown -R nginx:nginx /etc/nginx/ /usr/share/nginx
RUN chown nginx:nginx /sbin/nginx

FROM scratch

COPY --from=base /etc/passwd /etc/passwd
COPY --from=base /usr/share/nginx /usr/share/nginx
COPY --from=base /etc/nginx/ /etc/nginx/
COPY --from=base /sbin/nginx/ /sbin/nginx/

EXPOSE 8080
USER nginx
ENTRYPOINT ["/sbin/nginx"]
CMD ["-g", "daemon off;"]