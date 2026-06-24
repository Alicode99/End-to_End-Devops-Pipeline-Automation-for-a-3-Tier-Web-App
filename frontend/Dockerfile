# ------------------- Stage 1: Build Stage ------------------------------
FROM node:21 AS frontend-builder

WORKDIR /app

# Copy dependencies configuration
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Environment file set karna build se pehle (agar runtime par chahiye)
COPY .env.docker .env.local

# ✅ Production build banana (Yeh 'dist' ya 'build' folder generate karega)
RUN npm run build

# ------------------- Stage 2: Production Stage (Nginx) ------------------
FROM nginx:alpine

# ✅ Purane node_modules ke bajay sirf tayar shuda HTML/CSS/JS files copy karna
# Note: Agar aapka project Vite par hai toh 'dist' hoga, agar Create-React-App hai toh 'build' hoga.
COPY --from=frontend-builder /app/dist /usr/share/nginx/html

# Default Nginx HTTP Port expose karna
EXPOSE 80

# Nginx automatically background mein chal parta hai, CMD likhne ki zaroorat nahi hoti