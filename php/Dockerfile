#FROM php:8.4-fpm
FROM php:8.4-fpm-alpine

# Arguments
ARG USERNAME=customuser
ARG UID=1000
ARG GID=1000

# Enviroments
ENV USERNAME=${USERNAME}
ENV UID=${UID}
ENV GID=${GID}

# Create user and group with UID and GID
RUN addgroup --system --gid ${GID} ${USERNAME} && \
    adduser --system --uid ${UID} --ingroup ${USERNAME} --shell /usr/sbin/nologin --disabled-password --no-create-home ${USERNAME}

# Replace user in configs
RUN sed -i 's/user = www-data/user = ${USERNAME}/g' /usr/local/etc/php-fpm.d/www.conf
RUN sed -i 's/group = www-data/group = ${USERNAME}/g' /usr/local/etc/php-fpm.d/www.conf

# Install needed packets
#RUN apt update && apt install -y \
#    libfreetype6-dev \
#    libjpeg62-turbo-dev \
#    libpng-dev \
#   iproute2 \
#    && docker-php-ext-configure gd --with-freetype --with-jpeg \
#   && docker-php-ext-install pdo pdo_mysql

RUN apk update && apk add --no-cache \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    iproute2 \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
   && docker-php-ext-install pdo pdo_mysql