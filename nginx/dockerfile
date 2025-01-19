# Image source
FROM nginx:alpine

# Add needed packets
# RUN apk update && apk add bash

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

# Replace the user in nginx.conf
RUN sed -i "s|user  nginx;|user  ${USERNAME};|g; s|pid /var/run/nginx.pid;|pid /tmp/nginx.pid;|g" /etc/nginx/nginx.conf

# Switch back to root
USER root

#COPY ./app/public /var/www/html

#COPY ./nginx/nginx.conf /etc/nginx/nginx.conf

#COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf