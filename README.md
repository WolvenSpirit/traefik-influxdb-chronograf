#### Example deployment: Traefik (load-balancer and reverse-proxy), InfluxDB, Chronograf, Grafana
### Important
- Please make sure all of the declared ports in the docker-compose.yml and configuration files are open.
- To query InfluxDB from the terminal please install influxdb-client - it can be installed via `apt-get -y influxdb-client` on Debian systems.
- The docker.sock needs to be mounted so that Traefik can monitor it.
- In this example InfluxDB monitors only the connections with Traefik on UDP but it exposes the API and it can log anything else also.

Chronograf exposed Admin interface:
`http://localhost:8888/sources/0/chronograf/data-explorer`

Traefik exposed Admin interface:
`http://localhost:8080/dashboard/#/`

Grafana:
`http://localhost:3000`

User: admin, Password: admin

Set up InfluxDB as source from Grafana admin:
- Host: http://tsdb:8086
- No auth required

Simple deploy (recommended):
`docker-compose up -d` 

Shut down the stack:
`docker-compose down`

----------------------------

Create a simple swarm https://docs.docker.com/engine/reference/commandline/swarm_init/
Swarm mode doesn't work if docker was installed sandboxed by Snap.
`docker swarm init`

Enable `swarmMode = true` in traefik.toml

With Swarm mode enabled:
`docker stack deploy -c my-stack`

Remove deployed stack:
`docker stack rm my-stack`

To check stack status:
`docker stack ps my-stack`