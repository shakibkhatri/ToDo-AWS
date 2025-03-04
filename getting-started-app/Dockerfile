# syntax=docker/dockerfile:1

FROM node:18-alpine
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn config set registry http://registry.yarnpkg.com
RUN yarn install --network-timeout 100000000 --frozen-lockfile --production
COPY . .
EXPOSE 3000
CMD ["node", "src/index.js"]