FROM debian:jessie

RUN apt-get update &&\
    apt-get install -y curl nginx-light
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

EXPOSE 80
CMD ["nginx", "-c", "/etc/nginx/nginx.conf"]
