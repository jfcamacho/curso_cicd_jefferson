FROM node:22-alpine AS builder

WORKDIR /app

RUN apk update && apk upgrade --no-cache && rm -rf /var/cache/apk/*

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build


FROM node:22-alpine

WORKDIR /app

ENV NODE_ENV=production

RUN apk update && apk upgrade --no-cache && rm -rf /var/cache/apk/*

COPY package*.json ./
RUN npm ci --omit=dev

COPY --from=builder /app/dist ./dist

EXPOSE 8080

USER node

CMD ["node", "dist/main"]