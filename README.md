# XDGFX / docker-compose
This is my WIP custom docker-compose. Feel free to use bits from it, or copy the whole thing. Some containers might not work straight off the bat and may require referral to tutorials - e.g. `guacamole` and `traefik-forward-auth`.

## Basic Setup
Traefik works as a reverse proxy to all apps that require it. It's using HTTPS on my own custom domain. I would recommend you follow the tutorial I did [here](https://www.smarthomebeginner.com/traefik-reverse-proxy-tutorial-for-docker/), to make sure you set everything up correctly.

Authentication is done using [thomseddon/traefik-forward-auth](https://github.com/thomseddon/traefik-forward-auth). It authenticates users with their Google account. It took me a while to get this working properly but hopefully my setup is fairly transferrable. Refer back there if you get stuck. I'm using auth mode. 

The main network is traefik_proxy. Using the default network (by not specifying the traefik_proxy network) means they won't be proxied, and they can't communicate with containers only inside traefik_proxy network.

See **Credentials** for info about environment variables

## Containers Included

#### General Networking / Access / Control
- `Traefik v1.7` - *Reverse proxy*
- `thomseddon/traefik-forward-auth` - *Authentication for reverse proxy*
- `guillaumebriday/traefik-custom-error-pages` - *Makes errors slightly more fun*
- `portainer/portainer` - *For managing all the containers*
- `watchtower` - *Automatically updates containers*
- `mariadb` - *Database app, currently only used for Guacamole*
- `adminer` - *Database management. Lighter than phpMyAdmin*

#### Server Remote Access
- `guacamole/guacd` - *The backend for guacamole*
- `guacamole/guacamole` - *The web app for guacamole*

#### Media Server
- `linuxserver/tautulli` - *Plex server monitoring*
- `linuxserver/deluge` - *Torrent client*

## Credentials
All credentials are stored separately in `.env`

The folder structure is

```
docker/
├── docker-compose.yml
├── .env
├── traefik/
├── shared/
└── ... etc
```

`.env` should contain the following:

```
MYSQL_PASSWORD=XXXXX
TRAEFIK_CLIENT_ID=XXXXX
TRAEFIK_CLIENT_SECRET=XXXXX
TRAEFIK_SECRET=XXXXX
TRAEFIK_WHITELIST=example@example.com
DELUGE_TORRENTS_DIR=/example/directory/torrents
DELUGE_DOWNLOADS_DIR=/example/directory/downloads
```
