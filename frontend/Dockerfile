FROM node:18.12.1

# 安裝 vim
RUN apt update -y
RUN apt install vim -y

# 安裝 bash，並且預設用 bash 開啟
RUN apt install bash	
RUN ln -sf /bin/bash /bin/sh

ENV NODE_ENV=development

WORKDIR /var/www/html

COPY . .

RUN yarn install

ENV NUXT_HOST=0.0.0.0
ENV NUXT_PORT=3000

ENV PATH=./node_modules/.bin/:$PATH

CMD ["yarn", "dev"]
