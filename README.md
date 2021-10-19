# Add Redis password

Please after checkout run once the gen-redis-password.sh to generate a random password for redis, and setup in both redis config and edumeet config.
# eduMeet in docker container

Docker hub repository: [edumeet/edumeet](https://hub.docker.com/r/edumeet/edumeet)

This is the container, or a "dockerized" version of the [eduMeet](https://github.com/edumeet/edumeet).
(Successor of [multiparty meeting](https://github.com/havfo/multiparty-meeting) fork of mediasoup-demo)

## Run it in few easy step

1. Git clone this code to your docker machine.
2. Copy your cert in `certs/cert.pem` and `certs/privkey.pem`
    1. In case you need to generate a new cert and private key, you can use (note -nodes flag, which allows to generate unencrypted private key)

```sh
        $ openssl req -x509 -newkey rsa:4096 -keyout privkey.pem -out cert.pem -days 365 -nodes
```

3. **Recomended**: set TURN server and credential in `configs/server/config.js`
    1. In case you are using coturn, you can generate a user and key with

```sh
        $ turnadmin -k -u <username> -p <password>
```

Placeholder looks like

```js
	turnServers     : [
		{
			urls : [
				'turn:example.com:443?transport=tcp'
			],
			username   : 'example',
			credential : 'example'
		}
  ]
```

You would need to replace example.com by your IP or domain, add the username previously used `<username>` and credential is the code generated by the above mentioned command.

4. **Optional:** Change other stuff in config:
    1. **Optional:** replace logo/logo.svg with your company logo svg.
    2. **Optional:** sort audio/video codecs according to preference.

## Run

Run with `docker-compose` 
/ [install docker compose](https://docs.docker.com/compose/install/) /

```sh
  $ sudo docker-compose up --detach
```

## Rebuild

If you change .env then you have to rebuild the image.

```sh
  $ sudo docker-compose up --build --detach
```

## Docker networking

Container works in "host" network mode, because birdge mode has the following issue

[Docker - Docker hangs when attempting to bind a large number of ports] (https://success.docker.com/article/docker-compose-and-docker-run-hang-when-binding-a-large-port-range)

## Further Informations

Read more about configs and settings in [eduMeet](https://github.com/edumeet/edumeet) README.
