# vaultstack

compose project for HA consul + vault + nginx

dockerhub images acker/consul acker/vault built from local dirs.

## setup

- export env var COMPOSE_PROJECT_NAME or pass `-p <name>` to docker-compose

- `docker-compose --x-networking -x-network-driver -p <name> up -d`

- as of compose-1.6.0 and engine-1.9 order containers are brought up
  is non-deterministic, so a `docker-compose restart <comp>` may be helpful

- monitor progress with `docker-compose logs`, once consul cluster is
  sync'd, export env var `VAULT_ADDR=http://<ip-of-nginx>:8200` and
  run the following

- `vault status` to ensure HA is enabled and cluster is in initial state.

- `vault init | tee /some/place/safe` to generate keyset

- target each vault container and unseal each via
  `docker exec -it vault0 env VAULT_ADDR=http://localhost:8200 vault unseal <key>`



## caveats

- persistent volumes can be enabled (just uncomment volumes section),
  but will need to be cleared out across cluster instances. eg. consul
  data will likely not carry over consul restarts. (might be a bug
  here?)

- no ssl baked in yet, salt the nginx Dockerfile to taste (the nginx
  component is intentionally built with `docker-compose build` for
  this purpose)
