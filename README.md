# php-node-build
Docker images with php and nodejs for build development pruposes

This Alpine based image was create to run [Particle](https://github.com/phase2/particle) (Last version v10.0.0-beta.3) on a local docker environment with `docker-compose` this image has:

* php `7.2.2`
* composer `1.6.4`
* node `8.11.1`
* npm `5.6.0`
* yarn `1.5.1`

Using this image on `docker-compose` environment

```
  theme:
    image: weknow/build-php-node
    # use the volume of your php service 
    volumes_from:
      - php
    ports:
      - '8080:8080'
    # set the working directory of the theme
    working_dir: ${DRUPAL_ROOT}/themes/custom/my_theme
```

Using this image on `docker-compose` environment with a reverse proxy (example traefik)

```
  theme:
    image: weknow/build-php-node
    volumes_from:
      - php:delegated
    labels:
      - 'traefik.backend=theme'
      - 'traefik.port=8080'
      - 'traefik.frontend.rule=Host:pl.${PROJECT_URL}'
    working_dir: ${DRUPAL_ROOT}/themes/custom/my_theme
```

If you are using a reverse proxy, you need to adding the next params on your `webpack.pl.dev` 

```
 devServer: {
    disableHostCheck: true,
    public: 'pl.mywebsite.develop' // add your host name 
 },
```
