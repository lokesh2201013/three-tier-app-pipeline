# Stage 1: Build stage
FROM node:lts-alpine AS build

WORKDIR /usr/src/app

COPY ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "./"]
RUN npm install --production --silent

# Stage 2: Production stage
FROM node:lts-alpine

ENV NODE_ENV=production
WORKDIR /usr/src/app

COPY --from=build /usr/src/app/node_modules ./node_modules
COPY . .

USER node
CMD ["node", "index.js"]
