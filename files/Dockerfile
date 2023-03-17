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

# fix var
COPY --from=base /var/ /var/

COPY --from=base /etc/group /etc/group 
COPY --from=base /etc/passwd /etc/passwd
# ldd /sbin/nginx
#  linux-vdso.so.1 (0x00007ffce5ea2000)
#  libcrypt.so.1 => /lib/x86_64-linux-gnu/libcrypt.so.1 (0x00007f09d0948000)
#  libpcre.so.3 => /lib/x86_64-linux-gnu/libpcre.so.3 (0x00007f09d08d2000)
#  libssl.so.3 => /lib/x86_64-linux-gnu/libssl.so.3 (0x00007f09d082d000)
#  libcrypto.so.3 => /lib/x86_64-linux-gnu/libcrypto.so.3 (0x00007f09d03dc000)
#  libz.so.1 => /lib/x86_64-linux-gnu/libz.so.1 (0x00007f09d03c0000)
#  libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f09d01b9000)
#  /lib64/ld-linux-x86-64.so.2 (0x00007f09d0adb000)

                              
#COPY --from=base /lib/x86_64-linux-gnu/ /lib/x86_64-linux-gnu/

#COPY --from=base /lib/x86_64-linux-gnu/audit/ /lib/x86_64-linux-gnu/audit/
#COPY --from=base /lib/x86_64-linux-gnu/e2fsprogs/ /lib/x86_64-linux-gnu/e2fsprogs/
#COPY --from=base /lib/x86_64-linux-gnu/engines-3/ /lib/x86_64-linux-gnu/engines-3/
#COPY --from=base /lib/x86_64-linux-gnu/gconv /lib/x86_64-linux-gnu/gconv

#COPY --from=base /lib/x86_64-linux-gnu/ossl-modules/ /lib/x86_64-linux-gnu/ossl-modules/
#COPY --from=base /lib/x86_64-linux-gnu/perl-base/ /lib/x86_64-linux-gnu/perl-base/
#COPY --from=base /lib/x86_64-linux-gnu/security/ /lib/x86_64-linux-gnu/security/

COPY --from=base /lib/x86_64-linux-gnu/libgcc_s.so.1 /lib/x86_64-linux-gnu/libgcc_s.so.1
COPY --from=base /lib/x86_64-linux-gnu/libstdc++.so.6 /lib/x86_64-linux-gnu/libstdc++.so.6
COPY --from=base /lib/x86_64-linux-gnu/libicudata.so.71 /lib/x86_64-linux-gnu/libicudata.so.71
COPY --from=base /lib/x86_64-linux-gnu/libc.so.6 /lib/x86_64-linux-gnu/libm.so.6
COPY --from=base /lib/x86_64-linux-gnu/liblzma.so.5 /lib/x86_64-linux-gnu/liblzma.so.5
COPY --from=base /lib/x86_64-linux-gnu/libicuuc.so.71 /lib/x86_64-linux-gnu/libicuuc.so.71
COPY --from=base /lib/x86_64-linux-gnu/libxml2.so.2 /lib/x86_64-linux-gnu/libxml2.so.2
COPY --from=base /lib/x86_64-linux-gnu/libcap-ng.so.0 /lib/x86_64-linux-gnu/libcap-ng.so.0
COPY --from=base /lib/x86_64-linux-gnu/libaudit.so.1 /lib/x86_64-linux-gnu/libaudit.so.1
COPY --from=base /lib/x86_64-linux-gnu/libpam.so.0 /lib/x86_64-linux-gnu/libpam.so.0
COPY --from=base /lib/x86_64-linux-gnu/libcrypt.so.1 /lib/x86_64-linux-gnu/libcrypt.so.1
COPY --from=base /lib/x86_64-linux-gnu/ /lib/x86_64-linux-gnu/
COPY --from=base /lib/x86_64-linux-gnu/libpcre.so.3 /lib/x86_64-linux-gnu/libpcre.so.3
COPY --from=base /lib/x86_64-linux-gnu/libssl.so.3 /lib/x86_64-linux-gnu/libssl.so.3
COPY --from=base /lib/x86_64-linux-gnu/libcrypto.so.3 /lib/x86_64-linux-gnu/libcrypto.so.3
COPY --from=base /lib/x86_64-linux-gnu/libz.so.1 /lib/x86_64-linux-gnu/libz.so.1
COPY --from=base /lib/x86_64-linux-gnu/libc.so.6 /lib/x86_64-linux-gnu/libc.so.6
COPY --from=base /lib64/ld-linux-x86-64.so.2  /lib64/ld-linux-x86-64.so.2

COPY --from=base /var/lib/nginx/ /var/lib/nginx/
COPY --from=base /usr/lib/nginx/ /usr/lib/nginx/
COPY --from=base /usr/share/nginx/ /usr/share/nginx/
COPY --from=base /var/log/nginx/ /var/log/nginx/ 
COPY --from=base /etc/nginx/ /etc/nginx/
COPY --from=base /sbin/nginx /sbin/nginx

EXPOSE 8080
#USER nginx
CMD ["/sbin/nginx","-g", "daemon off;"]
