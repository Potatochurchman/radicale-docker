# Radicale-Docker

Simple dockerization of the [Radicale](https://radicale.org/2.1.html) CalDav/CardDav server

## Setup

Clone the repo and copy the config
```bash
git clone https://github.com/Potatochurchman/radicale-docker.git && cd radicale-docker
cp config.ini /srv/radicale
```

Create accounts

```bash
sudo htpasswd -B /srv/radicale/users $USERNAME
```

Create radicale system user and change permissions

```bash
sudo adduser --gid 2999 --uid 2999 --shell /bin/false --disabled-password --no-create-home radicale
sudo chown -R radicale:radicale /srv/radicale
sudo chmod 0600 /srv/radicale/users
```

## Build and run the container
```bash
docker build -t radicale:latest .
```
```bash
docker run \
    -d \
    --restart unless-stopped
    -v /srv/radicale:/srv/radicale \
    -p 5232:5232 \
    --name radicale \
    radicale:latest
```
