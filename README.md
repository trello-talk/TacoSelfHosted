# Taco Self-Hosted
This is an easy way to start an instance of Taco for yourself. Make sure that you change the branding for your own self-hosted instance for your own usage.

> **Note** Please do not host Taco as a public listed bot. This is meant for private use for servers that need a self-hosted solution.

## Quick Start
You will need a Trello account that the bot will control in order to use Trello's API. I recommend creating a new account for this as your API key is tied to your account. You can find your API key and OAuth secret [here](https://trello.com/app-key).
> **Warning** You can't regenerate or change the API key or OAuth secret. Make sure these variables are secure.

```sh
# Clone repo
git clone https://github.com/trello-talk/TacoSelfHosted taco
cd taco

# Copy the env files and fill out the variables
cp api.env.example api.env
cp auth.env.example auth.env
cp interactions.env.example interactions.env
cp ws.env.example ws.env

# Pull and start services
docker-compose up -d
```

| Service                | Port   |
|:-----------------------|:------:|
| Webhook API            | `3000` |
| Authentication Service | `8001` |
| Interactions           | `8020` |

Make sure to configure your URLs properly. `WEBHOOK_BASE_URL` in `interactions.env` must end with a slash!

## Updating Services
You can update and restart services by pulling and restarting the containers:
```sh
docker-compose pull
docker-compose up -d
```

## Notes

##### Expose database
You can expose the database with this override:
```yml
# docker-compose.override.yml
services:
  postgres:
    ports:
      - "5432:5432"
```

##### Use master images
You can use the latest built images from the master branches with this override:
```yml
# docker-compose.override.yml
services:
  interactions:
    image: ghcr.io/trello-talk/tacointeractions:master
  ws:
    image: ghcr.io/trello-talk/tacows:master
  webhookapi:
    image: ghcr.io/trello-talk/webhookapi:master
  auth:
    image: ghcr.io/trello-talk/tacoauth:master
```
