FROM acker/consul

ENV VAULT_VERSION 0.4.0
ADD https://releases.hashicorp.com/vault/${VAULT_VERSION}/vault_${VAULT_VERSION}_linux_amd64.zip /tmp/vault.zip
RUN cd /bin && unzip /tmp/vault.zip && chmod +x /bin/vault && rm /tmp/vault.zip

ADD vault.hcl /config/

ADD start.vault /bin/start.vault

ENTRYPOINT ["/bin/start.vault"]
