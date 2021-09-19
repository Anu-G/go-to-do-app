FROM node:14-alpine as immutable-dependencies
WORKDIR /client
RUN npm set progress=false && npm config set depth 0
COPY package.json package-lock.json ./
RUN npm install

FROM node:14-alpine as build
WORKDIR /client
COPY --from=immutable-dependencies /client/node_modules ./node_modules
COPY . .
RUN npm run build

FROM abdennour/nginx-distroless-unprivileged:1.18 as release
WORKDIR /opt/app
COPY --from=build --chown=1001:0 /client/conf/nginx /etc/nginx/conf.d
COPY --from=build  --chown=1001:0 /client/build/. .
EXPOSE 8081