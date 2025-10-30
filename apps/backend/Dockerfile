# Etapa 1: Build
FROM node:20 AS builder

WORKDIR /app

COPY package*.json ./
COPY prisma ./prisma/
COPY tsconfig*.json ./
COPY src ./src/

RUN npm install
RUN npx prisma generate
RUN npm run build

# Etapa 2: Runtime
FROM node:20

WORKDIR /app

COPY --from=builder /app/dist ./dist
COPY package*.json ./
COPY prisma ./prisma/

RUN npm install --omit=dev

ENV NODE_ENV=production
ENV PORT=4000

EXPOSE 4000
CMD ["node", "dist/main.js"]