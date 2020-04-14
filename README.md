# Traefik Docker boilerplate
## Example how to run Traefik reverse proxy with Let's Encrypt DNS checker on DigtalOcean

### Follow these steps:

1. First of all create external docker network: `docker network create web`
2. Generate Personal access token at https://cloud.digitalocean.com/account/api/tokens in your account
3. Replace xxx with your access tokern in docker-compose.yml - "DO_AUTH_TOKEN=xxx"
4. Make sure your domain/subdomain A record set to the server where traefik will be installed
5. Replace `example.com`in `"traefik.http.routers.api.rule=Host(`traefik.<example.com>`)"` with your domain. This subdomain will be used for services monitoring.
6. Run:
```bash 
echo $(htpasswd -nb admin password) | sed -e s/\\$/\\$\\$/g
```
use your values instead of `admin` & `password`. Then copy outputted value to `"traefik.http.middlewares.auth.basicauth.users=admin:$$apr1$$7P/yeHno$$AV6pmR7SRanY.zpn/vPfO."` instead of `admin:$$apr1$$7P/yeHno$$AV6pmR7SRanY.zpn/vPfO.`
7. Set rights 600 to acme.json with command:
```bash
chmod 600 acme.json
```

8. To start traefik, run:

```bash
docker-compose up -d
``` 

Now you ready yo start your services, and traefik will create SSL Let's Encrypt cert for tyour services.

8. Create your service docker-compose.yml file. Use example from whoami folder (Thisfolder can be removed, used only as service example)
Replace `example.com` to your domain in `- "traefik.http.routers.whoami.rule=Host(`example.com`)"`

Run service, wait few seconds and youare ready!

Good luck 
