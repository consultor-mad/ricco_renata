FROM nginx:alpine
# Copia o site
COPY . /usr/share/nginx/html

# Config simples: sempre entregar index.html (SPA-friendly)
RUN rm -f /etc/nginx/conf.d/default.conf && \
    printf 'server {\n  listen 80;\n  server_name _;\n  root /usr/share/nginx/html;\n  index index.html;\n  location / {\n    try_files $uri $uri/ /index.html;\n  }\n  location ~* \\.(png|jpg|jpeg|webp|svg|ico)$ {\n    expires 7d;\n    add_header Cache-Control "public";\n  }\n}\n' > /etc/nginx/conf.d/default.conf

EXPOSE 80
