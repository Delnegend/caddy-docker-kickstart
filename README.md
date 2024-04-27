# Caddy-Docker kickstart
Basic Docker setup of Caddy

# Highlights
- No custom image (just the base `alpine` image)
- Pre-config wildcard TLS (one certificate for all subdomain of a domain)
- Bring your own binary, no DNS provider lock-in

# Usage

- Clone/download this repository

## A. Config
1. Customize the plugin and download the Caddy binary from the [download page](https://caddyserver.com/download), rename to `caddy` and place into this directory
2. Modify `DNS_PROVIDER` and `DNS_PROVIDER_TOKEN` inside `docker-compose.yml`
3. Modify `example.com` in `Caddyfile` to your domain

## B. Networking
1. Create a docker network (if you haven't)
    ```bash
    docker network create web
    ```
    > `web` is the name of the network, use anything you like, but remember to change accordingly in the `docker-compose.yml` file
2. Add other containers to use the network
    ```yml
    services:
        service_name:
            # ...
            networks:       # +
                - web       # +
            # ...
    
    networks:               # +
        web:                # +
            name: web       # +
            external: true  # +
    ```
    >
# C. Spin up
```bash
docker compose up -d
```
