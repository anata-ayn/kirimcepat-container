FROM node:20-alpine AS base
WORKDIR /app
COPY package*.json ./
RUN npm ci

FROM base AS test
COPY . .
RUN npm test

FROM node:20-alpine AS prod
RUN apk add --no-cache tzdata
ENV TZ=Asia/Jakarta NODE_ENV=production
WORKDIR /app
COPY package*.json ./
RUN npm ci --omit=dev
COPY src ./src
COPY migrations ./migrations
USER node
EXPOSE 8000
CMD ["node", "src/server.js"]
