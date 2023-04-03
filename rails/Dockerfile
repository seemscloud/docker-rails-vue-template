FROM ruby:3.2-alpine3.17

ENV APP_DIR="/app"

# Application Build
ARG USER_NAME="rails"
ARG USER_ID="1000"
ARG GROUP_NAME="rails"
ARG GROUP_ID="1000"

# Puma Defaults
ENV PUMA_BIND="0.0.0.0"
ENV PUMA_PORT="3000"
ENV PUMA_ENV="dev"

ARG RAILS_VERSION="7.0.4.3"

RUN apk add --no-cache bash g++ make git postgresql-dev

SHELL [ "/bin/bash", "-c" ]

RUN addgroup -g "${GROUP_ID}" "${GROUP_NAME}" && \
    adduser -s /bin/bash -h "${APP_DIR}" -G "${GROUP_NAME}" -u "${USER_ID}" -D "${USER_NAME}"

USER "${USER_NAME}"
WORKDIR "${APP_DIR}"

RUN mkdir -p src tmp && \
    gem update && \
    gem update --system && \
    gem install rails -v "${RAILS_VERSION}" && \
    gem install tzinfo-data

COPY ./docker-entrypoint.sh ./

ENTRYPOINT ["/bin/bash", "./docker-entrypoint.sh"]
