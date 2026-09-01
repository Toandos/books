# Build stage
FROM node:24-alpine AS builder
WORKDIR /app
COPY . .
RUN npm ci
RUN npm run build

# Runtime stage
FROM node:24-alpine
WORKDIR /app
COPY --from=builder /app/package.json /app/package-lock.json ./
COPY --from=builder /app/build ./build
RUN npm ci --omit=dev
EXPOSE 3000
CMD ["node", "build"]