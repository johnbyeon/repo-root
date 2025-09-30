# ===== Build assets =====
FROM node:20-slim AS build
WORKDIR /app
COPY package.json package-lock.json* yarn.lock* pnpm-lock.yaml* ./
RUN npm ci || yarn install || pnpm i
COPY . .
RUN npm run build || yarn build || pnpm build

# ===== Nginx serve =====
FROM nginx:1.28.0-alpine
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]