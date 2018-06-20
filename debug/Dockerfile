FROM zenika/alpine-maven:latest

RUN apk add --update curl bash \
&& rm -rf /var/cache/apk/*

WORKDIR /app
ADD . /app

RUN curl -L https://github.com/metafacture/metafacture-core/releases/download/metafacture-core-5.0.0/metafacture-core-5.0.0-dist.tar.gz \
2> /dev/null \
| tar -xz
RUN mv metafacture-core-5.0.0-dist/* . && rmdir metafacture-core-5.0.0-dist
RUN sed -i '13s/info/debug/' config/log4j.xml
ENV MFRUNNER /app

RUN mkdir /mfwf /in /out
VOLUME /app/plugins /mfwf /in /out
WORKDIR /mfwf
EXPOSE 50505

ENTRYPOINT ["/bin/bash", "/app/flux.sh"]
CMD ["indir=/in", "outdir=/out"]
