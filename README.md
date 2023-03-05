# Django + Nuxt.js + MySQL + Docker Compose 的配置設定

把 Django + Nuxt.js 的組合搭配在一起，做到前後端分離的專案

## Initial Settings

#### Docker Compose

- 建立 `.env` 檔案

    ```bash
    $ cp .env.example .env
    ```

- 編輯 `.env`
    設定 nginx 要使用的 server_name，設定好之後，在啟用 `docker-compose up` 時，就會當成變數帶入 nginx 的設定檔中 (`/etc/nginx/conf.d/my-nginx.conf`)

    ```.env
    # .env

    SERVER_NAME=localhost
    ```

#### Nginx

- 相關檔案會放在 `/nginx` 資料夾中

- 如果要使用 SSL 憑證，可以使用 [mkcert](https://github.com/FiloSottile/mkcert) 建立 local 的憑證

- 如果要調整 nginx 的配置設定，可以調整 `/nginx/conf.d/my-nginx.temp` 設定檔，這個檔案會在 `docker-compose up` 時，透過 **`envsubst`** 的方式把環境變數套入設定檔中，並建立一份 `my-nginx.conf` 檔案，讓 nginx 可以去讀取設定

#### Django

- 相關檔案會放在 `/api` 資料夾中

- Django 會使用 uwsgi 的方式運行

- 建立 `.env` 檔案給 Django 專案讀取用

    ```bash
    $ cp .env.example .env
    ```

- 建立 superuser 帳號

    ```bash
    $ python manage.py createsuperuser
    ```

- **進入後台介面**: `https://{domain}/backend/admin`

- 如果之後要打包依賴性相關套件可以使用

    ```bash
    $ pipreqs --force .
    ```

#### Nuxt.js

- 相關檔案放在 `frontend` 的資料夾中

- Hot reload

    會使用 `yarn dev` 的指令運行程式碼，所以在開發的時候，可以做到 hot reload 的效果

- **進到前台頁面**: `https://{domain}`

## 啟用 Docker Compose

```bash
$ docker compose build

# -d 會在背景執行
$ docker compose up -d
```

## 參考資料

- [docker-django-nginx-uwsgi-postgres-tutorial](https://github.com/twtrubiks/docker-django-nginx-uwsgi-postgres-tutorial)
- [Django](https://www.djangoproject.com/start/)
- [Nuxt.js](https://nuxtjs.org/docs/get-started/installation)