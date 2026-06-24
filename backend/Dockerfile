# ------------------- Stage 1: Build & Prepare ------------------------------
FROM node:21 AS backend-builder

WORKDIR /app

# ✅ Pehle sirf package files copy karein (Docker caching ka faida uthane ke liye)
COPY package*.json ./

# Packages install karein (production dependencies ke liye 'npm ci' ya 'npm i' use hota hai)
RUN npm install

# Baqi saara application code copy karein
COPY . .

# ⚠️ NOTE: 'RUN npm run test' ko yahan se nikal diya hai, isko GitHub Actions handle karega.

# ------------------- Stage 2: Final Slim Production Stage ------------------
FROM node:21-slim

WORKDIR /app

# Stage 1 se poora processed app copy karein
COPY --from=backend-builder /app .

# Environment file set karein
COPY .env.docker .env

# Backend Port
EXPOSE 8080

# App run karne ki command
CMD ["npm", "start"]