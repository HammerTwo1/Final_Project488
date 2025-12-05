# --- Build stage ---
FROM node:20-alpine AS builder
WORKDIR /app

# If you add a package.json for tooling, copy it here
# COPY package*.json ./
# RUN npm ci

COPY index.html script.js style.css ./

# In this simple static case there is no "build" step,
# but this stage is where you'd run React/Next build etc.

# --- Runtime stage ---
FROM node:20-alpine AS runtime
WORKDIR /app

RUN npm install express@4

COPY --from=builder /app /app
COPY server.js /app/server.js

ENV NODE_ENV=production
ENV PORT=3000
EXPOSE 3000

USER node

CMD ["node", "server.js"]
