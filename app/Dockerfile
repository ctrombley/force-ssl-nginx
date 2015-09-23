FROM nginx

RUN rm /etc/nginx/conf.d/default.conf
ADD nginx.conf /etc/nginx/conf.d/nginx.conf
ADD kind.conf /etc/nginx/kind.conf

ADD public /var/www

EXPOSE 8088
