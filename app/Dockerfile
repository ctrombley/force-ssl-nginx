FROM nginx

RUN rm /etc/nginx/conf.d/default.conf
ADD nginx.conf /etc/nginx/conf.d/nginx.conf
ADD shared.conf /etc/nginx/shared.conf

ADD public /var/www

EXPOSE 8088
