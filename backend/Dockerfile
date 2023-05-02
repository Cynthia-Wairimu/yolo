FROM node:20.0.0-alpine3.16 

WORKDIR /yolo-back

COPY package*.json .

RUN npm ci

COPY . .

CMD ["npm", "start"]