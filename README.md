# the.open.source.college Docker Compose

This docker compose will allow anyone to run the.open.source.college in their local machine for testing, debugging components and demo. The technology stack used to build this applications are,

* Strapi as CMS
* MongoDb for Strapi data persistence 
* Node JS for application services and proxy
* Gatsby for static wesite
* React JS for web application
* Keycloak for authentication and authorization
* MySQL for Keycloak data persistence

## 1. Before running

Before running docker-compose up make sure to create a .env file with the following attributes,

```
# For portal cms
DATABASE_CLIENT=mongo
DATABASE_NAME=<db name>
DATABASE_HOST=toscdb
DATABASE_PORT=<mongo db port>
DATABASE_USERNAME=<username>
DATABASE_PASSWORD=<password>

# For mongo db
MONGO_INITDB_ROOT_USERNAME=<username>
MONGO_INITDB_ROOT_PASSWORD=<password>

# For gatsby portal
STARPI_URL=http://cms:1337
ENABLE_GATSBY_REFRESH_ENDPOINT=1

KEYCLOAK_USER=<username>
KEYCLOAK_PASSWORD=<password>
# DB_ADDR=mysql use only if 'mysql name changes'

MYSQL_DATABASE=keycloak
MYSQL_USER=<username>
MYSQL_PASSWORD=<password>
MYSQL_ROOT_PASSWORD=<password>

# For node js app server
APPLICATION_PORT = 4000
KEYCLOAK_ENDPOINT=http://keycloak:8080/auth/realms/tosc/protocol/openid-connect/
KEYCLOAK_CLIENT_ID=<keycloak client id create it on first run and set it here>
KEYCLOAK_GRANT_TYPE=password
KEYCLOAK_CLIENT_SECRET=<generate the secret key after first run>
KEYCLOAK_SCOPE=openid
STRAPI_AUTH_URL=http://cms:1337/auth/local

# For react web application
TOSC_APP_SERVER_GRAPHQL=http://server:4000/__graphql
TOSC_CMS_URL=http://cms:1337/graphql
```

## 2. Setup

Since the docker compose will save the mounted DBs and config in your local machine there won't be any loss in data. However there are certian steps to be performed before the frontends can be used,

* On first run keycloak and strapi needs to be configured. Keys generated will need be used in the env file for authentication and the application to work.

* Gatsby is a static site generator so data is required to be pushed in the cms before the build can succeed. Once strapi is setup you will need to restart the container.

**Note: This project is currently under development and the docker compose and env variables are not final**