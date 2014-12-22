FROM debian:jessie

RUN apt-get update && apt-get install -y\
    curl\
    nginx-light\
    && apt-get clean

RUN echo "daemon off;" >> /etc/nginx/nginx.conf

#COPY index.html /var/www/html/

EXPOSE 80

CMD ["nginx", "-c", "/etc/nginx/nginx.conf"]
