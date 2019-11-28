FROM node:alpine AS base
WORKDIR '/app'
COPY package.json .
RUN npm install
COPY . .
RUN npm run build

FROM nginx AS final
EXPOSE 3000
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY --from=base /app/build /usr/share/nginx/html