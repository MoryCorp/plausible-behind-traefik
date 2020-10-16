# Plausible.io behind Traefik

Hello everyone, I created this repository to show you how to run **Plausible.io** with **Traefik** as a **reverse-proxy**. This will let you have a **SSL certificate** on your **self-hosted** instance.

The official documentation on which you have to rely to configure the different files is available at this address: https://docs.plausible.io/self-hosting

## Edit docker-compose.yml

This configuration assumes that you already have a Traefik instance configured with an **entrypoint** named **"websecure"** on port **443**.

If this is the case, the only thing you will have to edit is **line 41** of the docker-compose-.yml file, to put your domain name or sub-domain instead of "yourdomain.com".

The networks are configured so that only the plausible.io instance is exposed via Traefik. **Databases are not exposed** thanks to the "internal" network which is set to "external: false".

## Edit plausible-conf.env

There is not much to say about this file as it is quite simple to configure.
To generate a secret key, you can use the command : ``openssl rand -base64 64``

Add **"https://"** before your domain when you fill the **"BASE_URL"** parameter or the default value will override yours.

Example: ``BASE_URL=https://analytics.yourdomain.com``
