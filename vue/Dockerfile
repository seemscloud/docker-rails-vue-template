FROM node:18.15-alpine3.17

ENV APP_DIR="/app"

# Application Build
ARG USER_NAME="vue"
ARG USER_ID="1000"
ARG GROUP_NAME="vue"
ARG GROUP_ID="1000"

# Puma Defaults
ENV VUE_HOST="0.0.0.0"
ENV VUE_PORT="8080"
ENV VUE_ENV="dev"

ARG VUE_CLI_VERSION="5.0.8"

ENV PATH="${APP_DIR}/.yarn/bin:${PATH}"

RUN deluser --remove-home node

RUN apk add --no-cache bash g++ make git postgresql-dev

SHELL [ "/bin/bash", "-c" ]

RUN addgroup -g "${GROUP_ID}" "${GROUP_NAME}" && \
    adduser -s /bin/bash -h "${APP_DIR}" -G "${GROUP_NAME}" -u "${USER_ID}" -D "${USER_NAME}"

USER "${USER_NAME}"
WORKDIR "${APP_DIR}"

RUN mkdir -p src tmp && \
    chown "${USER_NAME}":"${GROUP_NAME}" -R src tmp && \
    yarn global add @vue/cli@"${VUE_CLI_VERSION}"

COPY ./docker-entrypoint.sh ./

ENTRYPOINT ["/bin/bash", "./docker-entrypoint.sh"]
