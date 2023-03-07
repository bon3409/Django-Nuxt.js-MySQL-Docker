FROM python:3.10

# 安裝 vim
RUN apt update -y
RUN apt install vim -y

# 安裝 bash，並且預設用 bash 開啟
RUN apt install bash	
RUN ln -sf /bin/bash /bin/sh

ENV PYTHONUNBUFFERED 1

RUN mkdir -p /var/www/html

WORKDIR /var/www/html

COPY . /var/www/html

RUN /usr/local/bin/python -m pip install --upgrade pip

RUN pip install -r requirements.txt

# 在執行 pip install 的時候不用使用 root 的權限
ENV PIP_ROOT_USER_ACTION=ignore

# 去除 windows 系統編輯文件多餘的空格
RUN sed -i 's/\r//' ./start.sh

# 給 start.sh 可以執行的權限
RUN chmod +x ./start.sh

CMD [ "/bin/bash", "start.sh" ]
