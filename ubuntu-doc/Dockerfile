# part de l'os ubuntu recherche dans  os ubuntu
FROM ubuntu:20.04
# lance telechargement
RUN apt update 
#lance installation nginx, php et fpm
RUN apt install -y nginx php-fpm supervisor
#definie les variables d'environnement pour nginx sur vhost 
ENV nginx_vhost /etc/nginx/sites-available/default
#defini  variables pour configurer php
ENV php_conf /etc/php/7.4/fpm/php.ini
# variable pour afficher nginx sur ubuntu
ENV nginx_conf /etc/nginx/nginx.conf
#variable pour afficher supervisor sur ubuntu
ENV supervisor_conf /etc/supervisor/supervisord.conf
# copie nginx sur virtual host dans l
COPY default ${nginx_vhost}
# lance la config de php et dans la config nginx et renomme path info pour acceder au bon chemin
RUN sed -i -e 's/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g' ${php_conf} && \
    echo "\ndaemon off;" >> ${nginx_conf}
# copie la config supervisord dans l'image en cours de creation  
COPY supervisord.conf ${supervisor_conf}
# créé un nouveau répertoire pour php fpm et modifi la propriété des repertoires en utilisateur www-data
RUN mkdir -p /run/php && \
    chown -R www-data:www-data /var/www/html && \
    chown -R www-data:www-data /run/php
#defini volume image pour monter tous répertoires sur la machine hôte
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/html"]
# defini commande conteneur par defaut a l'aide de cmd
COPY start.sh /start.sh
CMD ["./start.sh"]
#ouvre les port http/s par defaut sur le conteneur 
EXPOSE 80 443










 

