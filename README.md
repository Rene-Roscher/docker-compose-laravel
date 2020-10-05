# docker-compose-laravel
A pretty simplified Docker Compose workflow that sets up a LEMP network of containers for local Laravel development. You can view the full article that inspired this repo [here](https://dev.to/aschmelyun/the-beauty-of-docker-for-local-laravel-development-13c0).

## That's works perfectly

- Don't forget to give permissions 
```bash
cd docker-compose-laravel && chmod 777 * -R
```

# Quick Start

## Installing Docker
```bash
curl -sSL https://get.docker.com/ | CHANNEL=stable sh
```

## Installing Docker-Compose
```bash
curl -L https://github.com/docker/compose/releases/download/$(curl -Ls https://www.servercow.de/docker-compose/latest.php)/docker-compose-$(uname -s)-$(uname -m) > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

## Downloading Docker-Compose Files
```bash
cd /opt && git clone https://github.com/Rene-Roscher/docker-compose-laravel
```

## Downloading Laravel Files (or your own files 😉)
```bash
cd /opt/docker-compose-laravel/src && git clone https://github.com/laravel/laravel && cd laravel && mv * .. && cd .. && rm laravel -R && cd /opt/docker-compose-laravel && chmod 777 * -R && docker-compose up -d --build && docker-compose run --rm composer update
```

## Usage

- **nginx** - `:8080`
- **mysql** - `:3306`
- **php** - `:9000`

- `docker-compose run --rm composer update`
- `docker-compose run --rm npm run dev`
- `docker-compose run --rm artisan migrate` 

## Persistent MySQL Storage

By default, whenever you bring down the Docker network, your MySQL data will be removed after the containers are destroyed. If you would like to have persistent data that remains after bringing containers down and back up, do the following:

1. Create a `mysql` folder in the project root, alongside the `nginx` and `src` folders.
2. Under the mysql service in your `docker-compose.yml` file, add the following lines:

```
volumes:
  - ./mysql:/var/lib/mysql
```
