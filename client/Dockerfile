# Client Dockerfile (React)
FROM node:18-alpine AS builder

WORKDIR /app

# Accept build argument
ARG REACT_APP_API_URL=http://localhost:5000
ENV REACT_APP_API_URL=$REACT_APP_API_URL

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy application code
COPY . .

# Build the React app
RUN npm run build

# Production stage
FROM node:18-alpine

WORKDIR /app

# Install serve to run the React app
RUN npm install -g serve

# Copy built application from builder
COPY --from=builder /app/build ./build

# Expose port
EXPOSE 3000

# Start the application
CMD ["serve", "-s", "build", "-l", "3000"]
