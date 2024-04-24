FROM node:18-alpine AS build

WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:18-alpine AS runtime

WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY --from=build /app/.next ./.next
COPY --from=build /app/public ./public

# Installer le pilote MySQL
RUN npm install mysql2

# Variables d'environnement pour MySQL
ENV DB_HOST=localhost
ENV DB_USER=root
ENV DB_PASSWORD=your_password
ENV DB_DATABASE=mydatabase

EXPOSE 3000
USER node
CMD ["npm", "start"]
