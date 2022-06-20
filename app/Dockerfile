FROM node:14-alpine as build
RUN mkdir /employee-manager-app
WORKDIR /employee-manager-app

COPY . .
RUN yarn global add @angular/cli@12.0.1 && \
    yarn install && \
    ng build --deploy-url=/employee-manager-app/ --prod


FROM nginx:alpine as app

COPY ./.nginx/nginx.conf /etc/nginx/nginx.conf
RUN rm -rf /usr/share/nginx/html/*

COPY --from=build /employee-manager-app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
