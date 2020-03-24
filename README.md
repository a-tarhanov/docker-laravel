# Docker + Laravel

## Clone Repo

```bash
git clone https://github.com/a-tarhanov/docker-laravel.git
cd docker-laravel
```

## Build & Run

Copy .env.example to .env

```bash
docker-compose up --build -d
```

## Create App

```bash
docker-compose exec php bash

# laravel 
composer create-project --prefer-dist laravel/laravel .

# lumen 
composer create-project --prefer-dist laravel/lumen .
```

Navigate to [http://localhost:80](http://localhost:80)
