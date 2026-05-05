FROM node:20-alpine AS build
WORKDIR /app
RUN npm install 
RUN npm run build

FROM alpine:latest
WORKDIR /app
COPY --from=build /app/dist ./dist


