# Pull in dependencies with composer
FROM composer:latest as build
COPY composer.json ./
RUN composer install --ignore-platform-reqs

FROM bitnami/wordpress:6.7.0-debian-12-r2
USER root
# Install the opentelemetry and protobuf extensions

RUN apt-get update && apt-get install -y --fix-missing \
    autoconf \
    build-essential \
    gcc \
    make \
    dnsutils \
    curl \
    && rm -rf /var/lib/apt/lists/*

RUN pecl install opentelemetry protobuf
COPY otel.php.ini /opt/bitnami/php/etc/conf.d/
# Copy in the composer vendor files and autoload.php
COPY --from=build /app/vendor /var/www/otel
ENV OTEL_PHP_AUTOLOAD_ENABLED=true
ENV OTEL_SERVICE_NAME=my-wordpress-installation
ENV OTEL_EXPORTER_OTLP_ENDPOINT=http://opentelemetry-collector.default.svc.cluster.local:4318
ENV OTEL_TRACES_EXPORTER=otlp
ENV OTEL_METRICS_EXPORTER=otlp
ENV OTEL_LOGS_EXPORTER=otlp
ENV service.name=bitnami_wordpress_service
ENV service.version=f9bfeae9