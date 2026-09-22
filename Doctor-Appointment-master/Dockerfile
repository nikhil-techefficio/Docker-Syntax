# ==============================
# Stage 1: Build React frontend
# ==============================

FROM node:20-alpine AS build

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .

RUN npm run build


# ==============================
# Stage 2: Production runtime
# ==============================

FROM nginx:alpine


COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]