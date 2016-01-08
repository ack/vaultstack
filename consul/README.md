

# standalone mode
`docker run --rm -it acker/consul -bootstrap -config-file=/config/server.json`

# run server with auto-join
`docker run --rm -it -e CONSUL_SERVERS=c01,c02,c03 acker/consul -config-file=/config/server.json`

# agent with auto-join
`docker run --rm -it -e CONSUL_SERVERS=c01,c02,c03 acker/consul -config-file=/config/agent.json`
