FROM node:alpine AS base
WORKDIR '/app'
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

FROM nginx AS final
COPY --from=base /app/build /usr/share/nginx/html
