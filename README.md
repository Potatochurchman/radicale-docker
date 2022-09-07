# Radicale-Docker

Simple dockerization of the [Radicale](https://radicale.org/2.1.html) CalDav/CardDav server

## Setup

Clone the repo and copy additional files
```bash
git clone https://github.com/Potatochurchman/radicale-docker.git && cd radicale-docker
sudo mkdir /srv/radicale && sudo cp config.ini /srv/radicale
scp -P 69 -r /srv/radicale/collections/ user@NEW-SERVER-IP:/srv/radicale/collections # only if a previous calendar exists
```

Create accounts

```bash
sudo htpasswd -cB /srv/radicale/users [USER]
```

Create radicale system user and change permissions

```bash
sudo groupadd -r -g 2999 radicale
sudo adduser --gid 2999 --uid 2999 --shell /bin/false --disabled-password --no-create-home radicale
sudo chown -R radicale:radicale /srv/radicale
sudo chmod 0600 /srv/radicale/users
```

## Build and run the container
```bash
sudo docker build -t radicale:latest .
```

```bash
sudo docker run \
    -d \
    --restart unless-stopped \
    -v /srv/radicale:/srv/radicale \
    -p 5232:5232 \
    --name radicale \
    radicale:latest
```
