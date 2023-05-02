FROM node:20.0.0-alpine3.16 

WORKDIR /yolo

COPY package*.json .

RUN npm install

COPY . .

CMD ["npm", "start"]