# Nginx Unit containers for Laravel PHP Applications

## PHP 7.3
The `Dockerfile.php7` works just fine with the built-in php module that comes with unit. However, it is based of the `nginx/unit:1.21.0-full` just in case other services needed to be added.

You can find the working build at the [Docker Hub](https://hub.docker.com/r/rginnow/laravel-unit). The size of the container is approximately 760 MB.

## PHP 8.0 (build works, app does not find PHP module)
The `Dockerfile.php8` so far has the necessary components to get a running image, but the PHP 8 image at `nginx/unit:1.23.0-php8.0` does not allow installation of other PHP extensions. So, I added the Sury PHP PPA but now it will not run with the PHP module that Unit ships with. I've switched it to use the `nginx/unit:1.23.0-minimal` for now until I can build my own module for Unit.

Once I can get this working, the approximate size should be smaller than the PHP 7 build.

## Docker Compose
The `docker-compose.yml` file holds the minimum needed to launch the container. It includes a `networks` section if you use a nginx proxy or something similar.

The file also expects to be at the topmost level of your project, with a folder called `app` that holds your actual Laravel project files. However, you can rename it if you'd like by editing the `docker-compose.yml` file to match whatever you want it to be.

Example Project:

```
├── project-name-here
│   ├── app (this can be changed)
│   │   ├── app
│   │   ├── public
│   │   ├── resources
│   │   ├── package.json
│   │   ├── composer.json
│   │   └── ...(other folders and files)
└── └── docker-compose.yml
```

## Proxy Manager
If you're looking for a good proxy container, I recommend the [Nginx Proxy Manager](https://nginxproxymanager.com/)
