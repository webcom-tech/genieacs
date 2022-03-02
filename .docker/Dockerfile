FROM node as build

WORKDIR /app

COPY . .

RUN npm install
RUN npm run build

FROM node as production

WORKDIR /app

ENV NODE_ENV=production

COPY --from=build /app/dist /app

RUN npm install

RUN apt-get update && apt-get install -y supervisor

RUN mkdir -p /var/log/supervisor
RUN mkdir -p /var/log/genieacs

COPY supervisord.conf /app/supervisord.conf

CMD ["/usr/bin/supervisord","-c","/app/supervisord.conf"]
