FROM ubuntu/nginx:1.18-21.10_edge as base

COPY ./files/cv/resume.pdf /usr/share/nginx
COPY ./files/default.conf /etc/nginx/conf.d/default.conf

# create empty run directory
RUN mkdir -p /run/run

FROM scratch 

# we need the run directory to store the process.pid file
COPY --from=base /run/run/ /run/

# copy the users and groups files
COPY --from=base /etc/group /etc/group 
COPY --from=base /etc/passwd /etc/passwd
                              
# COPY the libraries needed to run nginx
# Some libraries are obtained using ldd. The rest are requieres libraries used by the actived modules by default
COPY --from=base /lib/x86_64-linux-gnu/libgcc_s.so.1 /lib/x86_64-linux-gnu/libgcc_s.so.1
COPY --from=base /lib/x86_64-linux-gnu/libstdc++.so.6 /lib/x86_64-linux-gnu/libstdc++.so.6
COPY --from=base /lib/x86_64-linux-gnu/libicudata.so.71 /lib/x86_64-linux-gnu/libicudata.so.71
COPY --from=base /lib/x86_64-linux-gnu/libc.so.6 /lib/x86_64-linux-gnu/libc.so.6
COPY --from=base /lib/x86_64-linux-gnu/liblzma.so.5 /lib/x86_64-linux-gnu/liblzma.so.5
COPY --from=base /lib/x86_64-linux-gnu/libicuuc.so.71 /lib/x86_64-linux-gnu/libicuuc.so.71
COPY --from=base /lib/x86_64-linux-gnu/libxml2.so.2 /lib/x86_64-linux-gnu/libxml2.so.2
COPY --from=base /lib/x86_64-linux-gnu/libcap-ng.so.0 /lib/x86_64-linux-gnu/libcap-ng.so.0
COPY --from=base /lib/x86_64-linux-gnu/libaudit.so.1 /lib/x86_64-linux-gnu/libaudit.so.1
COPY --from=base /lib/x86_64-linux-gnu/libpam.so.0 /lib/x86_64-linux-gnu/libpam.so.0
COPY --from=base /lib/x86_64-linux-gnu/libcrypt.so.1 /lib/x86_64-linux-gnu/libcrypt.so.1
COPY --from=base /lib/x86_64-linux-gnu/libpcre.so.3 /lib/x86_64-linux-gnu/libpcre.so.3
COPY --from=base /lib/x86_64-linux-gnu/libssl.so.3 /lib/x86_64-linux-gnu/libssl.so.3
COPY --from=base /lib/x86_64-linux-gnu/libcrypto.so.3 /lib/x86_64-linux-gnu/libcrypto.so.3
COPY --from=base /lib/x86_64-linux-gnu/libz.so.1 /lib/x86_64-linux-gnu/libz.so.1
COPY --from=base /lib/x86_64-linux-gnu/libc.so.6 /lib/x86_64-linux-gnu/libc.so.6
COPY --from=base /lib64/ld-linux-x86-64.so.2  /lib64/ld-linux-x86-64.so.2
COPY --from=base /lib/x86_64-linux-gnu/libm.so.6 /lib/x86_64-linux-gnu/libm.so.6
COPY --from=base /lib/x86_64-linux-gnu/libgcc_s.so.1 /lib/x86_64-linux-gnu/libgcc_s.so.1
COPY --from=base /lib/x86_64-linux-gnu/libmaxminddb.so.0 /lib/x86_64-linux-gnu/libmaxminddb.so.0
COPY --from=base /lib/x86_64-linux-gnu/libgd.so.3 /lib/x86_64-linux-gnu/libgd.so.3
COPY --from=base /lib/x86_64-linux-gnu/libpng16.so.16 /lib/x86_64-linux-gnu/libpng16.so.16
COPY --from=base /lib/x86_64-linux-gnu/libfontconfig.so.1 /lib/x86_64-linux-gnu/libfontconfig.so.1
COPY --from=base /lib/x86_64-linux-gnu/libfreetype.so.6 /lib/x86_64-linux-gnu/libfreetype.so.6
COPY --from=base /lib/x86_64-linux-gnu/libjpeg.so.8 /lib/x86_64-linux-gnu/libjpeg.so.8
COPY --from=base /lib/x86_64-linux-gnu/libuuid.so.1 /lib/x86_64-linux-gnu/libuuid.so.1
COPY --from=base /lib/x86_64-linux-gnu/libexpat.so.1 /lib/x86_64-linux-gnu/libexpat.so.1
COPY --from=base /lib/x86_64-linux-gnu/libwebp.so.7 /lib/x86_64-linux-gnu/libwebp.so.7
COPY --from=base /lib/x86_64-linux-gnu/libXpm.so.4 /lib/x86_64-linux-gnu/libXpm.so.4
COPY --from=base /lib/x86_64-linux-gnu/libtiff.so.5 /lib/x86_64-linux-gnu/libtiff.so.5
COPY --from=base /lib/x86_64-linux-gnu/libbrotlidec.so.1 /lib/x86_64-linux-gnu/libbrotlidec.so.1
COPY --from=base /lib/x86_64-linux-gnu/libX11.so.6 /lib/x86_64-linux-gnu/libX11.so.6
COPY --from=base /lib/x86_64-linux-gnu/libzstd.so.1 /lib/x86_64-linux-gnu/libzstd.so.1
COPY --from=base /lib/x86_64-linux-gnu/libLerc.so.3 /lib/x86_64-linux-gnu/libLerc.so.3
COPY --from=base /lib/x86_64-linux-gnu/libjbig.so.0 /lib/x86_64-linux-gnu/libjbig.so.0
COPY --from=base /lib/x86_64-linux-gnu/libdeflate.so.0 /lib/x86_64-linux-gnu/libdeflate.so.0
COPY --from=base /lib/x86_64-linux-gnu/libbrotlicommon.so.1 /lib/x86_64-linux-gnu/libbrotlicommon.so.1
COPY --from=base /lib/x86_64-linux-gnu/libxcb.so.1 /lib/x86_64-linux-gnu/libxcb.so.1
COPY --from=base /lib/x86_64-linux-gnu/libXau.so.6 /lib/x86_64-linux-gnu/libXau.so.6
COPY --from=base /lib/x86_64-linux-gnu/libXdmcp.so.6 /lib/x86_64-linux-gnu/libXdmcp.so.6
COPY --from=base /lib/x86_64-linux-gnu/libbsd.so.0 /lib/x86_64-linux-gnu/libbsd.so.0
COPY --from=base /lib/x86_64-linux-gnu/libmd.so.0 /lib/x86_64-linux-gnu/libmd.so.0
COPY --from=base /lib/x86_64-linux-gnu/libxslt.so.1 /lib/x86_64-linux-gnu/libxslt.so.1
COPY --from=base /lib/x86_64-linux-gnu/libexslt.so.0 /lib/x86_64-linux-gnu/libexslt.so.0
COPY --from=base /lib/x86_64-linux-gnu/libgcrypt.so.20 /lib/x86_64-linux-gnu/libgcrypt.so.20
COPY --from=base /lib/x86_64-linux-gnu/libgpg-error.so.0 /lib/x86_64-linux-gnu/libgpg-error.so.0

# copy the files that nginx needs to run
COPY --from=base /var/lib/nginx/ /var/lib/nginx/
COPY --from=base /usr/lib/nginx/ /usr/lib/nginx/
COPY --from=base /usr/share/nginx/ /usr/share/nginx/
COPY --from=base /var/log/nginx/ /var/log/nginx/ 
COPY --from=base /etc/nginx/ /etc/nginx/
COPY --from=base /sbin/nginx /sbin/nginx


EXPOSE 8080
# no need to use the USER directive bc the nginx process already runs as a non-priviledged user and we have no shell
CMD ["/sbin/nginx","-g", "daemon off;"]
