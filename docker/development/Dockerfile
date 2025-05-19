# 1단계: 빌드
FROM node:22-alpine AS builder

WORKDIR /app
COPY package.json package-lock.json* ./
RUN npm ci

COPY . .
RUN npm run build

# 2단계: nginx 정적 서버
FROM nginx:alpine

COPY --from=builder /app/dist /usr/share/nginx/html
COPY docker/development/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
