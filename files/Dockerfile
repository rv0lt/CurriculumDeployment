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

FROM nginx:alpine

COPY --from=pandoc /data/cv/resume.pdf /usr/share/nginx
COPY default.conf /etc/nginx/conf.d/default.conf

EXPOSE 8080

#ENTRYPOINT [ "sleep" ]
#CMD ["9999"]
