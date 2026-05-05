FROM node:18-alpine  As build
WORKDIR /app
COPY packege*.json ./
RUN npm ci --prefer-offline
COPY . . 
RUN npm run build


FROM nginx:1.27-alpine AS runtime

# Copy built assets
COPY --from=builder /app/dist /usr/share/nginx/html

# nginx config for SPA (React Router)
COPY nginx.conf /etc/nginx/conf.d/default.conf

HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
  CMD wget -qO- http://localhost:80/ || exit 1

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

