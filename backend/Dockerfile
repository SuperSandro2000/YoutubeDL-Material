FROM alpine:3.12

ENV UID=1000 GID=1000
RUN export user=youtube \
  && addgroup -S $user -g $GID && adduser -D -S $user -G $user -u $UID
USER $user

RUN apk add --no-cache \
    ffmpeg \
    npm \
    python2 \
    su-exec  \
  && apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing/ \
    atomicparsley

WORKDIR /app

COPY --chown=$UID:$GID [ "package.json", "package-lock.json", "/app/" ]
RUN npm install

COPY --chown=$UID:$GID [ "./", "/app/" ]

EXPOSE 17442
ENTRYPOINT [ "/app/entrypoint.sh" ]
CMD [ "node", "app.js" ]
