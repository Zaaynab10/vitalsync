# Multi-stage build : le premier stage installe les dépendances et exécute les tests
# dans un environnement complet. Le second stage produit une image de production
# allégée, sans les dépendances de développement ni les outils de test.
# Avantage sécurité : la surface d'attaque est réduite car l'image finale ne contient
# que le strict nécessaire pour faire tourner l'application.
# Avantage taille : l'image de production est significativement plus légère
# (node:20-alpine ~ 180 Mo contre node:20 ~ 1 Go).


# --- Stage 1 : installation et tests ---
    
FROM node:20-alpine AS builder

# node:20-alpine est choisi pour sa légèreté par rapport à node:20 (image Debian complète).
# Alpine Linux est une distribution minimaliste, ce qui réduit la taille et la surface d'attaque.

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm test

# --- Stage 2 : production ---
FROM node:20-alpine AS production

WORKDIR /app

COPY package*.json ./
RUN npm install --omit=dev

COPY --from=builder /app/server.js ./

EXPOSE 3000

CMD ["node", "server.js"]
