FROM openjdk:8-jdk

ARG user=minecraft
ARG group=minecraft
ARG uid=1001
ARG gid=1001
RUN groupadd -g ${gid} ${group} \
    && useradd -d /minecraft -u ${uid} -g ${gid} -m -s /bin/bash ${user}
RUN apt-get update && apt-get install -y rsync && rm -rf /var/lib/apt/lists/*

VOLUME /minecraft
COPY assets /assets
RUN chown -R ${user}:${group} /assets
EXPOSE 25565
USER ${user}
WORKDIR /minecraft

CMD rsync -a /assets/* /minecraft && java -Xmx3G -Xms3G -Dfml.queryResult=confirm -jar forge-1.12.2-14.23.2.2611-universal.jar nogui
