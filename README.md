# Radicale-Docker

Simple dockerization of the [Radicale](https://radicale.org/2.1.html) CalDav/CardDav server

## Setup

Clone the repo and build the image
```bash
git clone https://github.com/Potatochurchman/radicale-docker.git
docker build -t radicale:latest .
```

Copy the config from this repository to `$RADICALE_DIR`
```
cp config.ini /srv/radicale
```

Run it
```bash
docker run \
    -d \
    --restart unless-stopped
    -v /srv/radicale:/srv/radicale \
    -p 5232:5232 \
    --name radicale \
    radicale:latest
```

## Create accounts

```
sudo htpasswd -B /srv/radicale/users $USERNAME
```

## Create radicale system user and change permissions

```
sudo adduser --gid 2999 --uid 2999 --shell /bin/false --disabled-password --no-create-home radicale
sudo chown -R radicale:radicale /srv/radicale
sudo chmod 0600 /srv/radicale/users
```
