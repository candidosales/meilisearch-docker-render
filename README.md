# meilisearch-docker-render

Deploy Meilisearch to render.com and fly.io

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy)

## Environment Variables

- `MEILI_HTTP_ADDR` -- the address you want your Meilisearch server to run on. (Default = `0.0.0.0:80`)
- `MEILI_MASTER_KEY` -- the master key (Default = `{randomly_generated_key}`)
- `MEILI_DB_PATH` -- where we want to persist the data. Probably don't need to change this, as it's also in the render.yaml (Default = `/meili-data`)
- `MEILI_ENV` -- environemnt level. Options are `development` or `production`. (Default = `development`)

See full list of options you can configure [here](https://www.meilisearch.com/docs/learn/configuration/instance_options)

## Run locally

Install Docker Desktop

https://docs.docker.com/get-docker/

Build the image

```bash
docker build -t meilisearch .
```

Launch a container

```bash
docker run --env MEILI_MASTER_KEY=0xIMnKxGoGmSx0u3cBXKCjvhuFDfnul4 -p 7700:7700 -d meilisearch
```

## Deploy fly.io

```bash
## Create a new app
fly launch

## Deploy or update for the new version
fly deploy
```

Reference: https://dev.to/jakovglavac/deploy-meilisearch-on-flyio-p89

## Deploy in fly.io

It always is a problem because the database version is not compatible with the engine version. So, I delete the volume and recreate it.

```bash
gru [info]2025-10-25T19:54:19.707867Z ERROR meilisearch: error=Your database version (1.15.1) is incompatible with your current engine version (1.24.0).
2025-10-25T19:54:19Z app[d8d9e17b2e3768] gru [info]To migrate data between Meilisearch versions, please follow our guide on https://www.meilisearch.com/docs/learn/update_and_migration/updating.
2025-10-25T19:54:19Z app[d8d9e17b2e3768] gru [info]Error: Your database version (1.15.1) is incompatible with your current engine version (1.24.0).
2025-10-25T19:54:19Z app[d8d9e17b2e3768] gr
```