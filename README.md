# Radicale-Docker

Simple dockerization of the [Radicale](https://radicale.org/2.1.html) CalDav/CardDav server

## Setup

*Variables*
* `$RADICALE_DIR`: Folder on host file system where radicale related stuff will be stored
* `$PORT`: Exposed port on host machine

Build the image
```bash
docker build -t radicale:latest .
```

Copy the config from this repository to `$RADICALE_DIR`
```
cp config.ini $RADICALE_DIR
```

Run it
```bash
docker run \
    -d \
    --restart unless-stopped
    -v $RADICALE_DIR:/srv/radicale \
    -p $PORT:5232 \
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
