FROM node:18-alpine as base

FROM base as deps

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm ci

FROM base as build

WORKDIR app

COPY --from=deps  /app/node_modules ./node_modules

COPY . .

RUN npx nx run next-app:build:production

FROM base as app

WORKDIR app

COPY --from=build /app/dist/apps/next-app ./

RUN npm i

ENV NODE_ENV=production

ENV PORT=3000

EXPOSE 3000

CMD npm start
