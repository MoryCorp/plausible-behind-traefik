
# Plausible.io behind Traefik 2

Hello everyone, I created this repository to show you how to run **Plausible.io** with **Traefik** as a **reverse-proxy**. This will let you have a **SSL certificate** on your **self-hosted** instance.

The official documentation on which you have to rely to configure the different files is available at this address: https://docs.plausible.io/self-hosting

> If you want to host your Plausible.io instance but you don't have a Traefik container yet, you can use this repository that I have created and tested with Plausible.io and other services : https://github.com/MoryCorp/traefik2-minimalist-configuration

## Edit docker-compose.yml

This configuration assumes that you already have a Traefik instance configured with an **entrypoint** named **"websecure"** on port **443**.

If this is the case, the only thing you will have to edit is **line 41** of the docker-compose-.yml file, to put your domain name or sub-domain instead of "yourdomain.com".

The networks are configured so that only the plausible.io instance is exposed via Traefik. **Databases are not exposed** thanks to the "internal" network which is set to "external: false".

## Edit plausible-conf.env

There is not much to say about this file as it is quite simple to configure.
To generate a secret key, you can use the command : ``openssl rand -base64 64``

Add **"https://"** before your domain when you fill the **"BASE_URL"** parameter or the default value will override yours.

Example: ``BASE_URL=https://analytics.yourdomain.com``

## Edit geoip-conf.env

In order to run the GeoIP service and display the country of your visitors, you will need to create a free account on maxmind.com and generate an API key.

Once you have created your account, go to the "My License Key" page and generate one.
Put down your "Account/User ID" and your "License key" in geoip-conf.env 

![enter image description here](https://i.imgur.com/Z6aQoYO.png)
