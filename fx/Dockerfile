FROM alpine:latest

ARG MYSQL_USER
ARG MYSQL_PASSWORD
ARG MYSQL_DB
ARG MYSQL_HOST
ARG RCON_PASS
ARG BANNER_DETAIL
ARG BANNER_CONNECTING
ARG SV_HOSTNAME
ARG STEAM_KEY
ARG SV_MAXCLIENTS
ARG ADMIN_ID
ARG SV_LICENSEKEY
ARG FX_VER

RUN apk update && apk upgrade && \
    apk add nodejs-npm \
    ca-certificates \
    curl \
    gettext \
    git

RUN mkdir -p /srv

WORKDIR /srv

RUN curl https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/3456-35a48b6a57d995930d87ad969b075fe50ed70ad6/fx.tar.xz | tar xJ -C /srv

RUN mkdir -p /srv/resources

COPY "./resources/package.json" /srv/resources/package.json

RUN cd /srv/resources && npm install

COPY template.server.cfg .

RUN envsubst < template.server.cfg > server.cfg

COPY ./wait .

RUN chmod +x ./wait

CMD ./wait && sh /srv/run.sh

