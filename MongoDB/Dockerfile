FROM debian:buster AS Build

RUN apt-get update -y
RUN apt-get install -y git python3-pip build-essential libcurl4-openssl-dev libssl-dev
RUN mkdir /app
WORKDIR /app
RUN git clone https://github.com/mongodb/mongo.git .
RUN git checkout r4.2.8
RUN pip3 install -r etc/pip/compile-requirements.txt
RUN python3 buildscripts/scons.py mongod

FROM debian:buster
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

COPY --from=Build /app/mongod /usr/bin/mongod 

#... 25 minutes later ...
#Install file: "build/opt/mongo/mongod" as "mongod"
#scons: done building targets.

#$ build/opt/mongo/mongod --version
#db version v4.2.8
#git version: 43d25964249164d76d5e04dd6cf38f6111e21f5f
#allocator: system
#modules: none
#build environment:
#    distarch: x86_64
#    target_arch: x86_64 

# ldd mongod
        # linux-vdso.so.1 (0x00007fffa8174000)
        # libcurl.so.4 => /usr/lib/x86_64-linux-gnu/libcurl.so.4 (0x00007f2eaa358000)
        # libresolv.so.2 => /lib/x86_64-linux-gnu/libresolv.so.2 (0x00007f2eaa33e000)
        # libcrypto.so.1.1 => /usr/lib/x86_64-linux-gnu/libcrypto.so.1.1 (0x00007f2eaa055000)
        # libssl.so.1.1 => /usr/lib/x86_64-linux-gnu/libssl.so.1.1 (0x00007f2ea9fc3000)
        # libdl.so.2 => /lib/x86_64-linux-gnu/libdl.so.2 (0x00007f2ea9fbe000)
        # librt.so.1 => /lib/x86_64-linux-gnu/librt.so.1 (0x00007f2ea9fb4000)
        # libstdc++.so.6 => /usr/lib/x86_64-linux-gnu/libstdc++.so.6 (0x00007f2ea9e2e000)
        # libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007f2ea9cab000)
        # libgcc_s.so.1 => /lib/x86_64-linux-gnu/libgcc_s.so.1 (0x00007f2ea9c91000)
        # libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007f2ea9c70000)
        # libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f2ea9aaf000)
        # libnghttp2.so.14 => /usr/lib/x86_64-linux-gnu/libnghttp2.so.14 (0x00007f2ea9a87000)
        # libidn2.so.0 => /usr/lib/x86_64-linux-gnu/libidn2.so.0 (0x00007f2ea9a66000)
        # librtmp.so.1 => /usr/lib/x86_64-linux-gnu/librtmp.so.1 (0x00007f2ea9849000)
        # libssh2.so.1 => /usr/lib/x86_64-linux-gnu/libssh2.so.1 (0x00007f2ea981b000)
        # libpsl.so.5 => /usr/lib/x86_64-linux-gnu/libpsl.so.5 (0x00007f2ea9808000)
        # libgssapi_krb5.so.2 => /usr/lib/x86_64-linux-gnu/libgssapi_krb5.so.2 (0x00007f2ea97bb000)
        # libkrb5.so.3 => /usr/lib/x86_64-linux-gnu/libkrb5.so.3 (0x00007f2ea96db000)
        # libk5crypto.so.3 => /usr/lib/x86_64-linux-gnu/libk5crypto.so.3 (0x00007f2ea96a5000)
        # libcom_err.so.2 => /lib/x86_64-linux-gnu/libcom_err.so.2 (0x00007f2ea969f000)
        # libldap_r-2.4.so.2 => /usr/lib/x86_64-linux-gnu/libldap_r-2.4.so.2 (0x00007f2ea964b000)
        # liblber-2.4.so.2 => /usr/lib/x86_64-linux-gnu/liblber-2.4.so.2 (0x00007f2ea963a000)
        # libz.so.1 => /lib/x86_64-linux-gnu/libz.so.1 (0x00007f2ea941c000)
        # /lib64/ld-linux-x86-64.so.2 (0x00007f2eadf72000)
        # libunistring.so.2 => /usr/lib/x86_64-linux-gnu/libunistring.so.2 (0x00007f2ea9296000)
        # libgnutls.so.30 => /usr/lib/x86_64-linux-gnu/libgnutls.so.30 (0x00007f2ea90e9000)
        # libhogweed.so.4 => /usr/lib/x86_64-linux-gnu/libhogweed.so.4 (0x00007f2ea90b0000)
        # libnettle.so.6 => /usr/lib/x86_64-linux-gnu/libnettle.so.6 (0x00007f2ea9078000)
        # libgmp.so.10 => /usr/lib/x86_64-linux-gnu/libgmp.so.10 (0x00007f2ea8ff5000)
        # libgcrypt.so.20 => /lib/x86_64-linux-gnu/libgcrypt.so.20 (0x00007f2ea8ed7000)
        # libkrb5support.so.0 => /usr/lib/x86_64-linux-gnu/libkrb5support.so.0 (0x00007f2ea8ec6000)
        # libkeyutils.so.1 => /lib/x86_64-linux-gnu/libkeyutils.so.1 (0x00007f2ea8ebf000)
        # libsasl2.so.2 => /usr/lib/x86_64-linux-gnu/libsasl2.so.2 (0x00007f2ea8ea2000)
        # libp11-kit.so.0 => /usr/lib/x86_64-linux-gnu/libp11-kit.so.0 (0x00007f2ea8d73000)
        # libtasn1.so.6 => /usr/lib/x86_64-linux-gnu/libtasn1.so.6 (0x00007f2ea8b60000)
        # libgpg-error.so.0 => /lib/x86_64-linux-gnu/libgpg-error.so.0 (0x00007f2ea8b3b000)
        # libffi.so.6 => /usr/lib/x86_64-linux-gnu/libffi.so.6 (0x00007f2ea8b31000)