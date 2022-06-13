FROM node:12.18.1
ENV NODE_ENV=production
WORKDIR /app
RUN apt update -y
RUN apt install nodejs -y
COPY apiCoinGeckoVue .
RUN npm install -g vue -y
RUN npm install
CMD npm run serve