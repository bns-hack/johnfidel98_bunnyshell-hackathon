FROM nginx:1.15.12-alpine

RUN echo -e '''\
server {\n\
    listen 80;\n\
    \n\
    root /var/www/html;\n\
    index index.php; \n\
    access_log /var/log/nginx/access.log;\n\
    error_log /var/log/nginx/error.log;\n\
    location / {\n\
        try_files $uri $uri/ /index.php$args;\n\
    }\n\
    \n\
    location ~ \\.php$ {\n\
        try_files $uri =404;\n\
        fastcgi_split_path_info ^(.+\\.php)(/.+)$;\n\
        fastcgi_pass wp:9000;\n\
        fastcgi_index index.php;\n\
        include fastcgi_params;\n\
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;\n\
        fastcgi_param PATH_INFO $fastcgi_path_info;\n\
    }\n\
}\n\
''' > /etc/nginx/conf.d/default.conf;

