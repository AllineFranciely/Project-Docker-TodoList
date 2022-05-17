FROM node:14-alpine AS todobackend
WORKDIR /app
EXPOSE 3001
ADD node_modules.tar.gz ./
COPY . .
RUN npm install
CMD [ "npm", "start" ]