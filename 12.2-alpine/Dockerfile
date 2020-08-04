FROM postgres:12.2-alpine

##
## Solution 1: 
## "Musl" has a limited set of locales (cs_CZ.UTF-8 locale is missing) and you can’t generate specific ones.
##
## locale
## locale -a
##

#ENV MUSL_LOCALE_DEPS cmake make musl-dev gcc gettext-dev libintl 
#ENV MUSL_LOCPATH /usr/share/i18n/locales/musl

#RUN apk add --no-cache \
#    $MUSL_LOCALE_DEPS \
#    && wget https://gitlab.com/rilian-la-te/musl-locales/-/archive/master/musl-locales-master.zip \
#    && unzip musl-locales-master.zip \
#      && cd musl-locales-master \
#      && cmake -DLOCALE_PROFILE=OFF -D CMAKE_INSTALL_PREFIX:PATH=/usr . && make && make install \
#      && cd .. && rm -r musl-locales-master





##
## Solution 2: 
## cs_CZ.UTF-8 sorting does not work :(
##
## https://github.com/sgerrand/alpine-pkg-glibc/
## Note that locale -a is not available in alpine linux, use `/usr/glibc-compat/bin/locale -a` instead
##

RUN echo "Locales" \
&&  wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
&&  wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.31-r0/glibc-2.31-r0.apk \
&&  wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.31-r0/glibc-bin-2.31-r0.apk \
&&  wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.31-r0/glibc-i18n-2.31-r0.apk \
&&  apk add \
        glibc-2.31-r0.apk \
        glibc-bin-2.31-r0.apk \
        glibc-i18n-2.31-r0.apk \
&&  ln -s /usr/glibc-compat/bin/locale /usr/local/bin \
&&  /usr/glibc-compat/bin/localedef -i cs_CZ -f UTF-8 cs_CZ.UTF-8

ENV LANG=cs_CZ.UTF-8
ENV LANGUAGE=
ENV LC_CTYPE=cs_CZ.UTF-8
ENV LC_NUMERIC=cs_CZ.UTF-8
ENV LC_TIME=cs_CZ.UTF-8
ENV LC_COLLATE=cs_CZ.UTF-8
ENV LC_MONETARY=cs_CZ.UTF-8
ENV LC_MESSAGES=cs_CZ.UTF-8
ENV LC_PAPER=cs_CZ.UTF-8
ENV LC_NAME=cs_CZ.UTF-8
ENV LC_ADDRESS=cs_CZ.UTF-8
ENV LC_TELEPHONE=cs_CZ.UTF-8
ENV LC_MEASUREMENT=cs_CZ.UTF-8
ENV LC_IDENTIFICATION=cs_CZ.UTF-8
ENV LC_ALL=
