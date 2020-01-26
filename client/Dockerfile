FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

# Since we're not using docker-compose, 
# this will tell AWS to have this listen on port 3000
FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf .etc/nginx/conf.d/default.conf
# From builder get the built version of production assets and put them into /usr
COPY --from=builder /app/build /usr/share/nginx/html
