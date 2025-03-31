# Frontend Dockerfile
FROM node:20-alpine AS builder

# Set working directory
WORKDIR /app

# Install dependencies
COPY package.json package-lock.json ./
RUN npm install

# Check if vite is installed successfully
RUN npm list vite

# Copy source code
COPY . .

# Build the Vite app
RUN npm run build -- --force

# Production image
FROM node:20-alpine

WORKDIR /app

# Copy built frontend files from the builder stage
COPY --from=builder /app/dist ./dist
COPY package.json package-lock.json ./

# Install only production dependencies
RUN npm install --omit=dev

# Expose frontend port
EXPOSE 5173

# Serve the Vite app using the preview command
CMD ["npm", "run", "preview", "--", "--host", "0.0.0.0", "--port", "5173"]
