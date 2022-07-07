# Docker SSH Tunnel

Create a lightweight Alpine Linux based SSH tunnel to a host. Uses pure SSH, no fluff.

## Versions

[![dockeri.co](http://dockeri.co/image/jujhars13/docker-ssh-tunnel)](https://hub.docker.com/r/jujhars13/docker-ssh-tunnel/)

- [`v1.8`, `latest` (_Dockerfile_)](https://github.com/jujhars13/docker-ssh-tunnel/blob/v1.8/Dockerfile) [![](https://images.microbadger.com/badges/image/jujhars13/docker-ssh-tunnel.svg)](http://microbadger.com/images/jujhars13/docker-ssh-tunnel "Get your own image badge on microbadger.com")
- [`v1.7`, `v1.7.2` (_Dockerfile_)](https://github.com/jujhars13/docker-ssh-tunnel/blob/v1.7/Dockerfile) [![](https://images.microbadger.com/badges/image/jujhars13/docker-ssh-tunnel.svg)](http://microbadger.com/images/jujhars13/docker-ssh-tunnel "Get your own image badge on microbadger.com")
- [`v1.6` (_Dockerfile_)](https://github.com/jujhars13/docker-ssh-tunnel/blob/v1.6/Dockerfile) [![](https://images.microbadger.com/badges/image/jujhars13/docker-ssh-tunnel.svg)](http://microbadger.com/images/jujhars13/docker-ssh-tunnel "Get your own image badge on microbadger.com")
- [`v1.5` (_Dockerfile_)](https://github.com/jujhars13/docker-ssh-tunnel/blob/v1.5/Dockerfile) [![](https://images.microbadger.com/badges/image/jujhars13/docker-ssh-tunnel.svg)](http://microbadger.com/images/jujhars13/docker-ssh-tunnel "Get your own image badge on microbadger.com")
- [`v1.4` (_Dockerfile_)](https://github.com/jujhars13/docker-ssh-tunnel/blob/v1.4/Dockerfile) [![](https://images.microbadger.com/badges/image/jujhars13/docker-ssh-tunnel.svg)](http://microbadger.com/images/jujhars13/docker-ssh-tunnel "Get your own image badge on microbadger.com")
- [`v1.3`, `v1.3.1` (_Dockerfile_)](https://github.com/jujhars13/docker-ssh-tunnel/blob/v1.3.1/Dockerfile) [![](https://images.microbadger.com/badges/image/jujhars13/docker-ssh-tunnel.svg)](http://microbadger.com/images/jujhars13/docker-ssh-tunnel "Get your own image badge on microbadger.com")
- [`v1.2` (_Dockerfile_)](https://github.com/jujhars13/docker-ssh-tunnel/blob/v1.2/Dockerfile) [![](https://images.microbadger.com/badges/image/jujhars13/docker-ssh-tunnel.svg)](http://microbadger.com/images/jujhars13/docker-ssh-tunnel "Get your own image badge on microbadger.com")
- [`v1.1` (_Dockerfile_)](https://github.com/jujhars13/docker-ssh-tunnel/blob/v1.1/Dockerfile) [![](https://images.microbadger.com/badges/image/jujhars13/docker-ssh-tunnel.svg)](http://microbadger.com/images/jujhars13/docker-ssh-tunnel "Get your own image badge on microbadger.com")
- [`v1.0` (_Dockerfile_)](https://github.com/jujhars13/docker-ssh-tunnel/blob/v1.0/Dockerfile) [![](https://images.microbadger.com/badges/image/jujhars13/docker-ssh-tunnel.svg)](http://microbadger.com/images/jujhars13/docker-ssh-tunnel "Get your own image badge on microbadger.com")

For single TCP port applications (database/webserver/debugging access) a SSH tunnel is far faster and simpler than using a VPN like OpenVPN; see this excellent [blog post](https://blog.backslasher.net/ssh-openvpn-tunneling.html) for more info.

For example I use it to create a SSH tunnel from a GCP Kubernetes cluster into an on prem bastion host in order to talk to an on prem MySQL database; it SSHs onto the internal LAN and connects me to the internal on prem MySQL server.

Inspired by https://github.com/iadknet/docker-ssh-client-light and [GCP CloudSQL Proxy](https://cloud.google.com/sql/docs/mysql/sql-proxy)

## Required Parameters

```bash
# local port on your machine/k8s cluster
LOCAL_PORT=3306

# remote port from the machine your SSHing into
REMOTE_PORT=3306

# OPTIONAL defaults to 127.0.0.1
REMOTE_SERVER_IP="my.internal.mariadb.server"

# the bastion/host you're connecting to
SSH_BASTION_HOST="bastion.host"

# OPTIONAL defaults to 22
SSH_PORT=2297

SSH_USER="tunnel_user"

SSH_PASS="tunnel_pass"

```

Also be sure to inject/mount your private ssh key into the container to `/ssh_key/id_rsa`

## Example

```bash
# connect to our mongo server in AWS via a bastion host
# now we can use a connection string like this:
# mongodb://localhost:27017
# to talk to our AWS mongo install

docker run -it --rm \
-p 5432:5432 \
-e LOCAL_PORT=5432 \
-e REMOTE_PORT=5432 \
-e SSH_BASTION_HOST=IP_BASTION \
-e REMOTE_SERVER_IP=DNS_RDS_AWS \
-e SSH_USER=ec2-user \
-e SSH_PASS=YOUR_PASSWORD \
jujhars13/docker-ssh-tunnel

# connection established, now we can postgresql on localhost

```

## TODO

- [x] add example `docker-compose.yml` to `/examples`

## Version

- 2022-07-07 - `v1.9`
