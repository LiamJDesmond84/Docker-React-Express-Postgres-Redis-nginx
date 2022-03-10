FROM node:16-alpine as builder
WORKDIR '/app'
COPY ./package.json .
RUN npm install
COPY . .
RUN npm run build

# nginx needed for deployment as production server
FROM nginx
# For AWS Elastic Beanstalk for port mapping incoming traffic - 3000 so it hits React port first
EXPOSE 3000

# New default.conf file is changing the default port(80) that nginx listens on to 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# Copying build from above into html folder
COPY --from=0 /app/build /usr/share/nginx/html