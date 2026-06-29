# Frontend Dockerfile - multi-stage build for Next.js
# Use Node 20 because Next.js requires Node >= 20.9.0
FROM node:20-alpine AS builder
WORKDIR /app

# Install dependencies and build
COPY package*.json ./
COPY . ./
RUN npm ci
RUN npm run build

FROM node:20-alpine AS runner
WORKDIR /app
ENV NODE_ENV=production

# Copy built output and prod dependencies
COPY --from=builder /app/ .
EXPOSE 3000

# Run Next.js production server
CMD ["npm", "run", "start", "--", "-p", "3000"]
