FROM node as build
WORKDIR /source
COPY package*.json yarn.lock /source/
RUN yarn install
COPY . /source/
RUN yarn build

FROM nginx
COPY --from=build /source/dist /usr/share/nginx/html
COPY ./nginx.conf /etc/nginx/nginx.conf