# Этап 1 сборка
FROM node:18-alpine AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

ENV NODE_ENV=production
ENV NODE_OPTIONS=--openssl-legacy-provider

RUN npm run build

# Этап 2 создание минимального образа
FROM nginx:alpine

# RUN addgroup -S frontendgroup && adduser -S appuser -G frontendgroup

RUN rm -rf /usr/share/nginx/html/*

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=builder /app/dist /usr/share/nginx/html/momo-store

USER nginx 

EXPOSE 80
