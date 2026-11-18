# Backend: Node.js / Express API
FROM node:22-alpine

# Non-secret defaults only. DATABASE_URL, REDIS_URL and JWT_SECRET are
# injected at runtime by Docker Compose (never baked into the image).
ENV NODE_ENV=production \
    PORT=3000

WORKDIR /app

# Copy manifests first so the dependency layer is cached until they change
COPY package.json ./
RUN npm install --omit=dev --no-audit --no-fund \
    && npm cache clean --force

# Copy only the application source
COPY --chown=node:node src ./src

# Run as the unprivileged user shipped with the node image
USER node

EXPOSE 3000

CMD ["node", "src/server.js"]
