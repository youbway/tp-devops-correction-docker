FROM node:20-bookworm-slim AS build

WORKDIR /opt/front

COPY package.json ./
RUN npm install --legacy-peer-deps --no-audit --no-fund

COPY babel.config.js ./
COPY public/ public/
COPY src/ src/

ARG VUE_APP_API_URL=/api
ENV VUE_APP_API_URL=${VUE_APP_API_URL}
ENV NODE_OPTIONS=--openssl-legacy-provider

RUN npm run lint
RUN npm run build

FROM nginx:1.27-alpine

COPY default.conf /etc/nginx/conf.d/default.conf
COPY --from=build /opt/front/dist/ /usr/share/nginx/html/

EXPOSE 80
