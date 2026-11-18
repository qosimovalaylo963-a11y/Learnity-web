# =========================================================
# LEARNITY — Full-Stack Production Dockerfile (Node.js + Python 3)
# Works out-of-the-box on Railway, Render, Fly.io, and Docker VPS
# =========================================================
FROM node:20-alpine

# Install Python 3 (with built-in sqlite3 support for sqlite_worker.py)
RUN apk add --no-cache python3 sqlite

WORKDIR /app

# Copy package files and install dependencies
COPY package.json package-lock.json ./
RUN npm install --omit=dev

# Copy full application source
COPY . .

# Ensure persistent storage directories exist with proper permissions
RUN mkdir -p /app/data/uploads /app/data/backups && chown -R node:node /app

ENV NODE_ENV=production
ENV PORT=3000
ENV DATA_DIR=/app/data
ENV DB_PATH=/app/data/learnity.sqlite
ENV UPLOAD_DIR=/app/data/uploads

USER node
EXPOSE 3000

CMD ["npm", "start"]
