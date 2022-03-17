# caddy-fastapi ⛳

This is a template repo to deploy [Caddy](https://caddyserver.com/) + [FastAPI](https://fastapi.tiangolo.com/) with docker-compose

## Usage 🔨

To use this repo simply do the following:

1. Clone the repo
1. Run the following command:

    ```bash
    docker-compose up --build
    ```

1. Navigate to your domain: [localhost](https://localhost:443/)

That's it!

## TLS Certificate 🔐

Caddy automatically provisions TLS certificates for you. In order to make use of this awesome feature, do the following:

1. Ensure your server has ports `80` and `443` open
1. Have a DNS record pointed to your server for the domain you wish to obtain a certificate for (e.g. `app.example.org` -> `<IP address>`)
1. Export the env var for the domain you wish to use:

    ```bash
    export DOMAIN=app.example.org
    ```

1. Start the docker-compose stack:

   ```bash
   docker-compose up --build
   ```

1. Navigate to your domain and enjoy your easy TLS setup with Caddy! -> [https://app.example.org](https://app.example.orgg)

## Extra Info 📚

Here is some extra info about the setup

### Volumes 🛢️

The docker-compose file creates two volumes:

- `./data/caddy_data:/data`
- `./data/caddy_config:/config`

The config volume is used to mount Caddy configuration

The data volume is used to store certificate information. This is really important so that you are not re-requesting TLS certs each time you start your container. Doing so can cause you to hit Let's Encrypt rate limits that will prevent you from provisioning certificates.

### Environment Variables 📝

If you run the stack without the `DOMAIN` variable set in your environment, the stack will default to using `localhost`. This is ideal for testing out the stack locally.

If you set the `DOMAIN` variable, Caddy will attempt to provision a certificate for that domain. In order to do so, you will need DNS records pointed to that domain and you will need need traffic to access your server via port `80` and `443`.

### Disclaimer

This repo is extremely simple on purpose. You should tailor this to your needs if you plan on adapting it for production usage of any kind.
