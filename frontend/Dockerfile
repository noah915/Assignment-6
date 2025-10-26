FROM node:18-alpine as build

WORKDIR /app

# Accept build-time Vite API URL so import.meta.env.VITE_API_URL is baked into the build
ARG VITE_API_URL
ENV VITE_API_URL=${VITE_API_URL}

COPY package*.json ./

RUN npm install

COPY . .

# Build the production assets (Vite will read VITE_API_URL from env at build time)
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]