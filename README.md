<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
</p>

## About Project

Laravel-fpm-mysql is a fully dockerized environment for your Laravel project.

## Requirements

Docker with Compose V2

## Containers list

- **nginx** - Web server
- **php-fpm** - Workspace
- **mysql** - Database
- **traefik** - Reverse proxy (*optional*)

## Getting started

#### 1. Build images

```shell
docker compose build
```

#### 2. Run containers

```shell
docker compose up -d
```

#### 3. Access to workspace (php-fpm)

```shell
docker compose exec php-fpm bash
```

#### 4. Install dependencies

```shell
composer install
```

#### 5. Generate encryption key
```shell
php artisan key:generate
```

#### 6. Enjoy 💙

**Access to your project:** [Localhost](http://localhost)
