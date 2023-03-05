FROM nginx:latest

# 安裝 vim
RUN apt update -y
RUN apt install vim -y

# 安裝 bash，並且預設用 bash 開啟
RUN apt install bash	
RUN ln -sf /bin/bash /bin/sh

# 為了要使用 envsubst 的功能，可以替換 nginx.conf 的變數
RUN apt install gettext-base

COPY nginx.conf /etc/nginx/nginx.conf
COPY ./conf.d/ /etc/nginx/conf.d/