# Fase de construcción
FROM node:18 as builder
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build

# Imagen final ligera
FROM node:18-alpine
WORKDIR /usr/src/app

# Copiar desde builder
COPY --from=builder /usr/src/app .
COPY --from=builder /usr/src/app/node_modules ./node_modules

EXPOSE 5678
CMD ["npm", "run", "start"]
