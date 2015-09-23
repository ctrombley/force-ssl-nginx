FROM nginx

ADD force-ssl.crt /etc/nginx/ssl/
ADD force-ssl.key /etc/nginx/ssl/

RUN rm /etc/nginx/conf.d/default.conf
ADD nginx.conf /etc/nginx/conf.d/nginx.conf

EXPOSE 8080 8443
