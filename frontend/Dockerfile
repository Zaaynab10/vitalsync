# Image nginx:alpine choisie pour sa legerete et sa stabilite.
# nginx:alpine est la version Alpine de Nginx, offrant les memes performances
# que nginx:latest avec une taille d'image reduite (~25 Mo contre ~140 Mo).
FROM nginx:alpine

# Copier la configuration Nginx personnalisee
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copier les fichiers statiques du front-end
COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
