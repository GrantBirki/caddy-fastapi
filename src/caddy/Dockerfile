FROM caddy/caddy:2.9.1-alpine

RUN mkdir /app
COPY start.sh /app/start.sh

COPY Caddyfile /etc/caddy/Caddyfile

CMD ["sh", "/app/start.sh"]
