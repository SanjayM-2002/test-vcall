# Backend Dockerfile
FROM node:20-alpine AS builder

# Set working directory
WORKDIR /app

# Install dependencies
COPY package.json package-lock.json ./
RUN npm install

# Copy source code
COPY . .

# Build the TypeScript project
RUN npm run build

# Production image
FROM node:20-alpine

WORKDIR /app

# Copy built files from the builder stage
COPY --from=builder /app/dist ./dist
COPY package.json package-lock.json ./

# Install only production dependencies
RUN npm install --omit=dev

# Expose backend port
EXPOSE 3000

# Start backend server
CMD ["node", "dist/index.js"]
