# usable for either server or agent
FROM acker/alpine

RUN apk -U add curl bash netcat-openbsd unzip

ENV CONSUL_VERSION 0.6.3
ADD https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip /tmp/consul.zip
RUN cd /bin && unzip /tmp/consul.zip && chmod +x /bin/consul && rm /tmp/consul.zip

ADD https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_web_ui.zip /tmp/ui.zip
RUN cd /tmp && unzip -d ui ui.zip && mv ui /ui && rm ui.zip

# comma-separated hostnames of consul servers
ENV CONSUL_SERVERS ''

ADD server.json /config/
ADD agent.json /config/

ADD start.consul /bin/start.consul

ENTRYPOINT ["/bin/start.consul"]
