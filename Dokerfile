FROM nginx:alpine

RUN mkdir -p /etc/nginx/ssl

VOLUME /etc/nginx/ssl

COPY ./certs/homelab.crt /etc/nginx/ssl/
COPY ./certs/homelab.key /etc/nginx/ssl/

RUN echo 'server {\
    listen 80;\
    server_name localhost;\
    return 301 https://$host$request_uri;\
}\
\
server {\
    listen 443 ssl;\
    server_name localhost;\
\
    ssl_certificate /etc/nginx/ssl/homelab.crt;\
    ssl_certificate_key /etc/nginx/ssl/homelab.key;\
\
    location / {\
        root /usr/share/nginx/html;\
        index index.html;\
    }\
}' > /etc/nginx/conf.d/default.conf

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
