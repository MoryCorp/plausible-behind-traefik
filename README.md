
# Plausible.io behind Traefik

Hello everyone, I created this repository to show you how to run **Plausible.io** with **Traefik** as a **reverse-proxy**. This will let you have a **SSL certificate** on your **self-hosted** instance.

The official documentation on which you have to rely to configure the different files is available at this address: https://docs.plausible.io/self-hosting

> If you want to host your Plausible.io instance but you don't have a Traefik container yet, you can use this repository that I have created and tested with Plausible.io and other services : https://github.com/MoryCorp/traefik2-minimalist-configuration

## Edit docker-compose.yml

This configuration assumes that you already have a Traefik instance configured with an **entrypoint** named **"websecure"** on port **443**.

If this is the case, the only thing you will have to edit is **line 49** of the docker-compose-.yml file, to put your domain name or sub-domain instead of "yourdomain.com" and the **.env** file to modify variables.

The networks are configured so that only the plausible.io instance is exposed via Traefik. **Databases are not exposed** thanks to the "internal" network which is set to "external: false".

## Edit .env

There is not much to say about this file as it is quite simple to configure.  
To generate a secret key, you can use the command : ``openssl rand -base64 64``

Add **"https://"** before your domain when you fill the **"BASE_URL"** parameter or the default value will override yours.

Example : ``BASE_URL=https://analytics.yourdomain.com``  
Also change the ``POSTGRES_PASSWORD=xxxx`` with a strong password

## Tips & tricks

I noticed that **uBlock Origin** web extension often blocked the loading of my plausible scripts.  
On closer inspection, some of the uBlock filters are based on the words "data" "analytics" and other words related to data collection.  
If these words are part of your domain or sub-domain, then your script may be blocked and you may not be able to collect data.  

I therefore advise you to use a sub-domain that has nothing to do with analytics vocabulary.  
You can for example use Greek or Roman God names like: zeus.yourdomain.com
